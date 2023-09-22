---

layout: post
title: 07. Subsonic Inflow
category: Inlet
---

# 07. Subsonic Inflow

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/11.8.png"><br>
    그림 11.8
</p>

* Subsonic Inflow 조건은 압축성 유동의 유체기계와 같은 내부유동의 입구 아음속 경계조건이다.<br>

* Mach Number, Total Pressure, Total Temperature를 입력값으로 받는다.<br>

* 각 필드는 다음의 경계조건을 사용한다.<br>
&ensp; - 압력, 속도, 온도 : subsonicInflow 조건이 사용된다.<br>
&ensp; - k : NEXT::turbulentInetnsityInletOutletTKE<br>
&ensp; - ε, ω : NEXT::viscosityRatioIneltOutletTDR<br>

* 입력값에 대한 설명은 아래와 같다.<br>
&ensp; - Flow Direction : 유동 방향이다.<br>
&ensp; - Total Pressure, P<sub>0</sub> : 경계면에서 Total Pressure을 의미한다.<br>
&ensp; - Total Temperature, T<sub>0</sub> : 경계면에서 Total Temperature을 의미한다.<br>