---
layout: post
title: baramMesh Guide
category: meshguide
---

# baramMesh Guide 

baramMesh is pre-processing (meshing) module. baramMesh means BARAM + snappyHexMesh.

It is for the users who want to make mesh of the BARAM or OpenFOAM.

And we provide the guide of baramMesh.

<ul>
  {% assign sorted_posts = site.categories.mesh | sort: 'title' %}
  {% for post in sorted_posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

* [2D Multi Region Mesh](https://drive.google.com/file/d/1e1G92wd9SFeuzXfLqCYTL9HUCeqw5Tp3/view?usp=sharing)