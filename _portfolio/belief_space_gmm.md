---
title: Learning a POMDP policy from human demonstrations
permalink: /projects/belief_space_policy/
excerpt: Learning a POMDP search policy from demonstrations
video_path: /projects/belief_pomdp/videos/air_search.wmv

header:
  teaser:  /projects/belief_pomdp/barret_search-th.png
  image:   /projects/belief_pomdp/barret_search.png

sidebar:
  - title: "Role"
    image: http://placehold.it/350x250
    image_alt: "logo"
    text: "Designer, Front-End Developer"
  - title: "Responsibilities"
    text: "Reuters try PR stupid commenters should isn't a business model"

gallery:
  - url: /projects/belief_pomdp/unsplash-gallery-image-1.jpg
    image_path: /projects/belief_pomdp/unsplash-gallery-image-1-th.jpg
    alt: "placeholder image 1"
  - url: /projects/belief_pomdp/unsplash-gallery-image-2.jpg
    image_path: /projects/belief_pomdp/unsplash-gallery-image-2-th.jpg
    alt: "placeholder image 2"
  - url: /projects/belief_pomdp/unsplash-gallery-image-3.jpg
    image_path: /projects/belief_pomdp/unsplash-gallery-image-3-th.jpg
    alt: "placeholder image 3"
---

{% include base_path %}

<!-- KaTeX -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.6.0/katex.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/KaTeX/0.6.0/katex.min.js"></script>

katex.render("c = \\pm\\sqrt{a^2 + b^2}", element);


<html>
<body>
element

</body>
</html>

# Gathering human demonstrations

A human teacher gives a demonstration on how to achieve the task (find the wooden green block on the table) given
that he is blindfolded.
<br>
<iframe width="560" height="315" src="https://www.youtube.com/embed/J5gwhKX6jcA" frameborder="0" allowfullscreen></iframe>
<br>
The position of the teacher's hand is recorded with an vision tracking system (I was using [Optitrack](http://optitrack.com/)). The
sensations the human perceives are inferred from the geometric relation of his hand with a model of the environment which
is known a priori.
<iframe width="640" height="640" src="http://www.youtube.com/embed/jgYcVh6pVdU" frameborder="0" allowfullscreen></iframe>

## Summary video

## GMM model

<iframe width="560" height="315" src="https://www.youtube.com/embed/fcjkHjOH_sE" frameborder="0" allowfullscreen></iframe>

## KUKA searching

<iframe width="560" height="315" src="https://www.youtube.com/embed/CjV6vfCSlM8" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/_lDDQ0dpAdE" frameborder="0" allowfullscreen></iframe>
