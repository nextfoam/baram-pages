---
layout: post
title: 05. Free Stream
category: Inlet
---

# 05. Free Stream

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/11.6.png"><br>
    그림 11.6
</p>

* Free Stream 조건은 플럭스의 방향에 따라 Fixed Value와 Zero Gradient가 적용되는 조건이다.<br>

* 각 필드는 다음의 경계조건을 사용한다.<br>
&ensp; - 압력 : freestreamPressure<br>
&ensp; - 속도 : freestreamVelocity<br>
&ensp; - 난류 필드값 : freestream<br>