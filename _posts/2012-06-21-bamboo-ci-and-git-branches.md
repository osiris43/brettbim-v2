---
id: 2298
title: 'Bamboo CI and Git Branches'
date: '2012-06-21T10:16:21-05:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=435'
permalink: /2012/06/21/bamboo-ci-and-git-branches/
categories:
    - Programming
tags:
    - bamboo
    - 'continuous building'
    - git
---

On the off chance that Google even indexes my blog anymore, I thought I’d write a short post about an issue we resolved with Bamboo and Git branches last week that doesn’t seem to be documented anywhere. We are using Bamboo to do continuous building (we’re not doing continuous integration because we use feature branches – that’s a topic for an entirely different post). Last week, we needed the branch name to create packages for the build artifacts. The Bamboo documentation doesn’t have anything related to git and branch name though it does say that ${repository.hg.branch} will get you the branch if you’re using Mercurial.

As it turns out, if you prefix the variable with bamboo, things start working. As in ${bamboo.repository.git.branch}. This successfully returned the branch name. As far as I can tell, this isn’t in the Bamboo documentation anywhere so it can live here for posterity (or obscurity, whichever).