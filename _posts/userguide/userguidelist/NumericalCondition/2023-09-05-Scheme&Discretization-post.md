---
layout: post
title: 1. Scheme & Discretization
category: NumericalCondition
---

# 1. Scheme & Discretization

* 해석에 사용되는 Scheme과 Discretization은 다음과 같다. <br>

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/13.1.png"><br>
    그림 13.1
</p>

&ensp; - Pressure-Velocity Coupling Scheme : SIMPLE과 SIMPLEC를 설정할 수 있다.<br>

&ensp; - Discretization Schemes<br>
&ensp; &ensp; - Time : First Order Implicit, Second Order Implicit Schemes을 선택할 수 있다.<br><br>
&ensp; &ensp; - Momentum Predictor : 운동량 보존을 만족하기 위해 속도에 대해 explicit correction을 적용한다.<br>
&ensp; &ensp;   일반적으로 Pressure Equation이 아닌 Momentum Equation을 풀기 시작하며, Momentum Predictor이라고 한다.Reynolds Number가 낮은 유동, 다상 유동 (Multiphase) Momentum Predictor를 off한다.<br><br>
&ensp; &ensp; - Momentum : First Order Upwind, Second Order Upwind 계열을 선택할 수 있다.<br><br>
&ensp; &ensp; - Energy :  First Order Upwind, Second Order Upwind 계열을 선택할 수 있다.<br><br>
&ensp; &ensp; - Turbulence : First Order Upwind, Second Order Upwind 계열을 선택할 수 있다.<br><br>
&ensp; &ensp; - Volume Fraction : First Order Upwind, Second Order Upwind 계열을 선택할 수 있다.<br><br>