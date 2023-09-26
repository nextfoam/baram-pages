---
layout: post
title: 01. Velocity Inlet
category: Inlet
---

# 01. Velocity Inlet

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/11.2.png"><br>
    그림 11.2
</p>

* Velocity Inlet 조건은 유동의 입구에 속도, 난류 필드, 온도 값을 주는 조건이다.<br><br>
* 각 필드는 다음의 경계조건을 사용한다.<br>
&ensp; - 압력 : zeroGradient<br>
&ensp; - 속도 : fixedValue<br>
&ensp; - 온도 : fixedValue<br>
&ensp; - k : NEXT::turbulentInetnsityInletOutletTKE<br>
&ensp; - ε, ω : NEXT::viscosityRatioIneltOutletTDR<br><br>
* Velocity Specification Method는 아래 2가지 방법을 사용한다.<br>
&ensp; - Component : 속도의 크기를 x, y, z축 방향 벡터로 입력한다.<br>
&ensp; - Magnitude, Normal to Boundary : 경계면에 수직한 방향으로 속도의 크기를 입력한다.<br>

* Profile Type에서 Inlet 영역의 속도, 온도 프로파일을 설정할 수 있다.<br>
&ensp; - Constant : 경계면 전체에 일정한 값을 설정한다.<br>
&ensp; - Spatial Distribution : 경계면의 위치에 따라 속도를 줄 수 있다.<br>
&ensp; 이 때, 분포는 아래와 같은 방식으로 작성된 CSV 파일 형식을 불러와야한다.<br>

|x<sub>1</sub>|y<sub>1</sub>|z<sub>1</sub>|u<sub>1</sub>|v<sub>1</sub>|w<sub>1</sub>|
|:---:|:---:|:---:|:---:|:---:|:---:|
|**x<sub>2</sub>**|**y<sub>2</sub>**|**z<sub>2</sub>**|**u<sub>2</sub>**|**v<sub>2</sub>**|**w<sub>2</sub>**|
|**x<sub>n</sub>**|**y<sub>n</sub>**|**z<sub>n</sub>**|**u<sub>n</sub>**|**v<sub>n</sub>**|**w<sub>n</sub>**|

&ensp; - Temporal Distribution : 시간에 따른 u<sub>x</sub>, u<sub>y</sub>, u<sub>z</sub>를 줄 수 있다.<br>
&ensp; 이 때, 분포는 아래와 같은 방식으로 작성된 CSV 파일 형식을 불러오거나, BARAM에서 직접 해당 형식으로 입력할 수 있다.<br>

|t|u<sub>x</sub>|u<sub>y</sub>|u<sub>z</sub>|
|:---:|:---:|:---:|:---:|
|**t<sub>1</sub>**|**u<sub>x1</sub>**|**u<sub>y1</sub>**|**u<sub>z1</sub>**|
|**t<sub>2</sub>**|**u<sub>x2</sub>**|**u<sub>y2</sub>**|**u<sub>z2</sub>**|

* Turbulence에서는 Intensity and Viscosity Ratio 혹은 k / ε, ω 값을 입력할 수 있다.