---
layout: page
title: Happy Holidays!
tagline: 
---
{% include JB/setup %}
<div class="row">
	<div class="col-md-4 post">
		<h2>Recent posts</h2>
		<ul>
		  {% for post in site.posts %}
		    {% unless post.next %}
		      <h3>{{ post.date | date: '%Y %b' }}</h3>
		    {% else %}
		      {% capture year %}{{ post.date | date: '%Y %b' }}{% endcapture %}
		      {% capture nyear %}{{ post.next.date | date: '%Y %b' }}{% endcapture %}
		      {% if year != nyear %}
		        <h3>{{ post.date | date: '%Y %b' }}</h3>
		      {% endif %}
		    {% endunless %}
		    <li><a href="{{ post.url }}">{{ post.title }}</a></li>
		  {% endfor %}
		</ul>
	</div>
	<div class="col-md-4">
		<h2>Delicious</h2>
		<div id="delicious">
			<p>Tags: <strong id="tags">drexel biomed</strong></p>
			<ul></ul>
		</div>
	</div>
	<div class="col-md-4">
		<h2>Something Else</h2>
	</div>
</div>
<script>
	var tags = $("#tags").html();
	get_delicious_json(tags, settings);
</script>
<!--
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
-->
<div class="row">
<div class="col-md-12">
<h2>About the Author</h2>

<strong>Hi!</strong> My name is David Myers, I am a digital media designer/developer. Currently I am working at Drexel University's School of Biomedical Engineering.

<h2>About this site</h2>

This site is made to keep track of projects I am working on, save resources, links, and documentation linkable/shareable with co-workers, friends, or the casual google-surfer. The theme is [jekyll bootstrap](http://github.com/plusjade/jekyll-bootstrap) and it is hosted with [github pages](http://pages.github.com/)

</div>
</div>

