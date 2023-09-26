---
layout: post
title: 05. Porous Jump
category: Misc
---

# 05. Porous Jump

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/11.17.png"><br>
    그림 11.17
</p>

* Porous Jump 조건은 계산영역 내부에 있는 cyclic 면에서 압력 변화를 주는 조건이다.<br>

* 각 필드는 다음의 경계조건을 따른다.<br>
&ensp; - 압력 : porousBafflePressure<br>
&ensp; - 나머지 : cyclic<br>

* 압력 변화는 식 11.6과 같이 계산된다.<br>

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/식 11.6.png"><br>
    식 11.6
</p>

* 입력값은 다음과 같다.<br>
&ensp; - Darcy Coefficient<br>
&ensp; - Intertial Coefficient<br>
&ensp; - Porous Media Thickness<br>