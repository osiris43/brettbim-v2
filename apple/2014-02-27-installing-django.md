---
id: 2301
title: 'Installing Django'
date: '2014-02-27T22:01:01-06:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=448'
permalink: /2014/02/27/installing-django/
categories:
    - Programming
tags:
    - django
    - python
---

This is just a page for me to remember what I did while installing Django so that when something breaks in six months, I have a point of reference.

Followed this page: [Setup Django on Lion](http://hackercodex.com/guide/python-install-django-on-mac-osx-lion-10.7/) to some degree. Worked through the tutorial on djangoproject as well.

Made changes to where site packages are created, namely ~/.local/lib/python2.7 instead of the default.

When installing virtualenv and virtualenvwrapper, I received the following error related to a virtualenvwrapper dependency on stevedore: “raise TypeError, “dist must be a Distribution instance”  
TypeError: dist must be a Distribution instance”. I fixed this by installing virtualenv, virtualenvwrapper and stevedore individually instead of with the command in the installation guide linked above.

Virtualenv sites exist in /Users/<myuser>/Sites/env.</myuser>