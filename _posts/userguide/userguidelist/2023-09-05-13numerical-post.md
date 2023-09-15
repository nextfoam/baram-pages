---
layout: post
title: 13. Numerical Conditions
category: userguidelist
---

# 13. Numerical Conditions

* 해석에 사용되는 각종 수치 조건들을 설정할 수 있다.<br>

* 각 조건들에 대한 설명은 아래와 같다. <br>

<ul>
  {% assign sorted_posts = site.categories.NumericalCondition | sort: 'title' %}
  {% for post in sorted_posts %}
    <li><a href="{{ site.baseurl }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>