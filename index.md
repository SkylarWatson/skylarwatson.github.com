---
layout: page
title: Skylar Watson
tagline: ...
---
{% include JB/setup %}
<div class="blog-index">
	{% assign post = site.posts.first %}
  	{% assign content = post.content %}

	<h1 class="entry-title">
	{% if post.title %}
	    <a href="{{ root_url }}{{ post.url }}">{{ post.title }}</a>
	{% endif %}
	</h1>
	</br>
	<div class="entry-content"><p>{{ content }}</p></div>
</div>
</br>
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


