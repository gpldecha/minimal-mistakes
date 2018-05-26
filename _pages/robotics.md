---
layout: single
title: "Robotics"
permalink: /robotics/
header:
  overlay_color: "#333"
excerpt: "A collection of robotic notes"
author_profile: false
---

{% include base_path %}

{% for post in site.robotics %}
  {% include archive-single.html %}
{% endfor %}
