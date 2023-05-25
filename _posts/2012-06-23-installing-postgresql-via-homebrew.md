---
id: 2299
title: 'Installing PostgreSQL via Homebrew'
date: '2012-06-23T17:25:01-05:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=438'
permalink: /2012/06/23/installing-postgresql-via-homebrew/
categories:
    - Programming
---

This is mostly for my edification only with little potential value for any one other than the Google overlords but maybe it will come in handy in the future.

Today, I thought I’d do some Rails dev on my football website but when I fired up rails s, I got an error related to PostgreSQL and the associated gem file. I haven’t done any rails work in 3 months but I’m pretty sure when I last left things, Postgres was working just fine. I rooted around a little in the path from the exception and apparently, Postgres had disappeared from the location the gem expected it to be in. I have no idea how that happened but that was the situation I found myself in. I spent an hour or two trying to find an installation for Postgres with little luck and finally just gave up and went to installing it with Homebrew.

I followed steps 1, 2, 4 and 5 from [this link](http://blog.dyve.net/upgrade-your-mac-to-postgres-9-using-homebrew) on upgrading PostgreSQL via Homebrew. One difference was because I wasn’t upgrading, I actually did a clean install with Homebrew. When I did this, the default user created was the same as my logged in user account instead of the standard “postgres” account. I couldn’t connect to the database server via pgAdmin because it wasn’t running so steps 4 and 5 came in handy. Homebrew installed Postgres in /usr/local/var/postgres. Once I copied my plist file from that location to Library/LaunchAgents and ran pg\_ctl -D /usr/local/var/postgres/ start, the server was back in business and I could connect with pgAdmin.

I then created the postgres login role and was back in business. rails s started fine and after several hours of learning about things like ps, launchctl and psql, I should be able to start writing some code.