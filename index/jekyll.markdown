---
layout: page
title: Jeykll
permalink: /jekyll
---

<!-- {% for jekylldoc in site.jekyll %}
<div>
  <a href="{{ jekylldoc.url | relative_url }}" class="post-link">
    <h3 class="h1 post-title">{{ jekylldoc.title }}</h3>
  </a>
</div>
{% endfor %} -->

{% assign posts_count = site.jekyll | size %}

<!-- {% include pagination.html %}<hr> -->
<div class="home">
  {% if posts_count > 0 %} 
  <div class="posts">
    {% for jekylldoc in site.jekyll %}
    <div class="post py3">
      <a href="{{ jekylldoc.url | relative_url }}" class="post-link">
        <h3 class="h1 post-title">{{ jekylldoc.title }}</h3>
      </a>
      <span class="post-summary">
        {% if jekylldoc.summary %}
        {{ jekylldoc.summary }}
        {% else %}
        <!-- {{ post.title }} -->
        {% endif %}
      </span>
    </div>
    {% endfor %}
  </div>

  <!-- <hr>{% include pagination.html %} -->
  {% else %}
  <h1 class='center'>{{ site.text.index.coming_soon }}</h1>
  {% endif %}
</div>