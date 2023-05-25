---
id: 2305
title: 'Mavericks Upgrade and Postgres Pain'
date: '2014-07-04T14:16:52-05:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=464'
permalink: /2014/07/04/mavericks-upgrade-and-postgres-pain/
categories:
    - Programming
tags:
    - homebrew
    - postgresql
    - Rails
---

[Just like the last time](http://mentalpandiculation.com/2014/03/rails-homebrew-postgres-and-the-apocalypse/) I upgraded my OS a mere 3 months ago (though after this week, it feels like a lifetime), when I upgraded to Mavericks last weekend so that the App Store upgrades would shut up about it, my PostgreSQL installation got hosed up. It took until today off and on to figure it out. It was similar to last time but this time I knew my Homebrew installation of PG was correct. I finally found the answer [here](http://stackoverflow.com/a/11678981/117502) in the comments to a previous post about a similar problem. I had to symlink an existing socket file into the location the homebrew installation was expecting it. If that sounds like I know what I’m talking about, you can forget about it because I have no idea why the socket file was in the wrong place. Still, it fixed it immediately.

I write about this only because at some point, when some other OS upgrade message beats me down, I’ll upgrade and face the same thing again. Or maybe a new problem. Who knows.