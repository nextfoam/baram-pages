---
layout: post
title: 04. Actuator Disk
category: CellZoneConditions
---

# 04. Actuator Disk

* Actuator Disk 모델은 프로펠러와 같은 회전체를 디스크로 모델링하여 속도를 소스항으로 처리한다.<br>
* BARAM v23에서는 Froude's Method와 Variable-Scaling Method을 사용할 수 있다.<br>

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/10.6.png"><br>
    그림 10.6
</p>

* 아래는 Froude's Method의 수식이다.<br>

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/식 10.3.png"><br>
    식 10.3
</p>

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/식 10.5.png"><br>
</p>

&ensp; - ρ : 유체의 밀도<br>
&ensp; - A : 디스크의 면적 (㎡)<br>
&ensp; - u<sub>m</sub> : Upsteam Point에서 유체의 속도<br>
&ensp; - n : Upstream Point의 normal Vector, 그림 10.6에서 Disk Direction이 된다.<br>
&ensp; - c<sub>p</sub> : Power Coefficient.<br>
&ensp; - c<sub>t</sub> : Thrust Coefficient.<br>

* 아래는 Variable-Scaling Method의 수식이다.<br>

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/식 10.7.png"><br>
    식 10.4
</p>

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/식 10.6.png"><br>
</p>

&ensp; - ρ : 유체의 밀도<br>
&ensp; - A : 디스크의 면적 (㎡)<br>
&ensp; - u<sub>m</sub> : Upsteam Point에서 유체의 속도<br>
&ensp; - u<sub>0</sub> : Actuator Disk의 유체 평균 속도<br>
&ensp; - n : Upstream Point의 normal Vector, 그림 10.6에서 Disk Direction이 된다.<br>
&ensp; - c<sub>p</sub> : Power Coefficient.<br>
&ensp; - c<sub>t</sub> : Thrust Coefficient.<br>