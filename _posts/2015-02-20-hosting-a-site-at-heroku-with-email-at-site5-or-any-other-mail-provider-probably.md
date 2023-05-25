---
id: 2307
title: 'Hosting A Site At Heroku With Email at Site5 (or any other mail provider probably)'
date: '2015-02-20T07:19:43-06:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=472'
permalink: /2015/02/20/hosting-a-site-at-heroku-with-email-at-site5-or-any-other-mail-provider-probably/
categories:
    - Programming
tags:
    - aws
    - email
    - Heroku
    - site5
---

My wife’s non-profit theater website, [Cry Havoc Theater](http://www.cryhavoctheater.org) was created by moi after we had a temporary dalliance with WordPress. We bought a really nice template but couldn’t figure out how to make it work well with her logos. So I built a site on sunday using Rails and Bootstrap. I hosted it on Heroku using Amazon Route 53 DNS which is my standard now that Zerigo has started charging a lot more money. This costs me about $1.11 a month per site.

The kicker to this story is that I had never bothered to set up email on [The Sports Pool Hub](http://www.thesportspoolhub.com) because I just use a non-branded Gmail account (and no one has ever signed up so it’s a moot point anyway). Because we’d originally created and hosted the site at [Site5](http://www.site5.com/) (which I totally and whole-heartedly recommend by the way for any WordPress hosting you might want to do), I had originally set up her webmail there. When she tried to log in the other day after I’d moved to Heroku, that clearly didn’t work anymore.

After spending a little time googling and thinking about the solution, I learned about MX records and I figured I could still host the mail at Site5 while the host was at Heroku. Unfortunately, there was precious little documentation on how to do that. The fantastic support team at Site5 were quick to respond to my request and after 10 minutes of configuration, I had mail back up and running at Site5. This is a reminder/tutorial for anyone else out there wanting to do the same thing. You will need the mail subdomain from your host (ours was mail.<ourdomain>.org but yours may be different). You will also need the IP address for the domain.</ourdomain>

In your AWS Dashboard, go to Route 53. Click on Hosted Zones and then go to the recordset for the zone/domain that you want to route email for. Create an A record for the mail subdomain with a value of the IP address that you received from your host. Site5 told me to set the TIL to 1 hour so feel free to choose that. Save the record.

Then create an MX record with the same Name as the A record you just created. I made the TIL the same as the A record and set the Value to “10 mail.cryhavoctheater.org”. This sets the priority the routing goes through. With only 1 option, 1 would have been fine but most of the examples I’d seen chose 10 for later flexibility. Save the record set.

Then at Site5 (or wherever the email hosting is happening), in SiteAdmin, you need to edit the MX record for the domain in question. It was originally set up as a root domain, cryhavoctheater.org. It needs to be whatever the mail subdomain was from steps 1 and 2 above. In this case, mail.cryhavoctheater.org. After propagation, which in our case was immediate, pinging your mail subdomain should result in the IP address provided by your mail provider. You can then go to <subdomain>/webmail and login.</subdomain>

The hardest part as with anything new is just figuring out the details. The implementation was pretty straightforward.