---
nav_order: 7
layout: page
title: Guides
---

Here are Guides for BARAM Users.<br>
We are providing now Korean version guides.<br>
Soon We will update as English version.<br>

<h1>baramFlow user guide</h1>

<ul>
  {% assign sorted_posts = site.categories.userguide | sort: 'title' %}
  {% for post in sorted_posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

<h1>baramFlow tutorials guides</h1>

<ul>
  {% assign sorted_posts = site.categories.tutorialguide | sort: 'title' %}
  {% for post in sorted_posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>

<h1>baramMesh tutorials guides</h1>

<ul>
  {% assign sorted_posts = site.categories.meshguide | sort: 'title' %}
  {% for post in sorted_posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>