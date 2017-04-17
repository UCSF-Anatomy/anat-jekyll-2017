---
layout: page
title: Latest News!
permalink: /news/
---
<ul class="post">
  {% for post in site.categories.news %}
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      <p class="author"><span class="date">{{ post.date | date_to_string }}</span></p>
        <p>{{post.excerpt}}</p>
        <p class="post-more"><a href="{{ post.url }}"><i class="icon-right-thin"></i>read more</a></p>
  {% endfor %}
</ul>
