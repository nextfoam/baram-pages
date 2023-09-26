---
layout: post
title: 06. Fan
category: Misc
---

# 06. Fan

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/11.18.png"><br>
    그림 11.18
</p>

* Fan 조건은 cyclic 면에 팬의 압력-유량 곡선을 (P-Q Curve) 주는 조건이다.<br>

* Fan 조건을 선택하면 압력-유량 곡선 파일을 선택하는 창이 열린다.<br>

* 여기서, csv file 형식의 압력-유량 곡선 파일을 선택하면 된다.<br>

* 각 필드는 다음의 경계조건을 따른다.<br>
&ensp; - 압력 : fanPressureJump<br>
&ensp; - 나머지 : cyclic<br>