---
layout: post
title: 04. ABL Inlet
category: Inlet
---

# 04. ABL Inlet

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/11.5.png"><br>
    그림 11.5
</p>

* ABL Inlet 조건은 대기 경계층 입구 조건이다.<br><br>

* ABL Inlet 조건의 수식은 다음과 같다.<br>

* ABL 조건은 다음 논문을 참고하였다.<br>

* D.M. Hargreaves and N.G. Wright, On the use of the k-epsilon model in commercial CFD software to model the neutral atmospheric boundary layer<br>

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/식 11.1.png"><br>
    식 11.1
</p>

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/식 11.6.png"><br>
    식 11.2
</p>

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/식 11.7.png"><br>
    식 11.3
</p>

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/식 11.4.png"><br>
    식 11.4
</p>

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/식 11.5.png"><br>
    식 11.5
</p>

* 각 기호에 대한 설명은 다음과 같다.<br>
&ensp; - U<sup>*</sup> : Friction Velocity<br>
&ensp; - κ : Von Karman's Constant<br>
&ensp; - C<sub>μ</sub> : Turbulent Viscosity Coefficient<br>
&ensp; - z : 수직 방향 좌표<br>
&ensp; - z<sub>0</sub> : Surface Roughness Height<br>
&ensp; - z<sub>ref</sub> : u<sup>*</sup>를 측정하는 Reference Height<br>
&ensp; - d : 최소 z좌표<br>
&ensp; - C<sub>1</sub> : Curve-fitting coefficient for YGCJ profiles<br>
&ensp; - C<sub>2</sub> : Curve-fitting coefficient for YGCJ profiles<br>

* 각 필드는 다음의 경계조건을 사용한다.<br>
&ensp; - 압력 : zeroGradient<br>
&ensp; - 속도 : atmBoundaryLayerInletVelocity<br>
&ensp; - k : atmBoundaryLayerInletK<br>
&ensp; - ε : atmBoundaryLayerInletEpsilon<br>

* 입력값에 대한 설명은 아래와 같다.<br>
&ensp; - Flow Direction : 주 유동 방향이다.<br>
&ensp; - Ground-Normal Direction : 땅의 Normal Vector 방향이다.<br>
&ensp; - Reference Flow Speed u<sub>ref</sub> : 위 식에서 u<sub>ref</sub>에 해당하는 값이다.<br>
&ensp; - Reference Height z<sub>ref</sub> : Reference Height<br>
&ensp; - z<sub>0</sub> : Surface Roughness Height<br>
&ensp; - Minimum z-coordinate : 최소 z좌표<br>