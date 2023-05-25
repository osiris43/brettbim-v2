---
id: 2295
title: 'Web Deployment Cage Fight &#8211; 2002 versus 2011'
date: '2011-06-16T14:01:18-05:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=354'
permalink: /2011/06/16/web-deployment-cage-fight-2002-versus-2011/
categories:
    - Programming
tags:
    - Heroku
    - Rails
    - Zerigo
---

When I first started doing web development with Visual Studio 2005, it was pretty painful work. Not only was the development itself difficult in many ways (if I say “typed DataSet” and “bloodthirsty bedbugs”, which makes you cringe more?) but the deployment of sites was often a long, tedious manual process for a site of any size. I distinctly remember having to log into my hosting provider, upload a zip file or collection of files, manually unzip or move them around and then hope that everything and the stars were lined up properly. Microsoft tried to make things easier with the Publish technology from Visual Studio but that never worked particularly seamlessly, at least not in my limited experience. On top of all that, it required considerable discipline (and a kickass source control which I’m not sure existed) if you wanted to deploy certain changes but not others.

Take a quantum leap forward into 2011. Over the last 3.5 days, I built a website to serve as my central home on the web, a place where I can aggregate my work, writing and other activities easily. I built the site in Rails, used git for source control and when it came time to deploy the site, [Heroku](http://www.heroku.com) for the hosting. To deploy my site, I had to do to things: \[sourcecode language=”bash”\]heroku create\[/sourcecode\] and \[sourcecode\]git push heroku master\[/sourcecode\] When that was done, I had a live, working test site on the internet that I could test in multiple browsers, get feedback on, etc. When I was ready to redirect my current home on the web to the new one, all I had to do was add a custom domain and Zerigo DNS add-on at Heroku, update my nameservers and presto chango, the production site was up and running.

On top of that, because branches are so painless and easy in git, I can create a new branch, work on it, merge it with the master and update the site all from the command line of my laptop. The idea of having to log into a hosting provider to upload files suddenly feels like waterboarding. If you have a significant test suite, it’s a matter of having your tests pass and then just updating your production site. Obviously, as a site grows, it won’t be quite that easy but it’s not going to get that much harder either.

The smart folks at Heroku have removed some of the major obstacles to web development so we can focus more on writing the code now and less on the administrative agony. On top of all that, for small sites like mine, the cost is negligible or non-existent. Lots of things aren’t better in 2011 than they were in 2002 (the world’s going to end next year) but web deployment, if you choose the right tools, is infinitely better in a way that’s almost inexpressible.