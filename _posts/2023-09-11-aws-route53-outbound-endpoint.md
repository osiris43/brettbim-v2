---
title: 'Building AWS Route53 Resolver Outbound Endpoints with Terraform'
layout: single 
categories:
    - Technology 
highlighter: rouge
---

At work, we are moving out of an legacy data center to AWS.  Our initial stab at that has been to stand up a staging environment that clients can use to verify changes.  Currently, we have several Docker Swarms that run different services.  These services use [Traefik](https://traefik.io/) as an application gateway to route requests from client applications.  To facilitate this, we need URLs for particular sections of our application stack like `preprod-dmz.example.com`.  

Normally, in a purely cloud environment, this would be straightforward.  We'd set up a hosted zone and utilize Route53 to create and manage these zones.  However, DNS is not something we migrating immediately and we still wanted to use [Active Directory](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/dns-and-ad-ds) to manage our DNS.  We needed a way for the EC2 instances that host the Docker Swarms to be able to resolve DNS in our on-prem domain controllers.  We explored two options, Private Hosted Zones and AWS Route53 Resolver endpoints.  In the end, the latter seemed the easiest to set up.

This post details how we went about setting this up.  As always, the AWS documentation seemed to be missing a few critical pieces for a real world app that bit us but overall, this was a pretty easy process.  We use Terragrunt and Terraform to provision infrastructure.  

One thing to note: these nodes are not currently on our domain which is why we're going this direction.  Obviously, if we joined them to the domain, DNS resolution would probably be a trivial matter.  However in the short term, we have not done that as we expect to migrate away from Docker Swarm to managed services in AWS.

AWS Route53 Resolver has two ways to manage DNS queries: Inbound and Outbound endpoints.  The former is used to send DNS queries from your on-prem network to DNS resolvers in AWS.  The latter is the opposite.  For now, we only have a use case for Outbound, e.g. sending DNS queries in the Swarms to our on-prem domain controllers.  

``` terraform 
module "resolver_sg" {
  source = "./security_group"

  name         = var.name
  description  = "Security group for forwarding endpoints in AWS Resolver"
  vpc_id       = var.vpc_id
  tags         = merge(local.tags, { Name = var.name })
  egress_rules = var.egress_rules
}
```

First, we need a security group.  This is where the one gotcha that we ran into lies.  Intuitively, and in the AWS docs, for an Outbound Endpoint, you'd assume you needed an Egress Rule of tcp(DNS) on port 53.  However, this assumption would be wrong.  More on that to follow.

``` terraform
resource "aws_route53_resolver_endpoint" "endpoint" {
  name               = var.name
  direction          = "OUTBOUND"
  security_group_ids = [module.resolver_sg.security_group.id]

  dynamic "ip_address" {
    for_each = var.domains

    content {
      subnet_id = ip_address.value.subnet_id
    }
  }

  tags = local.tags
}
```

Next, you need the endpoint definition.  In this case, it's an OUTBOUND endpoint.  We build the ip_address section dynamically based on how many domains are passed in.  

``` terraform 
resource "aws_route53_resolver_rule" "rule" {
  for_each = var.domains

  domain_name          = each.value.domain_name
  rule_type            = "FORWARD"
  name                 = each.key
  resolver_endpoint_id = aws_route53_resolver_endpoint.endpoint.id
  target_ip {
    ip = var.domain_controller_ip
  }

  tags = local.tags

}

resource "aws_route53_resolver_rule_association" "assoc" {
  for_each = aws_route53_resolver_rule.rule

  resolver_rule_id = each.value.id
  vpc_id           = var.vpc_id
}
```

Finally we build the rules that the Resolver uses to know to forward queries based on the domains.  The `target_ip` is our domain controller for this environment.  

When this Terraform was executed, it seemed to properly set up the required infrastructure.  First glance at a domain in the zone resolved the URL properly.  However, upon further examination, lots of the queries were timing out and returning a SERVFAIL when using `dig`.  

To diagnose the problem, we turned on [Resolver Query Logging](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resolver-query-logs.html).  This made the problem immediately apparent when logs like this started coming through:

``` json
 {
     "version": "1.100000",
     "account_id": "111111111",
     "region": "us-west-2",
     "vpc_id": "vpc-thevpc",
     "query_timestamp": "2023-09-11T19:01:45Z",
     "query_name": "preprod-dmz.example.com.",
     "query_type": "A",
     "query_class": "IN",
     "rcode": "SERVFAIL",
     "answers": [],
     "srcaddr": "10.100.51.140",
     "srcport": "38214",
     "transport": "UDP",
     "srcids": {
         "instance": "i-someinstanceid",
         "resolver_endpoint": "rslvr-out-resolverid"
     }
 }
```

These queries are coming across UDP and so only having Egress Rules on the security group for port 53 and TCP was clearly not going to work.  We added the UDP ports in our Terragrunt along with a CIDR restriction of our internal network and suddenly, the DNS resolution started happening on the Outbound Endpoints.

Overall, this was an easy setup with only the one gotcha.  We now have URLs successfully resolving in Docker Swarm on EC2 instances by forwarding specific queries to our own prem domain controller.