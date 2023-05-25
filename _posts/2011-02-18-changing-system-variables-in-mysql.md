---
id: 2292
title: 'Changing System Variables in MySQL'
date: '2011-02-18T17:55:22-06:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=329'
permalink: /2011/02/18/changing-system-variables-in-mysql/
categories:
    - Programming
tags:
    - 'mac dev'
    - mysql
---

Lots of fun today, dealing with what feels like the innards of MySQL but probably just barely scratches the epidermis. What I did learn today though was how to set MySQL system variables using a configuration file on Mac OSX. I figure that this will come up again and I’ll have to learn it all over again unless I write it down, thus, I’m writing it down while a 22 minute query runs on the other machine.

Today, I needed to increase the innodb\_buffer\_pool\_size value from the default 8MB to something useful for my purposes like 2 GB. You can’t do that from SqlYog or from the command line as it happens to be a readonly variable. So you need to create a configuration file. That file lives in root directory at /etc/my.cnf. I first tried to create this file using vi, got it all typed up and then when I saved it, was told that wasn’t going to fly, you don’t have the requisite permissions. Stupid \*nix operating system. Not that I’m complaining but after the day I’ve had, I would have liked to have just created the file.

So back to the command prompt and try sudo vi my.cnf. Lo and behold that works like a champ. The file looked like this when I was done:  
\[mysqld\]  
innodb\_buffer\_pool\_size=2G

Saved that, restarted the MySQL server and it had updated correctly as seen using SHOW VARIABLES;

Probably all very elementary stuff but for a guy who prefers not to get his hands dirty with database stuff, good to know for the future. Also learned about profiling which you can enable in a script in SqlYog with a SET profiling=1; at the beginning of your script and a SHOW profiles; at the end.