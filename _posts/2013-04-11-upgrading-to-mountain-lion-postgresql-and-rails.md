---
id: 1823
title: 'Upgrading To Mountain Lion, PostgreSQL and Rails'
date: '2013-04-11T05:29:39-05:00'
author: Brett
layout: single
guid: 'http://www.anexperimentinscotch.com/?p=1823'
permalink: /2013/04/11/upgrading-to-mountain-lion-postgresql-and-rails/
categories:
    - Random
    - Technology
---

I’m probably late to the party on this since Mountain Lion has been out for an internet eternity but if I ever have to do it again or if someone is a worse procrastinator than me, this will live in perpetuity in the Googleverse to aid us on out travels.

I upgraded to Mountain Lion this weekend and several things immediately went wrong. I’ve already forgotten a couple (which is why I’m writing this) but the one I ran into last night involved creating a new Rails site using PostgreSQL. When I did a “rails new”, I received the following error:

```
<pre class="shell" name="code">
Installer::ExtensionBuildError: ERROR: Failed to build gem native extension.

        /Users/osiris43/.rvm/rubies/ruby-1.9.2-p136/bin/ruby extconf.rb
checking for pg_config... yes
Using config values from /usr/bin/pg_config
checking for libpq-fe.h... *** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of
necessary libraries and/or headers.  Check the mkmf.log file for more
details.  You may need configuration options.

Provided configuration options:
	--with-opt-dir
	--without-opt-dir
	--with-opt-include
	--without-opt-include=${opt-dir}/include
	--with-opt-lib
	--without-opt-lib=${opt-dir}/lib
	--with-make-prog
	--without-make-prog
	--srcdir=.
	--curdir
	--ruby=/Users/osiris43/.rvm/rubies/ruby-1.9.2-p136/bin/ruby
	--with-pg
	--without-pg
	--with-pg-dir
	--without-pg-dir
	--with-pg-include
	--without-pg-include=${pg-dir}/include
	--with-pg-lib
	--without-pg-lib=${pg-dir}/lib
	--with-pg-config
	--without-pg-config
	--with-pg_config
	--without-pg_config
/Users/osiris43/.rvm/rubies/ruby-1.9.2-p136/lib/ruby/1.9.1/mkmf.rb:368:in `try_do': The complier failed to generate an executable file. (RuntimeError)
You have to install development tools first.
	from /Users/osiris43/.rvm/rubies/ruby-1.9.2-p136/lib/ruby/1.9.1/mkmf.rb:452:in `try_cpp'
	from /Users/osiris43/.rvm/rubies/ruby-1.9.2-p136/lib/ruby/1.9.1/mkmf.rb:853:in `block in find_header'
	from /Users/osiris43/.rvm/rubies/ruby-1.9.2-p136/lib/ruby/1.9.1/mkmf.rb:693:in `block in checking_for'
	from /Users/osiris43/.rvm/rubies/ruby-1.9.2-p136/lib/ruby/1.9.1/mkmf.rb:280:in `block (2 levels) in postpone'
	from /Users/osiris43/.rvm/rubies/ruby-1.9.2-p136/lib/ruby/1.9.1/mkmf.rb:254:in `open'
	from /Users/osiris43/.rvm/rubies/ruby-1.9.2-p136/lib/ruby/1.9.1/mkmf.rb:280:in `block in postpone'
	from /Users/osiris43/.rvm/rubies/ruby-1.9.2-p136/lib/ruby/1.9.1/mkmf.rb:254:in `open'
	from /Users/osiris43/.rvm/rubies/ruby-1.9.2-p136/lib/ruby/1.9.1/mkmf.rb:276:in `postpone'
	from /Users/osiris43/.rvm/rubies/ruby-1.9.2-p136/lib/ruby/1.9.1/mkmf.rb:692:in `checking_for'
	from /Users/osiris43/.rvm/rubies/ruby-1.9.2-p136/lib/ruby/1.9.1/mkmf.rb:852:in `find_header'
	from extconf.rb:43:in `<main>'


Gem files will remain installed in /Users/osiris43/.rvm/gems/ruby-1.9.2-p136@rails3tutorial/gems/pg-0.15.1 for inspection.
Results logged to /Users/osiris43/.rvm/gems/ruby-1.9.2-p136@rails3tutorial/gems/pg-0.15.1/ext/gem_make.out
An error occured while installing pg (0.15.1), and Bundler cannot continue.
Make sure that `gem install pg -v '0.15.1'` succeeds before bundling.
</main>
```

Several StackOverflow posts led me in different directions but eventually, I stumbled onto the following which worked: Install latest XCode, upgrading postgres using homebrew (if you aren’t using [HomeBrew](http://mxcl.github.io/homebrew/), you’re really making life hard for yourself) and then running bundle install again on the new rails app.