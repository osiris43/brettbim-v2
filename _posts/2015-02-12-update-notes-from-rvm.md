---
id: 2306
title: 'Update Notes from RVM'
date: '2015-02-12T07:11:26-06:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=469'
permalink: /2015/02/12/update-notes-from-rvm/
categories:
    - Programming
tags:
    - 'ruby rvm'
---

I figure these might come in handy and then I’d have no idea how to find them.

In case of problems: http://rvm.io/help and https://twitter.com/rvm\_io

Upgrade Notes:

 \* WARNING: You have ‘~/.profile’ file, you might want to load it,  
 to do that add the following line to ‘/Users/osiris43/.bash\_profile’:

 source ~/.profile

 \* Zsh 4.3.15 is buggy, be careful with it, it can break RVM, especially multiuser installations,  
 You should consider downgrading Zsh to 4.3.12 which has proven to work more reliable with RVM.  
 \* RVM comes with a set of default gems including ‘bundler’, ‘rake’, ‘rubygems-bundler’ and ‘rvm’ gems;  
 if you do not wish to get these gems, install RVM with this flag: –without-gems=”rvm rubygems-bundler”  
 this option is remembered, it’s enough to use it once.

 \* RVM will try to automatically use available package manager, might require `sudo`,  
 read more about it in `rvm help autolibs`

 \* If you encounter any issues with a ruby ‘X’ your best bet is to:  
 rvm get head &amp;&amp; rvm reinstall X –debug

 \* RVM will run ‘rvm requirements’ by default, to disable run:  
 echo rvm\_autolibs\_flag=0 &gt;&gt; ~/.rvmrc

 \* RVM 1.20.12 removes the automated –progress-bar from curl options,  
 if you liked this then you can restore this behavior with:

 echo progress-bar &gt;&gt; ~/.curlrc

 \* RVM will set first installed ruby as default and use it if run as function.  
 To avoid this behavior either use full path to rvm binary or prefix it with `command `.

 \* To update RVM loading code run ‘rvm get … –auto-dotfiles’

 \* RVM 1.20 changes default behavior of Autolibs to Enabled – if you prefer the 1.19 behavior  
 then run “rvm autolibs read-fail”, read more details: rvm help autolibs

 \* RVM 1.24 changes default package manager on OSX to Homebrew,  
 use `rvm autolibs macports` if you prefer Macports.

 \* RVM 1.24 changes default `–verify-downloads` flag to `1` you can get the paranoid mode again with:

 echo rvm\_verify\_downloads\_flag=0 &gt;&gt; ~/.rvmrc

 \* RVM 1.25 disables default pollution of rvm\_path/bin, you still can generate the links using:

 rvm wrapper ruby-name # or for default:  
 rvm wrapper default –no-prefix

 \* RVM 1.25.11 ‘rvm remove’ will by default remove gems, to remove only ruby use ‘rvm uninstall’