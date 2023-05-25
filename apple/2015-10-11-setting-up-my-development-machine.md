---
id: 2122
title: 'Setting Up My Development Machine'
date: '2015-10-11T06:26:11-05:00'
author: Brett
layout: single
guid: 'http://www.anexperimentinscotch.com/?p=2122'
permalink: /2015/10/11/setting-up-my-development-machine/
categories:
    - Programming
---

Two weeks ago, my laptop started crashing randomly. Without going into all the gory details, I took it to the Apple store and they wiped the drive to try and update the OS. Turns out it was a bad stick of RAM so now I’m in the position of rebuilding my dev machine. This is probably a good thing because this is the same machine from 2010 that I started my Ruby-Javascript-Clojure journey on and it was an evolutionary process with lots of genetic dead ends. So this is just a frame of reference for the future when I need to do this again with a brand new machine. Almost everyone of my regular readers can go right back to whatever they were doing before they landed here.

1\. install latest OS, currently El Capitan.  
2\. Install XCode  
3\. install Homebrew  
4\. install rbenv: brew install rbenv  
5\. install macvim: brew install macvim  
6\. install rails: brew install rails  
7\. Install postgresql: brew install postgresql  
8\. Install heroku toolkit and xcode developer kit  
9\. Install The Ultimate Vim Distribution  
10\. Drink more coffee

At this point, I’m able to work on [my main project](http://www.thesportspoolhub.com/) in my main toolset which is rails. I can deploy to Heroku, run rake tasks and not dread all the manual work I had to do when my laptop was dead. There are still a bunch of things to get back up and running full time (install Clojure, bring all my code back from backup, install [Scrivener](https://www.literatureandlatte.com/scrivener.php), write long blog post about checking the easy things like RAM first when your computer starts to wig out, etc, etc). But thanks to homebrew, setting up a dev machine in 2015 is infinitely easier than it was in 2010. Not to mention, I half way know what I’m doing now.

Resources  
https://gorails.com/setup/osx/10.11-el-capitan  
http://vim.spf13.com/