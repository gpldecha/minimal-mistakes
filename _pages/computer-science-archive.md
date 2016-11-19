---
layout: single
title: "Computer science"
permalink: /cs/

header:
  overlay_image: code2.jpg
  caption: "Photo credit: [**Unsplash**](http://feelgrafix.com/997342-code.html)"

excerpt: "A collection of computer science articles"

author_profile: true
---

{% include base_path %}

{% for post in site.cs %}
  {% include archive-single.html %}
{% endfor %}
