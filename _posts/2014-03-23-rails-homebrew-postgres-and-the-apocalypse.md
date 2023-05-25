---
id: 2302
title: 'Rails, Homebrew, Postgres And The Apocalypse'
date: '2014-03-23T09:17:30-05:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=452'
permalink: /2014/03/23/rails-homebrew-postgres-and-the-apocalypse/
categories:
    - Programming
tags:
    - homebrew
    - postgresql
    - Rails
---

Ok, it’s not the apocalypse but still. On the off chance someone ends up being in the Venn Diagram overlapping section between “broken rails environment because Homebrew upgraded Postgres” and “found my blog in Google”, this post exists. Late last week, I did a “brew update” which promptly hosed up my Rails environment locally. The error was:

> rake aborted!  
> could not connect to server: No such file or directory  
>  Is the server running locally and accepting  
>  connections on Unix domain socket “/tmp/.s.PGSQL.5432”?

This happened trying to migrate or prepare the database as well as on connection through the UI. That “.s.PGSQL.5432” file doesn’t exist in tmp which makes sense given the error message but the question was, did it get deleted on the upgrade or was something else the problem? After an extensive Google/Stack Overflow/crying jag, I went through the following stages of grief debugging.

***DENIAL: [It’s a PATH problem](http://stackoverflow.com/questions/6770649/repairing-postgresql-after-upgrading-to-osx-10-7-lion/11678981#comment8036510_6770734)***  
This seemed promising since the error was similar. I had run into something similar when I upgraded to Mountain Lion and Postgres failed to start. Apparently I didn’t fix it completely then because when I ran “brew doctor”, I did in fact get the warning about path. So I fixed that. No love unfortunately other than removing the warning from brew.

***ANGER: [It’s a Permissions problem](http://stackoverflow.com/questions/8465508/can-not-connect-to-local-postgresql)***  
Again, the error is similar though careful reading will see that the error message from the link above says “Permission denied” and not “No such file or directory”. My Stack Overflow habit (which is qualitatively different from my scotch habit) is to find a post that looks like a good candidate and go to the answers. This is probably a bad habit to be in since it lowers understanding and leads me on wild goose chases like this one. As it turns out, this is not a permissions problem. I confirmed this by restarting and using pgAdmin to access my local database. This was likely a Rails problem and had to be related to the homebrew update.

***BARGAINING:[This is a PostgreSql installation problem](http://www.postgresqlformac.com/server/howto_edit_postgresql_confi.html)***  
This one also should have been eliminated quickly but it took a little while to put the dots together. I started digging into postgres configuration of which I know way less than I should. I found the postgres.conf file using “sudo find / -name postgres.conf”. In that, the key for the unix\_socket\_directory was set to “/var/pgsql\_socket” and not to the “/tmp” directory my error message was indicating.

***DEPRESSION: [I’m going to work outside all day and not think about it](http://www.anexperimentinscotch.com/2014/03/not-enough-time-or-energy-in-the-day/)***  
Sometimes, this is the only way to fix the problem.

***ACCEPTANCE: [It’s a change in where default socket files go](http://www.postgresql.org/message-id/401084E5E73F4241A44F3C9E6FD79428265691A7@exch-01)***  
Not really a change and I haven’t completely grokked how this could be the problem. However, where Postgres looks for socket files is dependent on how it was built from source. I came across several references to the default being the /tmp directory. My best guess as to why this happened is that previous versions of Postgres installed via Homebrew correctly looked for socket files in /var/pgsql\_socket and the latest (9.2.4 at the time of writing) does not. [This Homebrew issue](https://github.com/Homebrew/homebrew/issues/14527) started me off in the right direction specifically the comments about setting PGHOST environment variable to “localhost” or setting a host in my database.yml file. However, [several places](http://stackoverflow.com/questions/6770649/repairing-postgresql-after-upgrading-to-osx-10-7-lion/11678981#comment8036510_6770734) have said that is a bad idea because it forces a TCP connection instead of a socket connection. Having no understanding of the ramifications of that, I read the [docs on PGHOST](http://www.postgresql.org/docs/9.2/static/libpq-envars.html) which state that if the setting starts with a “/”, it specifies Unix domain communication instead of TCP. So I added “export PGHOST=”/var/pgsql\_socket” to my .bash\_profile, restarted terminal and boom, a working solution that I THINK satisfies most conditions.

Things I learned through all this: more postgres configuration, searching for files by name, a little about Unix permissions, a whole lot of patience.