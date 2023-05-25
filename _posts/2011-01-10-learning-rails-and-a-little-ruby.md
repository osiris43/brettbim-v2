---
id: 2291
title: 'Learning Rails (and a little Ruby)'
date: '2011-01-10T21:47:29-06:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=324'
permalink: /2011/01/10/learning-rails-and-a-little-ruby/
categories:
    - Programming
tags:
    - Rails
    - Ruby
    - 'thinking out loud'
---

As with most of my endeavors, I suddenly decided last week out of the blue that I needed to write a web site in Rails. I don’t really recall the thought process (which should tell you there wasn’t any) that led to this decision but given the fact that I didn’t know either Rails or Ruby past what I had learned writing WATIR scripts, I knew I needed to find a good tutorial. I reached out to my extensive (read: 82 followers) Twitter network and was pointed towards the [Rails Tutorial](http://railstutorial.org) by [Karthik](http://twitter.com/#!/hkarthik). Over the past 5 days, I’ve been spending a significant amount of time on learning Rails and I have to say that I have no idea why it took me this long to come around to trying it.

Quite awhile back, I dove into learning Python and the Pylons web framework and for the most part, I was happy with it. I never deployed an app using Pylons but my Python skills got to be where I could at least make things work. I enjoy the Python language but I always felt like testing was a second class citizen to a large degree. Maybe I just never read the right tutorial but tests and deployment seemed to be an afterthought. In Python’s defense, it never seemed to have the “cool kids” momentum like Ruby/Rails. And Pylons certainly has different goals than Rails given the fact that Pylons gives you some defaults but let’s you do what you want whereas Rails has the Rails Way and it’s clear you stray from it at your own risk.

But learning Pylons especially always felt like I was stabbing at zombies in the dark. I didn’t have a good mentor other than the web and while I certainly could have read code trying to figure out best practices, I’m lazy and would at least like to have some reasonable semblance of a roadmap to guide me. With Rails in general and the Rails Tutorial linked above specifically, the road map is more like a TomTom GPS system, giving you the steps you need to create and deploy applications in Rails right from the start. The emphasis on testing, source control and deployment is refreshing since I imagine that being a major headache of writing a decent sized web application in a new framework.

The use of convention over configuration, long a selling point for Rails, is wonderful. There are so many places over the last few days where I have compared my experience in the ASP.Net world to what I was learning in Rails and found the former terribly lacking. As an example, in ASP.Net MVC, named routes have to be created explicitly but in Rails, many useful named routes are created for you based on convention.

Another place Rails seems to have the advantage is database updates as you develop an application. I just went through a situation where I had to manually define how a couple of people would deal with updates to a database while working concurrently on a project. With Rails, it’s built in through the concept of migrations. So many pieces of the plumbing that you have to deal with on normal projects is just handled. I’m sure there are gotchas waiting to jump up and bite me but for someone first learning a framework and comparing it to other experiences in the past, it’s wonderfully refreshing to find so many pieces of the puzzle are taken care of for you.

On top of that, as someone who has struggled with how to coordinate programming styles and conventions on projects in the past, imagine my excitement when I learned about the Rails Way and convention over configuration. If you just do things the Rails Way, not only are certain things taken care of for you, but you can count on Rails code being comparable across projects. Imagine reading the open source code for a couple of ASP.net projects. While ASP.Net MVC has certainly moved the slider bar over towards convention, chances are the two projects would have drastically different flavors. Yet it seems to me that Rails projects would likely be reasonably similar.

Overall, I’m thrilled (obviously since I just ran through 700 words detailing my excitement) with Rails and the potential it has in my development toolbox. While it’s certainly early and I’ve no doubt been excited about things in the past, it’s encouraging to feel comfortable in a framework to some degree right from the start. Of course, major props has to go to Michael Hartl who wrote the tutorial I’m learning from. He’s done a fantastic job of laying out a good course through the material with reasons for doing things in a particular way. I intend to buy the screencasts once I work my way through the online book because I imagine they are filled with exactly the same kind of good teaching that is available in the book.