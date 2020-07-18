---
layout: page
title: Lyric
permalink: /lyric
---

<!-- {% for lyric in site.lyrics %}
<div>
  <a href="{{ lyric.url | relative_url }}" class="post-link">
    <h3 class="h1 post-title">{{ lyric.title }}</h3>
  </a>
</div>
{% endfor %} -->

{% assign posts_count = site.lyrics | size %}

<!-- {% include pagination.html %} -->
<hr>
<div class="home">
  {% if posts_count > 0 %} 
  <div class="posts">
    {% for lyric in site.lyrics %} 
    <div class="post py3">
      <a href="{{ lyric.url | relative_url }}" class="post-link">
        <h3 class="h1 post-title">{{ lyric.title }}</h3>
      </a>
      <span class="post-summary">
        {% if lyric.summary %}
        {{ lyric.summary }}
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