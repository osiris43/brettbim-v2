---
id: 2680
title: '(Re)Learning Elixir'
date: '2020-07-15T07:55:24-05:00'
author: Brett
layout: single
guid: 'https://www.anexperimentwithoutscotch.com/?p=2680'
permalink: /2020/07/15/relearning-elixir/
spay_email:
    - ''
categories:
    - Programming
tags:
    - elixir
    - 'functional programming'
    - mix
---

I’m writing a small app in Elixir and Phoenix to better organize data from the Texas Parks and Wildlife Draw Hunt system. In theory, this will allow me to build a calendar view to see when hunts are in a more systemic manner as well as track hunts that I’ve applied for along with the results.

Some day, I’m sure that I’ll work on a personal app that doesn’t involve HTML scraping but this isn’t the day. I could have probably just built a small UI to input data manually and been done in about the same amount of time but I’m learning a ton about the Enum module in Elixir along with the API of Floki. So it’s mostly a win-win though slow going.

Today’s lessons revolved around two main blocks: how to pass a module’s function to functions in the Enum module that require it and the behavior of Mix tasks as it relates to the entire application. Writing these down here in hopes of better remembering them in the future.

For the Enum and module functions, I knew this from a video course I took by Pragmatic Programmers. You have to append your module function with the ampersand sign to make it work along with passing along the arity of the function you are calling as seen below in the 3rd line. If you try to pass it as just the function name, you’ll get a complaint from the compiler that the function doesn’t exist.

```
<pre class="wp-block-code">```elixir
 def scrape() do
    hunts = get_hunts("ADE")
    Enum.each(hunts, &parse_baglimit/1)
  end
```
```

The second issue was the behavior of Mix as it relates to the entire application. I’m writing a custom Mix task to scrape the hunt data and what was working perfectly well in my iex console failed miserably in Mix. That’s because Mix does not load the entire application in the same way that iex will. So dependencies (in this case the hackney dependency of HTTPoison) will not be loaded. Adding a line to ensure the App is loaded makes this work as in line 2 below.

```
<pre class="wp-block-code">```elixir
  def run(_) do
    Application.ensure_all_started(:hackney)
    HuntScraper.scrape()
  end
```
```

References:

[Stackoverflow and mix](https://stackoverflow.com/questions/55946337/httpoison-argumenterror-on-phoenix-mix-task)

[Stackoverflow and function passing](https://stackoverflow.com/questions/37543286/how-to-pass-a-function-to-enum-each)