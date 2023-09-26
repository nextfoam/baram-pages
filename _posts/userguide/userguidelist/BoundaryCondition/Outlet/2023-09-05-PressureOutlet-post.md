---
layout: post
title: 01. Pressure Outlet
category: Outlet
---

# 01. Pressure Outlet

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/11.10.png"><br>
    그림 11.10
</p>

* Pressure Outlet 조건은 출구 경계면에 일정한 전압력을 (Total Pressure) 주는 조건이다.<br>

* Backflow의 난류 필드와 온도 값을 설정할 수 있다.<br>

* 각 필드는 다음의 경계조건을 사용한다.<br>
&ensp; - 압력 : totalPressure<br>
&ensp; - 속도 : pressureInletOutletVelocity<br>
&ensp; - 온도 : inletOutletTotalTemperature<br>
&ensp; - k : NEXT::turbulentInetnsityInletOutletTKE<br>
&ensp; - ε, ω : NEXT::viscosityRatioIneltOutletTDR<br>

* Total Pressure에 일정한 값을 입력할 수 있다.<br>

* Calculate Backflow를 활성화하면, Backflow의 난류필드와 온도 값을 설정할 수 있다.<br>
&ensp; - Backflow Total Temperature : Backflow의 온도<br>
&ensp; - 난류 필드 : Turbulent Intensity (%)와 Turbulent Viscosity Ratio를 입력하거나 k, ε, ω값을 직접 입력할 수 있다.<br>