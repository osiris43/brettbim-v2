---
id: 2780
title: 'Change Requires System Change'
date: '2021-03-08T07:58:17-06:00'
author: Brett
layout: single
guid: 'https://www.anexperimentwithoutscotch.com/?p=2780'
permalink: /2021/03/08/change-requires-system-change/
spay_email:
    - ''
categories:
    - Technology
tags:
    - change
    - sociotechical
    - systems
---

> “Getting started begins with the simple, self-evident premise that every system is perfectly designed to deliver the results it produces.”
> 
> <cite>Paul Batalden, MD</cite>

At first glance, this seems cliche. A traffic system is perfectly designed to produce the results of safe, smooth traffic flow through an intersection. A plumbing system is perfectly designed to bring water in and take gray and black water out. A release and deploy system is perfectly designed to walk through 7 stages and take 2 days and involve 40 people even if one of the company’s stated goals is to get better at web delivery. Oops.

I came across the leading quote in Esther Derby’s excellent book, *7 Rules for Positive, Product Change: Micro Shifts, Macro Results.* At its heart, it is an idea about systems thinking, about how change must either work within the system to change the boundaries of the system or work without the system to alter the system itself. If you want to change something, you must change the system that produces the behavior you are interested in. Any effort to implement change without first taking into account the sociotechnical system within which you are operating will result in muddled results at best and failure at worst.

Where I work, we currently have an annual goal to improve Web Delivery Excellence. At this level, we can think of it more as a vision made up in some part by the following: improve the performance of our funnel and improve the engineering discipline and performance of the overall system. We’re now in March, almost into the second quarter of the year and we’ve struggled to make much headway on this vision. I’ve spent quite a bit of time thinking about this and I think it’s directly attributable to Batalden’s quote. We have a sociotechnical system that is perfectly designed to produce mediocre web delivery. This is because the system wasn’t built to produce the result of Web Delivery Excellence. It was designed to Prevent Web Delivery Crappiness. Hoping to improve web delivery without explicitly addressing the underlying system will almost certainly result in failure.

What does the underlying system look like? Fairly common in the industry, we have a two week sprint cycle. We deploy everything at the end of the sprint. We have a waterfall designed SDLC even though we call it agile in that the reporting structure of teams is in silos with competing biases, incentives and directives. Teams are not empowered in any meaningful sense. The two week long feedback cycles are far too long to make immediate changes. Each silo (engineering, QA, ops) has built processes that serve the silo’s needs quite well while managing to serve the organization’s new needs quite poorly. The system that has been built is a direct artifact of Conway’s Law which is probably a corollary of Batalden’s quote.

Much of this system, perhaps all of it, was designed to protect against Web Delivery Crappiness, to wit, QA tests three times because QA often finds broken things in different types of environments and only Ops can deploy because the production environment is sacrosanct as a way to shield failures. There are many more examples, none particularly unique in the industry as it once existed. We’re actually quite good at this process. But today, after all the research that has come out of DORA and other organizations, we know this type of system is not the way to achieve excellence.

In order to implement change in a system like this, the system itself must be the target. You cannot will “Web Delivery Excellence” into a system that was specifically designed to protect against Web Delivery Crappiness. Protecting against Crappiness is not the flip side of the coin to Implementing Excellence unfortunately. To change the outcomes of your software delivery process, you must change your software delivery system that produces those outcomes. The good news is that the process for that is straightforward. Some people even [wrote a book](https://itrevolution.com/book/accelerate/) about it.

So often in my career, I have seen agents of change completely fail because they try to operate within the same system boundaries that produce the current situation the change agents want so desperately to change. Many times, they will intuitively understand this and will try to create an entirely new system. Unfortunately, this also often ends in failure because systems have evolved over time to prevent change unless the system is specifically designed to facilitate change. This is one of the reasons why rewrites go wrong so often because the sociotechnical system that the software system runs in has evolved to produce results designed specifically around the existing software. The only way to successfully rewrite a system like this is to also rewrite or rewire the surrounding sociotechnical system to accommodate it.

Change is hard. But it is also inevitable. In order for it to be orderly, change agents must alter the system that produces the outcomes. In order to do that, we must examine the sociotechnical system that produced the current outcomes we wish to change and then take steps to alter that meta system in a way that is likely to result in different outcomes. To achieve excellence as opposed to prevent crappiness, we must realize that fear of failure is a major part of the current system and we must ameliorate that fear by creating a system that welcomes failure as a path to learning. To achieve excellence as opposed to prevent crappiness, we must reduce process to a bare minimum so that we optimize for flow and feedback instead of gates and checkpoints. Until we begin to analyze the systems within which we operate and which are perfectly designed to produce the results we now no longer appreciate, we’ll continue to fail to change the outcomes we receive.