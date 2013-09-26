---
layout: page
title: 实践小队主页
tagline: 
---
{% include JB/setup %}
<div><img src="main.jpg"></div>
<br>
<a href="map/index.html"><h3>实践地图</h3></a>
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
