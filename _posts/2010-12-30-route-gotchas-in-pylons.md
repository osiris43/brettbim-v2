---
id: 2289
title: 'Route Gotchas In Pylons'
date: '2010-12-30T16:26:29-06:00'
author: Brett
layout: single 
guid: 'http://mentalpandiculation.com/?p=310'
categories:
    - Programming
tags:
    - pylons
    - python
    - routes
---

I’ve been working on a Pylons app quite a bit lately and occasionally I run across issues that warrant documentation on the interwebs. That happened today concerning routes and how Pylons deals with them.

If you start getting an Import error that says “No module named content found”, you’ve run into it. According to the [Pylons book](http://pylonsbook.com/en/1.1/urls-routing-and-dispatch.html#unnecessary-routes-features), “Routes has a surprising legacy feature that means that if you don’t specify a controller and an action for a particular route, the implicit defaults of controller=’content’ and action=’index’ will be used for you”. This is certainly surprising to me and as always, things that are implicit tend to annoy me. Luckily, you can change this behavior. In your config/routing.py file, set map.explicit = True and then you’ll need to alter the route that is giving you problems to make the controller and action explicit. For example:

Before  
\[sourcecode language=”python”\]def make\_map(config):  
 """Create, configure and return the routes Mapper"""  
 map = Mapper(directory=config\[‘pylons.paths’\]\[‘controllers’\],  
 always\_scan=config\[‘debug’\])  
 map.minimization = False  
 map.explicit = False

 # The ErrorController route (handles 404/500 error pages); it should  
 # likely stay at the top, ensuring it can always be resolved  
 map.connect(‘/error/{action}’, controller=’error’)  
 map.connect(‘/error/{action}/{id}’, controller=’error’)

 # CUSTOM ROUTES HERE  
 map.connect(‘schedule\_entry’, ‘schedule/index/{scheduleDay}’)  
 map.connect(‘/{controller}/{action}’)  
 map.connect(‘/{controller}/{action}/{id}’)

 return map  
\[/sourcecode\]

As you can see, the default behavior is for map.explicit to be set to False. The first route under CUSTOM ROUTES HERE is a named route that to my eye should match schedule up with a controller and index up with the action. Unfortunately, instead it tries to find the default implicit controller “content” which it can’t find and that throws the ImportError listed above. To fix it do this:

After  
\[sourcecode language=”python”\]  
def make\_map(config):  
 """Create, configure and return the routes Mapper"""  
 map = Mapper(directory=config\[‘pylons.paths’\]\[‘controllers’\],  
 always\_scan=config\[‘debug’\])  
 map.minimization = False  
 map.explicit = True

 # The ErrorController route (handles 404/500 error pages); it should  
 # likely stay at the top, ensuring it can always be resolved  
 map.connect(‘/error/{action}’, controller=’error’)  
 map.connect(‘/error/{action}/{id}’, controller=’error’)

 # CUSTOM ROUTES HERE  
 map.connect(‘/schedule/index/{scheduleDay}’, controller=’schedule’, action=’index’)  
 map.connect(‘/{controller}/{action}’)  
 map.connect(‘/{controller}/{action}/{id}’)

 return map  
\[/sourcecode\]

Now the map is set to explicit and the controller and action are explicitly specified which works just fine. This all may be an artifact my novice understanding of Routes but since the book documents it this way, I guess this is the way I’m going to do it.