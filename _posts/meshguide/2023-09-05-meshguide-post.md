---
layout: post
title: BARAM-Snappy Guide
category: meshguide
---

# BARAM-Snappy Guide 

BARAM-Snappy is pre-processing (meshing) module. BARAM-Snappy means BARAM + snappyHexMesh.

And as you can guess it is based on snappyHexMesh.

So, it is for the BARAM users who want to make mesh of the BARAM or OpenFOAM.

And we provide the guide of BARAM-Snappy.

The first one if for internal flow. (Mixing Pipe)

And the second one is for outernal flow. (Drone)

<ul>
  {% assign sorted_posts = site.categories.mesh | sort: 'title' %}
  {% for post in sorted_posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>