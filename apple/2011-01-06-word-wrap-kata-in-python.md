---
id: 2290
title: 'Word Wrap Kata in Python'
date: '2011-01-06T19:16:12-06:00'
author: Brett
layout: single
guid: 'http://mentalpandiculation.com/?p=318'
permalink: /2011/01/06/word-wrap-kata-in-python/
categories:
    - Programming
tags:
    - katas
    - python
    - TDD
---

Last month at [Dallas Hack Club](http://dallashackclub.com/), we did the [Word Wrap Kata](http://thecleancoder.blogspot.com/2010/10/craftsman-62-dark-path.html) from Uncle Bob Martin’s “Clean Coder”. I got there a touch late and rapidly figured out that we were doing it in Ruby. Now, my Ruby skills are right up there with my Mandarin Chinese skills which is to say, I can’t even order a scotch or find the restroom so I quickly figured out that if I followed along, I’d be sitting in a puddle of pee wishing I was drunk. So I made the executive decision to ignore most everyone else and do it in parallel with the group but in Python since I can at least code like I’m drunk in Python.

My experience was surprisingly similar to the post linked above, e.g. I went down the hardest path trying to solve the wrong test. I’ve since gone back and deleted the code but the pseudocode went something like this:  
\[sourcecode language=”python”\]Break text into a list using a list comprehension based on the length of the column  
Start looking for words with spaces  
Try to repiece things together based on the column length and the last space  
Cry  
\[/sourcecode\]

Clearly, this wasn’t going to work. About that time, we ran out of time and went to the Flying Saucer to drink beer and pretend like we weren’t geeks. But I decided to finish the kata this week during a slow period at work. Since I didn’t have Jerry there to talk me through how dumb I was, I started reading the post up until the point where it describes writing the wrong test and spending too much time trying to solve it. So I backed up, deleted everything and started down the easier path of solving all the non-space related issues first. Once I did that, and once I figured out that recursion was going to be a big help, the project really got easier.

The final solution is below:  
\[sourcecode language=”python”\]  
def wrap(text, num):

 if len(text) &lt;= num:  
 return text  
 elif text\[num-1\] == ‘ ‘:  
 return text\[:num\].rstrip() + ‘rn’ + wrap(text\[num:\], num)  
 elif text\[:num\].find(‘ ‘) &gt; -1:  
 rightSpaceIdx = text.rfind(‘ ‘)  
 return text\[:rightSpaceIdx\] + ‘rn’ + wrap(text\[rightSpaceIdx:\].lstrip(‘ ‘), num)  
 else:  
 return text\[:num\] + ‘rn’ + wrap(text\[num:\].lstrip(), num)  
\[/sourcecode\]

It’s fascinating how quickly the algorithm starts to come together when you write the correct test. The problem is, I’m terrible at all this so it’s going to take some time getting enough experience to correctly select what test to write next. I was writing a ton of code trying to solve a problem that was too hard and the solution I eventually would have come up with would have been effective but brittle.

The more I do TDD/BDD, the more I realize that it is \*THE\* way to develop software, especially if you’re working in a dynamic language. I’m currently working through the tutorials at [Ruby Tutorials](http://rubytutorials.org) and it’s great to see that TDD is a fundamental part of the process. As I learned Python and Pylons, it was up to me to figure out best practices it seemed like and that’s workable but frustrating in the long run. I’m planning on doing more katas in an effort to improve my craft.