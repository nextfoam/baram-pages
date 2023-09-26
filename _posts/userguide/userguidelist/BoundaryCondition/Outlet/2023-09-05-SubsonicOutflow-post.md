---

layout: post
title: 03. Subsonic Outflow
category: Outlet
---

# 03. Subsonic Outflow

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/11.11.png"><br>
    그림 11.11
</p>

* Subsonic Outflow 조건은 압축성 유동의 유체기계와 같은 내부유동의 출구 아음속 경계조건이다.<br>

* Mach Number, Total Pressure, Total Temperature를 입력값으로 받는다.<br>

* 각 필드는 다음의 경계조건을 사용한다.<br>
&ensp; - 압력, 속도, 온도 : subsonicOutflow 조건이 사용된다.<br>
&ensp; - 난류 필드 : zeroGradient를 사용한다.<br>

* 입력값에 대한 설명은 아래와 같다.<br>
&ensp; - Static Pressure, P<sub>0</sub> : 경계면에서 Static Pressure을 의미한다.<br>