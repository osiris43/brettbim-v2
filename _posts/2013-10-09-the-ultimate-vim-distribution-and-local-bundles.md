---
id: 2300
title: 'The Ultimate Vim Distribution and Local Bundles'
date: '2013-10-09T16:29:11-05:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=442'
permalink: /2013/10/09/the-ultimate-vim-distribution-and-local-bundles/
categories:
    - Programming
tags:
    - CoffeeScript
    - 'The Ultimate Vim Distribution'
    - vim
    - vundle
---

I’ve been using [The Ultimate Vim Distribution](http://vim.spf13.com/) for over a year now and I love it. Because I use it mostly as configured out of the box, I struggle any time I have to update something. Today’s lesson in configuration is brought to you by the fact that I have finally broken down and decided I can’t avoid CoffeeScript anymore (mostly because the Node.js PluralSight video I’m working though uses it instead javascript – how many technologies can I reference in one post to try and get hits?). Out of the box, the vim distribution doesn’t have a plug-in for CoffeeScript syntax. However, it’s really easy to add it once you find one you like.

I picked the [first one](https://github.com/kchmck/vim-coffee-script) from a [Google search](https://www.google.com/search?q=vim+coffeescript&oq=vim+coffee&aqs=chrome.1.69i57j0l5.2849j0j7&sourceid=chrome&espvd=210&es_sm=91&ie=UTF-8) for “vim coffeescript”, always a reliable way of choosing things in my experience. I [followed the directions on adding local bundles](http://vim.spf13.com/#custom) but then got stuck when I tried to run :BundleInstall from within Vim. It seemed like it was ignoring it completely. After some floundering, the Windows <del datetime="2013-10-09T21:14:08+00:00">hostage</del> user (and [this page](https://groups.google.com/forum/#!searchin/spf13-vim-discuss/local$20bundles/spf13-vim-discuss/s_PMWxVVogM/bfBrjwYXZEwJ)) in me decided to restart Vim and restart it with “mvim +BundleInstall +BundleClean +q”. Presto chango, CoffeeScript syntax and indentation was enabled.

I found documentation for BundleInstall and BundleClean (“:h vundle” is your friend) but I have no idea what the +q does. Anyway, this post brought to you by the fact I couldn’t figure out how to fit it in 140 characters on Twitter. Also, I’m half toying with trying to do [NaNoWriMo](http://nanowrimo.org/) after a year layoff and I need to be writing a LOT more, nonfiction or otherwise.

Alternatively, I just learned about the :BundleInstall! (notice the bang on the end, Emeril would be proud) command. That can be run without restarting Vim. Yay. However, you’ll still have to restart Vim to get the syntax highlighting you’re looking for.