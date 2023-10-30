---
layout: post
title: baramMesh Guide
category: meshguide
---

# baramMesh Guide 

baramMesh is pre-processing (meshing) module. baramMesh means BARAM + snappyHexMesh.

It is for the BARAM users who want to make mesh of the BARAM or OpenFOAM.

And we provide the guide of baramMesh.

The first one if for internal flow. (Mixing Pipe)

And the second one is for outernal flow. (drivAer)

<ul>
  {% assign sorted_posts = site.categories.mesh | sort: 'title' %}
  {% for post in sorted_posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>