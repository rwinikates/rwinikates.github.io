---
layout: page
title: 
tagline: 
published: true
---
* Husband
* Technologist
* Bostonian
* Sporadic photographer

This site doesn't get used for much, but below are a few posts over the past several years.  [Find me on twitter for a more active discussion](twitter.com/rob_w).

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
