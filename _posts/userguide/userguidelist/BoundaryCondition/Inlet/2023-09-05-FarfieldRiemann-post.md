---

layout: post
title: 06. FarField Riemann
category: Inlet
---

# 06. FarField Riemann

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/11.7.png"><br>
    그림 11.7
</p>

* Farfield Riemann 조건은 압축성 유동의 원방경계에 사용하는 Riemann 경계조건이다.<br>

* 각 필드는 다음의 경계조건을 사용한다.<br>
&ensp; - 압력, 속도, 온도 : farfieldRiemann<br>
&ensp; - k : NEXT::turbulentInetnsityInletOutletTKE<br>
&ensp; - ε, ω : NEXT::viscosityRatioIneltOutletTDR<br>
&ensp; - 𝜈<sub>𝜏</sub> : NEXT::turbulentInetnsityInletOutletTKE<br>

* 입력값에 대한 설명은 아래와 같다.<br>
&ensp; - Flow Direction : 유동 방향이다.<br>
&ensp; - Mach Number, M<sub>∞</sub> : Farfield에서 Mach Number를 의미한다.<br>
&ensp; - Static Pressure, P<sub>∞</sub> : Free Stream의 압력을 의미한다.<br>
&ensp; - Static Temperature, T<sub>∞</sub> : Free Stream의 온도를 의미한다.<br>