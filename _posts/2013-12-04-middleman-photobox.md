---
layout: post
title: "Ruby + Photobox"
description: ""
category: Web
tags: [Middleman, ImageMagick]
---
{% include JB/setup %}

_Disclaimer To complete this tutorial requires a basic knowledge of the **command line** plus **git** as well as **ruby gems**._

## Step 1 - Get [Photobox](http://dropthebit.com/demos/photobox/)

{% highlight yaml %}
git clone https://github.com/yairEO/photobox.git
{% endhighlight %}

## Step 2 - Get [ImageMagick](http://imagemagick.org/script/index.php)
You may install ImageMagick any way you prefer. I am using boxen so I used the boxen puppet module to install imagemagick. 
[https://github.com/boxen/puppet-imagemagick](https://github.com/boxen/puppet-imagemagick)

## Step 3 - Create Thumbnails

[ImageMagick Thumbnail One-stop Guide](http://www.imagemagick.org/Usage/thumbnails/#fit_summery)

- `-format jpg` specify the output file format
- `-quality ##` set the amount of compression. Generally 60 is where the compression becomes noticeable and a bit pixelated. 100 is the highest quality, but also highest filesize.
- `-thumbnail` 
- `-path ~/output_path/` Specify the output path
- `-extent` forces the strict dimensions even if the dimentional ratio's are different. 
- `*.jpg` target mogrify at the files within the given directory with that extension
		
{% gist 7807974 %}

## Step 4 -  Create the Markup

Since we are using Ruby, we can use loops to automate the markup creation! Below I have integrated the loop with MiddleMan's helper functions. It loops through 100 images, plus it uses a custom helper function for numberpadding.

{% gist 7877579 %}