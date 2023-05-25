---
id: 2309
title: 'Upgrading A Reasonably Big Ruby Site Part 1 (of at least 1)'
date: '2015-05-16T15:08:39-05:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=479'
permalink: /2015/05/16/upgrading-a-reasonably-big-ruby-site-part-1-of-at-least-1/
categories:
    - Programming
tags:
    - Rails
    - rspec
    - Ruby
---

I’m in the process of upgrading [The Sports Pool Hub](http://www.thesportspoolhub.com/) to Rails 4.2 loosely following [this advice](http://technology.customink.com/blog/2014/09/16/from-rails-3.2-to-4.2/) As part of this, I’m upgrading all gems in my bundle file. Rspec has taken the most time as I apparently haven’t done much with it in quite awhile and large breaking changes in syntax have occurred specifically around the matchers like have\_selector. My controller tests have a lot of view testing in them which is probably a big smell. When I built the site, I followed Michael Hartl’s tutorial and he was doing tests around the markup in controller tests at the time so I fell into that habit.

When I first tried the upgrade last year, Guard told me I had 327 broken tests out of 541. This caused me to check everything into a branch with a commit message of “this is never going to happen”. Six months went by and I quite happily didn’t worry too much about it. However, somewhere along the way I remembered this site actually has potential if for no other reason than to increase my ability to create something cool. Also, I built the [Cry Havoc Theater](http://www.cryhavoctheater.org/) in latest Rails and realized that a lot of the Rails world had passed me by on this site. So with only baseball to amuse me, I decided to try once again to upgrade.

As it turns out, those tests are largely easy to fix and revolve around two main types. The first is that some syntax had changed in the matchers as mentioned earlier. Changing a test like this:

\[ruby\]response.should have\_selector("td", :content =&gt; "Survivor")\[/ruby\]

to code like this:

\[ruby\]expect(response.body).to have\_content("Survivor")\[/ruby\]

is straightforward if tedious. Note that because of my occasional OCD, I also migrated from the old “should” syntax to the newer and apparently more hip “expect” syntax throughout the test suite. This caused my bourbon intake to increase slightly but not noticeably. I also upgraded all places that were looking for generic inputs like links and fields using “have\_selector” to the more specific matcher “have\_link” or “have\_field”. This cleaned up the code considerably.

The other major type of test that changed were the ones that verified records were being saved to the database using the old lambda-do-end syntax. They looked like this:

\[ruby\]lambda do  
 post :add\_pool, :id =&gt; @site.id, :include\_weekly\_jackpot =&gt; "1",  
 :current\_week =&gt; 1, :current\_season =&gt; ‘2011-2012’, :weekly\_jackpot\_amount =&gt; "1",  
 :pool =&gt; {:type =&gt; ‘PickemPool’}  
 end.should change(Jackpot, :count).by(1)  
\[/ruby\]

These tests weren’t broken exactly but if you’ve been reading along carefully, you know I have OCD issues when it comes to things like deprecation warnings which this test throws. So I wanted to get everything nice and clean. I had a little trouble tracking down what to do with these tests short of deleting them out of desperation. Somewhere, I stumbled onto the matching expect syntax though:

\[ruby\] it "adds weekly jackpot to the table" do  
 expect{  
 post :add\_pool, :id =&gt; @site.id, :include\_weekly\_jackpot =&gt; "1",  
 :current\_week =&gt; 1, :current\_season =&gt; ‘2011-2012’, :weekly\_jackpot\_amount =&gt; "1",  
 :pool =&gt; {:type =&gt; ‘PickemPool’}  
 }.to change(Jackpot, :count).by(1)  
 end  
\[/ruby\]

Ah, much nicer.

This is where things currently stand. My site is woefully short on functional tests so I may write a few of those before I do the final code commit but so far, things haven’t been too bad.