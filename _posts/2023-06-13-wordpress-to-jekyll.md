---
title: 'Migrating From Wordpress to Jekyll'
layout: single 
categories:
    - Technology 
---

I have been a Wordpress user for about as long as I have been writing online.  I have blog posts going back at least to 2005.  I have always enjoyed Wordpress much to the chargrin of my more technically hip friends.  But the platform is easy to setup, easy to find hosting for and in recent years, easy to self-host on AWS with Lightsail.

The plugin architecture of Wordpress means there is always a plugin for something you need to do, whether it's email newsletter subscriptions or large exports or SEO.  If you use a hosting Platform like Wordpress.com or other popular site, the setup and maintenance over time is pretty straightforward.  You pay a little more for that but it's worth it for non-technical people.  In recent years, I've self-hosted both on Azure and AWS.  Neither of these was terribly difficult to get goin if you have experience in the web and came with a cheaper monthly price tag.  

Azure was free because I had MSDN credits through a previous company.  AWS cost about $8 a month on Lightsail.  The downsides of this cost savings was ease of updates.  The updating of Wordpress itself and the plugins remained the same, just a step you could do through the interface.  However, updating the underlying infrastructure like PHP was much less user-friendly.  In my case, using a Bitnami provided image on Lightsail meant I had to update the entire setup.  As I've gotten older and taken on other hobbies (and responsibilities like entertaining a 6 year old), updating Lightsail images took a very serious back seat on the TODO list.

So recently, during a bout of activity reduction, I decided to explore other hosting options.  [Jekyll](https://jekyllrb.com/docs/) hosted on [Github Pages](https://pages.github.com/) quickly rose to the top because I'm familiar with Ruby should I ever need to do anything beyond writing Markdown and for a site like mine is completely free.  I don't have any dynamic content, just 18 years of blathering on about things that catch my fancy.  

Setting up Jekyll was easy for anyone comfortable with Github.  I had a basic blog in about an hour.  I then found a theme I liked, [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/) which has things like post archives and a nice splash screen for the home page.  Implementing it took about another day, with off and on work.  The final step was to try and get an import of my Wordpress content without too much difficulty.  

Luckily, because the Wordpress community is pretty awesome, there is a [good plugin](https://github.com/benbalter/wordpress-to-jekyll-exporter) for exporting Wordpress content out to Markdown files in the structure expected by Jekyll.  In theory you can install the plugin and then just do the export from the UI.  However, I ran into problems with this approach where the export would never succeed.  I anticipate it's because I was on an older version of both PHP and Wordpress than maybe it supported.  There was also a mention in the issues list about a large site timing out.  Luckily, that same issue mentioned the CLI.  The developer of the plugin had actually built a CLI for the tool which is amazing.  

I connected to my Lightsail instance and found the location where the plugin had been installed by Wordpress.  Sure enough, there was the CLI which you can execute directly on the command line.  This resulted in a zip file of all content going back 18 years from my site.  I copied that off the instance, unpacked it locally and began bringing over essays.  At first, I just did one at a time to try and figure out the pattern necessary for updating the Jekyll metadata.  That quickly revealed the necessary things that had to change and I did a quick Find and Replace on the entire archive, copied them into the right spot, published it to Github and the site was live.

I anticipate that any essays from Wordpress that had links or images are probably broken but for now, just having the content was what I wanted.  This enabled me to delete the Lightsail instance, saving ~$8 a month.  Overall the process was quite easy and I'm looking forward to sporadically posting with Jekyll without having to constantly worry about the maintenance and upkeep of Wordpress and PHP.  