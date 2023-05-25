---
id: 2128
title: 'Ruby Arrays of Objects and Unions'
date: '2015-12-16T09:07:51-06:00'
author: Brett
layout: single
guid: 'http://www.anexperimentinscotch.com/?p=2128'
permalink: /2015/12/16/ruby-arrays-of-objects-and-unions/
videourl:
    - ''
    - ''
    - ''
categories:
    - Programming
---

I’m working through the [Advent of Code](http://adventofcode.com/) and needed to union two Ruby arrays of objects together based on some properties on said objects. I wasn’t having much luck getting it to work and my Google fu was failing but I finally figured out the issue and want to post it here in case someone else ever manages to search using the right terms.

The key here is that you can’t just override `eql?`. You have to also override the `hash` method. So for a Position class, it might look like this:

```
<pre class="lang:ruby decode:true " title="Overriding eql? and hash">class Position
  attr_reader :x, :y

  def hash
    [@x, @y].hash
  end

  def initialize(coord=[])
    if coord==[]
      @x = 0
      @y = 0
    else
      @x = coord[0]
      @y = coord[1]
    end
  end

  def eql?(other_object)
    @x == other_object.x && @y == other_object.y
  end
end
```

This would allow the union of two arrays of Position objects to only include Positions that are unique by X and Y coordinates.