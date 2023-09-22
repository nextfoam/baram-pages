---
layout: post
title: 02. Flow Inlet
category: Inlet
---

# 02. Flow Inlet

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/11.3.png"><br>
    그림 11.3
</p>

* Flow Rate Inlet 조건은 유동의 입구에 질량유량 혹은 체적유량, 난류, 온도 값을 주는 경계조건이다.<br><br>
* 유량과 온도는 constant값만 입력할 수 있다.<br><br>
* 각 필드는 다음의 경계조건을 사용한다.<br>
&ensp; - 압력 : zeroGradient<br>
&ensp; - 속도 : flowRateInletVelocity<br>
&ensp; - 온도 : fixedValue<br>
&ensp; - k : NEXT::turbulentInetnsityInletOutletTKE<br>
&ensp; - ε, ω : NEXT::viscosityRatioIneltOutletTDR<br>

* Flow Rate Specification Method는 아래 2가지 방법을 사용한다.<br>
&ensp; - Mass Flow Rate : Inlet 경계면에 질량유량을 입력한다.<br>
&ensp; - Volume Flow Rate : Inlet 경계면에 체적유량을 입력한다.<br>

* Turbulence에서는 Intensity and Viscosity Ratio 혹은 k / ε, ω 값을 입력할 수 있다.