---
layout: post
title: 05. Cylinder
category: tutorials
---

# Cylinder 

## * [격자 파일 다운로드](https://drive.google.com/file/d/1KwU6-RFIv__nr8ovKGfNDX7g9ewrBJTy/view?usp=sharing)

## 1) 개요 
* 본 예제는 비정상상태 비압축성 유동해석 예제이다.<br>

* 직경이 1m인 2차원 실린더 주변의 박리 유동을 예측하는 문제이다. <br>

* 유동은 층류이며 레이놀즈 수는 100이다.<br>

* 격자는 Ansys Fluent .msh 형식의 파일을 사용한다.<br>

* OpenFOAM에서 2차원 격자는 자동적으로 3차원 격자로 변환된다.<br>
이 때, z축으로 새로 생긴 앞뒤 단면은 frontAndBackPlanes이란 이름으로 정의되고, Empty 경계 조건으로 정의한다.<br>

* 아래 그림에서 형상과 격자를 나타내었다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.1.png"><br>
</p>

계산 조건은 다음과 같다. <br>

●  solver : buoyantPimpleNFoam (넥스트폼이 개발한 비압축성 유동 해석 솔버) <br>

●  난류 모델 : laminar<br>

●  밀도 : 1𝑘𝑔/㎥ <br>

●  점성 계수 : 0.01𝑘𝑔/𝑚s <br>

●  속도 : 1m/s  <br>

BARAM을 실행하면 아래 과정을 따라서 case 파일을 만든다.<br>

●  New Case버튼 클릭<br>

●  Project Name : cylinder<br>

●  Flow Type : incompressible<br>

●  Multiphase Model : Off<br>

● Species Model : Not Include<br>

## 2) 격자
격자는 주어진 Ansys의 .msh 파일을 활용한다. <br>
상단 탭에서 File - Load Mesh - Fluent Mesh (ASCII) 순서대로 클릭하고 cylinder.msh 파일을 선택한다. <br>

## 3) 계산 조건
### (1) General
Time을 Transient로 변경한다.<br>
나머지는 Default로 설정한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.2.png"><br>
</p>

### (2) Models
난류 모델은 Laminar 모델을 사용하고 나머지는 Default를 사용한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.3.png"><br>
</p>

### (3) Materials
본 예제에서는 레이놀즈 수가 100이 되는 조건으로 물성치를 설정한다.<br>

●  밀도 : 1𝑘𝑔/㎥ <br>

●  점성 계수 : 0.01𝑘𝑔/𝑚s <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.4.png"><br>
</p>

### (4) Cell Zone Conditions
Cell Zone Conditions은 Default 조건을 사용한다.<br>

### (5) Boundary Conditions
아래와 같이 경계면 타입과 경계값을 설정한다.<br>

***●  cylinder : Wall***<br>
```Velocity Condition : No Slip```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.5.png"><br>
</p>

***●  sym : Symmetry***<br>

***●  out : Pressure Outlet***<br>
```Total Pressure : 0 (Pa)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.6.png"><br>
</p>

***●  in : Velocity Inlet***<br>
```Velocity Specification Method : Magnitudde, Normal to Boundary```<br>
```Profile Type : Constant```<br>
```Velocity Magnitude : 1 (m/s)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.7.png"><br>
</p>

***●  frontAndBackPlanes : Empty***<br>

### (6) Reference Values
본 예제에서는 cylinder의 Drag Coefficient와 Lift Coefficient를 확인한다.<br>
그러기 위해 Reference Values를 아래와 같이 설정한다.<br>

●  Area : 1  <br>

●  Density : 1  <br>

●  Length : 1  <br>

●  Pressure : 0  <br>

●  Velocity : 1  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.8.png"><br>
</p>

### (7) Numerical Conditions
Numerical Conditions은 다음과 같이 설정한다.<br>

●  Use Momentum Predictor : 활성화<br>

●  Discretization Schemes<br>
```Time : Second Order Implicit```<br>
```Momentum : Second Order Upwind```<br>

●  Max iterations per Time Step : 10<br>

●  나머지는 Default 조건을 사용한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.9.png"><br>
</p>

### (9) Monitoring
본 예제에서는 다음 2가지를 모니터링한다.<br>

1. cylinder에 작용하는 Drag Coefficient와 Lift Coefficient<br>
Add - Forces 버튼을 선택한다.<br>
Force Monitoring은 아래와 같이 설정한다.<br>

●  Write Interval : 1<br>

●  Lift Direction : 0 1 0<br>

●  Drag Direction : 1 0 0<br>

●  Center of Rotation : 0 0 1<br>

●  Boundaries : cylinder<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.10.1.png"><br>
</p>

2. cylinder중심에서 1m 떨어진 지점의 속도, 압력<br>
Add - Points 버튼을 선택한다.<br>
Point Monitoring은 아래와 같이 설정한다.<br>

●  Write Interval : 1<br>

●  Field : Pressure<br>

●  Coordinate : 1 0 0<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.10.2.png"><br>
</p>

같은 방식으로 동일한 지점의 Velocity Magnitude 모니터링도 설정한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.10.3.png"><br>
</p>

### (10) Initialization
●  X-Velocity : 1<br>
이외 값들은 Default값을 사용한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.11.png"><br>
</p>

### (11) Run
Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.<br>

●  Time Stepping Method : Adaptive  <br>

●  Max Courant Number : 1  <br>

●  End Time : 150  <br>

●  Data Write Format : Binary  <br>

●  Number of Cores : 4  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.12.png"><br>
</p>

계산이 완료된 Residuals<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.13.1.png"><br>
</p>

모니터링되는 항력계수, 양력계수, 속도, 압력 그래프<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.13.2.png"><br>
</p>

## 4) 후처리

### (1) 스칼라 분포
Cylinder 주변의 속도, 압력 분포를 확인한다.<br>
External tools의 parview 버튼을 클릭하여 paraview를 실행한다.<br>

Case Type을 Decomposed Case로 변경한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.14.png"><br>
</p>

상단 툴바의 Solid Color를 U 혹은 p_rgh로 변경하고 play 버튼을 클릭한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.15.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.16.png"><br>
</p>