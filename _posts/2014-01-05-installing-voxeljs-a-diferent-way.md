---
layout: post
title: "Installing Voxel.js a diferent way"
description: ""
category: 
tags: []
---
{% include JB/setup %}

{% highlight bash %}
mkdir voxel-engine
cd voxel-engine
npm init
npm install voxel-engine --save-dev
{% endhighlight %}

create index.js and link the voxeljs module. Then create the constructor function.
{% highlight javascript %}
var createGame = require("voxel-engine");
var game = createGame();
{% endhighlight %}

{% highlight html %}
<!doctype html>
<html>
  <body>
    <script src="bundle.js"></script>
  </body>
</html>
{% endhighlight %}

{% highlight javascript %}
var createGame = require("voxel-engine");
var game = createGame();
var container = document.body;
game.appendTo(container);
{% endhighlight %}

{% highlight bash %}
npm install voxel-player --save-dev
{% endhighlight %}

Now create the player.
{% highlight javascript %}
var createGame = require("voxel-engine");

var game = createGame();
var container = document.body;
game.appendTo(container);

var createPlayer = require("voxel-player");
var dude = createPlayer(dude.png)(game);

dude.possess();
dude.yaw.position.set(0,100,0)
{% endhighlight %}

Compile
{% highlight bash %}
browserify index.js -o bundle.js
{% endhighlight %}

Getting tired of compiling everytime you want to play a game? Browserify does have a watch function, but the tool "Browservefy" does creates a local development server and compiles your JavaScript automatically with browserify.

{% highlight bash %}
npm install browservefy --save-dev
{% endhighlight %}

Then drop this in your `package.json` file right above the devDependencies section.
{% highlight json %}
"scripts": {
	"start": "echo \"open localhost:8080/\" && .node_modules/.bin/browservefy index.js 8080 -- -d"
},
{% endhighlight %}


{% highlight bash %}
{% endhighlight %}

{% highlight javascript %}
{% endhighlight %}
