---
layout: post
title: "reveal js slideshows"
description: ""
category: Drexel
tags: [october]
---
{% include JB/setup %}

### Things
**Requires an IE7 fallback**
- Reveal.js is [IE8+ compatible](https://github.com/hakimel/reveal.js/wiki/Browser-Support), so the IE7 fallback will be a downloadable PDF file.

- This means a conditional html statement must be installed. I am exploring [a programatic way to do this in Ruby](http://stackoverflow.com/questions/5809917/conditional-tag-wrapping-in-rails-erb).

- [Quirksmode](http://www.quirksmode.org/css/condcom.html) has a nice resource on html conditional comments.

**Looping through slideshow images**
- I will have the ability to loop through each slide with a ruby loop. Since each image is named predictably as "Slide##.jpg" and the reveal syntax is repeatable, automation is possible.