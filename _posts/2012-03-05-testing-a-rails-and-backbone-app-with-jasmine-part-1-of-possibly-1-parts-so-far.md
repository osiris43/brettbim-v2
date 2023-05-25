---
id: 2297
title: 'Testing A Rails and Backbone App with Jasmine &#8211; Part 1 (of possibly 1 parts so far)'
date: '2012-03-05T17:48:48-06:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=380'
permalink: /2012/03/05/testing-a-rails-and-backbone-app-with-jasmine-part-1-of-possibly-1-parts-so-far/
categories:
    - Programming
tags:
    - backbone
    - jasmine
    - Rails
    - 'unit testing'
---

I’ve been playing around with [Backbone.js](http://documentcloud.github.com/backbone/) in my Rails work but I haven’t gotten around to testing the Backbone code until today. There are quite a few tutorials out there but my basic setup took some digging around and I thought I’d document the steps I took to get a brand new Rails app in a state where I could test the JavaScript code I’m writing.

My application is going to be an ESPN Headline browser essentially using the [ESPN Developer API](http://developer.espn.com/). This API really isn’t very interesting in that it gives about zero useful information to non-paying developers but there isn’t much I can do about that. If you want to follow along, you’ll need to request an API key from ESPN. This first part doesn’t involve any actual calls to ESPN so you can skip that step for now. All the code for this app is up on [Github](https://github.com/osiris43/espn_api_toy).

I’m using the Rails 3.1.3 and the lastest Jasmine code. The first thing you need to do is install the jasmine gem by adding it to your Gemfile  
\[sourcecode language=”rails”\]group :test do  
 gem ‘jasmine’  
end\[/sourcecode\]

Once that’s done, run “bundle install”.

There is some jasmine initialization that needs to happen once the gem has been installed so run “bundle exec jasmine init”. This will create configuration files for jasmine as well as some sample tests and javascript that you can safely delete. At the time of publication of this post, Jasmine seems to still be expecting an earlier version of Rails because the generated code ends up in the “public” folder and the configuration files all reference that generated code. If you’re using Rails 3.1.3 and the new asset folders, you just need to update the jasmine.yml file in spec/javascripts/support to reference those folders. More on that in a minute.

Once we have the gem installed, we can write our first test. I’m following the convention of [this guy](https://github.com/froots/backbone-jasmine-examples) and arranging my test code into spec/javascripts/\*\* and my javascript into app/assets/javascripts/\*\* where \*\* will match models, collections, views, etc. Fire up the Jasmine test runner by executing:  
\[sourcecode language=”rails”\]rake jasmine\[/sourcecode\]  
and then hit localhost:8888 in your browser. You should see something like this:

[![](http://mentalpandiculation.com/wp-content/uploads/2012/03/initialtests1-1024x625.png "initialtests1")](http://mentalpandiculation.com/2012/03/testing-a-rails-and-backbone-app-with-jasmine-part-1-of-possibly-1-parts-so-far/initialtests1/)

Those five tests are the sample ones that Jasmine created. A conscientious developer would delete those but I’m lazy. Plus, it makes me feel better that five tests already pass. Now, we’re ready to write our first test. I created Headline.spec.js in spec/javascripts/models to contain the test code for my Headline Backbone model.

\[sourcecode language=”javascript”\]describe("Headline model", function () {  
 beforeEach(function() {  
 this.headline = new Headline({  
 headline: "My Headline",  
 description: "a description",  
 source: "ESPN News",  
 byline: "Brett Bim"  
 });  
 });

 describe("when instantiated", function() {  
 it("exhibits the attributes", function() {  
 expect(this.headline.get("headline")).toEqual("My Headline");  
 });  
 });

});\[/sourcecode\]

This is a really basic test that in actuality is testing Backbone functionality more than code but it’s a good first starting point to make sure everything is set up correctly. Refresh localhost:8888 and you’ll find out it’s not.

[![](http://mentalpandiculation.com/wp-content/uploads/2012/03/firstfail-1024x268.png "firstfail")](http://mentalpandiculation.com/2012/03/testing-a-rails-and-backbone-app-with-jasmine-part-1-of-possibly-1-parts-so-far/firstfail/)

As you can see, Headline is not defined which is expected given that we haven’t defined it yet. Let’s do that now. Create Headline.js in app/assets/javascripts/models and add this code to it:

\[sourcecode language=”javascript”\]var Headline = Backbone.Model.extend();\[/sourcecode\]

This creates our model. Save the file and refresh localhost:8888. Surprisingly, you get the same failed test. This is because the Jasmine gem does not automatically reflect the asset structure from Rails 3.1.3. You need to explicitly specify where your files are. You can do this by going to spec/javascripts/support and opening the jasmine.yml file. There is a section for source files. You need to tell it where your source files are and add references to backbone.js and underscore.js as well.

\[sourcecode language=”bash”\]src\_files:  
 – public/javascripts/prototype.js  
 – public/javascripts/effects.js  
 – public/javascripts/controls.js  
 – public/javascripts/dragdrop.js  
 – app/assets/javascripts/underscore.js  
 – app/assets/javascripts/backbone.js  
 – public/javascripts/application.js  
 – public/javascripts/\*\*/\*.js  
 – app/assets/javascripts/\*\*/\*.js\[/sourcecode\]

I’ve added the three lines pointing to app/assets which will inform Jasmine where to find those files. Once that’s done and the file is saved, we can refresh localhost:8888 again.

[![](http://mentalpandiculation.com/wp-content/uploads/2012/03/finaltests-1024x78.png "finaltests")](http://mentalpandiculation.com/2012/03/testing-a-rails-and-backbone-app-with-jasmine-part-1-of-possibly-1-parts-so-far/finaltests/)

And our first test passes. We should now have Jasmine up and running for testing all our Backbone code. Stay tuned for another episode of “One Post Every 8 Months About Random Crap” where we discuss writing tank driving software using Lisp.