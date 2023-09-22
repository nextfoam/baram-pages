---
layout: post
title: 01. Inlet
category: BoundaryCondition
---

# 01. Inlet

<ul>
  {% assign sorted_posts = site.categories.Inlet | sort: 'title' %}
  {% for post in sorted_posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>