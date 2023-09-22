---
layout: post
title: 02. Porous Zone
category: CellZoneConditions
---

# 02. Porous Zone

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/10.3.png"><br>
    그림 10.3
</p>

* Porous Zone은 다공성 성질을 가진 영역을 모사하는 해석 기법이다.<br>
* Porous Model로는 Darcy-Forchheimer와 Power Law 두 가지가 있다.<br>

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/식 10.1.png"><br>
    식 10.1
</p>

* Darcy-Forchheimer Model의 식은 식 10.1과 같다.<br>
&ensp; - Direction-1 Vector, Direction-2 Vector : 압력 손실 방향은 1, 2 벡터에 의해 결정된다.<br>
&ensp; - d : Viscous Resistance Coefficient이다. 벡터로 입력하며 단위는 1/㎡.<br>
&ensp; - f : Inertial Resistance Coefficient이다. 벡터로 입력하며 단위는 1/m.<br>
&ensp; - ρ : 유체의 밀도<br>
&ensp; - U : 유체의 속도<br>

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/10.4.png"><br>
    그림 10.4
</p>

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/식 10.2.png"><br>
    식 10.2
</p>

* Power Law의 식은 식 10.2과 같다.<br>
&ensp; - ρ : 유체의 밀도<br>
&ensp; - U : 유체의 속도<br>
&ensp; - C0, C1 : 상수<br>