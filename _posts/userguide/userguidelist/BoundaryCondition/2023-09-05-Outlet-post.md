---
layout: post
title: 02. Outlet
category: BoundaryCondition
---

# 02. Outlet

<ul>
  {% assign sorted_posts = site.categories.Outlet | sort: 'title' %}
  {% for post in sorted_posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>