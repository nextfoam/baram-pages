---
layout: post
title: 11. Boundary Condtions
category: userguidelist
---

# 11. Boundary Condtions

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/11.1.png"> <img src="https:nextfoam.co.kr/baramManual/userguide/11.png"><br>
    그림 11.1
</p>

* Boundary Conditions에서 경계면에 해당하는 face의 조건을 바꿀 수 있다.<br>

* BARAM v23에서 제공하는 Boundary Condition의 종류는 총 21가지이다. <br>

<ul>
  {% assign sorted_posts = site.categories.BoundaryCondition | sort: 'title' %}
  {% for post in sorted_posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>