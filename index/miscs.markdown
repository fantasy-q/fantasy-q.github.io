---
layout: default
title: Miscs
permalink: /miscellaneous
---

{% assign posts_count = site.miscs | size %}

{% include pagination.html %}<hr>
<div class="home">
  {% if posts_count > 0 %} 
  <div class="posts">
    {% for post in site.miscs %} 
    <div class="post py3">
      <a href="{{ post.url | relative_url }}" class="post-link">
        <h3 class="h1 post-title">{{ post.title }}</h3>
      </a>
      <span class="post-summary">
        {% if post.summary %}
        {{ post.summary }}
        {% else %}
        {{ post.title }}
        {% endif %}
      </span>
    </div>
    {% endfor %}
  </div>

  <hr>{% include pagination.html %}
  {% else %}
  <h1 class='center'>{{ site.text.index.coming_soon }}</h1>
  {% endif %}
</div>