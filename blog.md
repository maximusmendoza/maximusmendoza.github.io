---
layout: page
title: My Personal Ramblings
permalink: /blog/
---

Welcome to my blog! Here you'll find my thoughts on anything and everything.

{% for post in site.posts %}
  <article class="post-preview">
    <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
    <p class="post-meta">{{ post.date | date: "%B %d, %Y" }}</p>
    {{ post.excerpt }}
    <a href="{{ post.url | relative_url }}" class="read-more">Read More...</a>
  </article>
{% endfor %}

