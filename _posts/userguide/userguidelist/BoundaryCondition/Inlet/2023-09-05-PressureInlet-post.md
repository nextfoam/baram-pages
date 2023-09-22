---
layout: post
title: 03. Pressure Inlet
category: Inlet
---

# 03. Pressure Inlet

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/11.4.png"><br>
    그림 11.4
</p>

* Pressure Inlet 조건은 입구 경계면에 일정한 전압력을 (Total Pressure) 주는 조건이다.<br><br>
* 각 필드는 다음의 경계조건을 사용한다.<br>
&ensp; - 압력 : totalPressure<br>
&ensp; - 속도 : pressureInletOutletVelocity<br>
&ensp; - 온도 : inletOutletTotalTemperature<br>
&ensp; - k : NEXT::turbulentInetnsityInletOutletTKE<br>
&ensp; - ε, ω : NEXT::viscosityRatioIneltOutletTDR<br>

* Total Pressure, Temperature에 일정한 값을 입력할 수 있다.<br>

* Turbulence에서는 Intensity and Viscosity Ratio 혹은 k / ε, ω 값을 입력할 수 있다.