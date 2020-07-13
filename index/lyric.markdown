---
layout: page
title: Lyric
permalink: /lyric
---

{% for lyric in site.lyrics %}
<div>
  <a href="{{ lyric.url | relative_url }}" class="post-link">
    <h3 class="h1 post-title">{{ lyric.title }}</h3>
  </a>
</div>
{% endfor %}

