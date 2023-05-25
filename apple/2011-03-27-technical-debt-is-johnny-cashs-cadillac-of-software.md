---
id: 2293
title: 'Technical Debt Is Johnny Cash&#8217;s Cadillac Of Software'
date: '2011-03-27T21:22:48-05:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=331'
permalink: /2011/03/27/technical-debt-is-johnny-cashs-cadillac-of-software/
categories:
    - Programming
tags:
    - architecture
    - design
    - 'technical debt'
---

<iframe allowfullscreen="" frameborder="0" height="390" loading="lazy" src="http://www.youtube.com/embed/sIuo0KIqD_E" title="YouTube video player" width="480"></iframe>

For those of you who aren’t country music fans, Johnny Cash sings about working in the the GM plant and building a Caddy one piece at a time by bringing the pieces home in his lunch pail over a number of years. In the end, he puts the car together and while he has a functioning, hot-rod Cadillac, it’s a bit, how shall we say, bolted together with duct tape and bailing wire. I can only imagine what it would be like to perform repairs on a car that’s built from a variety of parts over 10 or 15 years. It seems like a far fetched system but in the software world, it’s exactly what you get in a system that ignores technical debt over time to focus on delivery of features.

There’s been [some](http://www.m3p.co.uk/blog/2010/07/23/bad-code-isnt-technical-debt-its-an-unhedged-call-option/) [writing](http://blog.jayfields.com/2011/03/types-of-technical-debt.html) lately on metaphors for technical debt which has caused me to think about what it means to have bad, messy, untested code in a system of any size. I think the idea of Johnny’s Caddy is an excellent metaphor for explaining both what technical debt is and how it affects the functionality and maintainability of a system. When you have three headlights and no tail fins, the car still runs but it’s a little odd looking. But when you try to dig into the guts and replace a ’52 carburetor bolted onto a a ’62 intake manifold, you’re going to have to have extremely specialized system knowledge about the car you are working on. If the original mechanic gets hit by a bus, the new guy can’t go to AutoZone and pick up a ’49, ’50, ’51, ’52, ’53, ’54, ’55, ’56, ’57, ’59 Caddy manual.

The same thing holds true for a system that’s been continually extended over a number of years to do more and more things for its users. If the code is never revisited to make it more maintainable or flexible and if it was originally written without consideration for future changes, the system becomes brittle and difficult to understand. Without a manual (either the domain knowledge of the original system builders or tests to protect developers from unintended consequences), modifying the system can become rather hazardous. Over time, if no attempts are made to bring the code into some semblance of normalcy, the system can even get to the point where it can’t be changed for fear of the [consequences](http://chadfowler.com/2011/03/17/leaving-a-legacy-system).

One thing to keep in mind, technical debt is a sign of success. Without the continual driver of success, systems don’t evolve to the point of having technical debt. But it’s important to always be aware of the debt, of its force and effect on the flexibility and maintainability of the system. Without constant attention, eventually the system becomes fragile and unstable, breaking unexpectedly when changes are made to seemingly unrelated sections of the app. Without some sort of design, either architectural through an initial design phase or protective through the use of solid tests, the system development is likely to eventually come to a slow halt because of the interrelatedness of the pieces.