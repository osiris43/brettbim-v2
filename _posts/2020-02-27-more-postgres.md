---
id: 2618
title: 'More Postgres'
date: '2020-02-27T05:40:15-06:00'
author: Brett
layout: single
guid: 'http://www.anexperimentinscotch.com/?p=2618'
permalink: /2020/02/27/more-postgres/
categories:
    - Technology
tags:
    - postgresql
---

In my [long suffering](https://www.anexperimentinscotch.com/?s=postgres), ongoing battle with Postgres running locally on the Mac installed via Homebrew, I fired it up a couple of weeks ago to start on a new project only to find it again didn’t run for some reason even though Homebrew said the service was running, as it always does. I’m not even sure what I did to fix it this time ([upgraded](https://stackoverflow.com/questions/17822974/postgres-fatal-database-files-are-incompatible-with-server), restarted, [created a db](https://stackoverflow.com/questions/17633422/psql-fatal-database-user-does-not-exist), created a user, [remove the process pid file](https://stackoverflow.com/questions/39710384/cannot-connect-to-postgres-server-running-through-brew-services), who knows) but what I do know is that in the future, FIND THE LOG FILES FIRST.

That was the key to the solution as it always is. I don’t know why I always look for logs when I’m at work but then don’t think about it when I’m working on my own tools.

Anyway, on my current system, I can find the log here:

atom /usr/local/var/log/postgres.log

And in it you’ll (and by you, I mean future Brett) find useful information that might help debug the problem.