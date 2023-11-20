---
layout: post
title: User Guide
category: userguide
---


# User Guide 

Here is the User guide for BARAM Users.<br>

Thank you.

<ul>
  {% assign sorted_posts = site.categories.userguidelist | sort: 'title' %}
  {% for post in sorted_posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>