---
layout: post
title: Porous Jump
category: tutorials
---

# Porous Jump 

* [격자 파일](https://drive.google.com/file/d/1c7RgueGF8kfG_pqA0tGbU_TbPpZ99tNG/view?usp=sharing)

## 1) 개요 
* 본 예제는 계산영역 내부에 porous media 혹은 fan을 두께가 없는 경계면으로 모사할 수 있는 Porous Jump 경계조건 예제이다.<br>

* 육면체 덕트 내부에 사각형의 면을 만들고 Porous Jump 경계조건을 사용하여 압력이 증가되고 속도가 높아지는 문제이다. <br>

* 격자는 주어진 OpenFOAM 격자를 사용한다.<br>

* 아래 그림에서 형상과 격자를 나타내었다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.1.png"><br>
</p>

계산 조건은 다음과 같다. <br>

●  solver : buoyantsimpleNFoam (넥스트폼이 개발한 비압축성 유동 해석 솔버) <br>

●  난류 모델 : 𝑘 − ε <br>

●  밀도 : 1.225𝑘𝑔/㎥ <br>

●  점성 계수 : 1.79e-5𝑘𝑔/𝑚s <br>

●  Porous 경계 조건<br>
```Darcy Coefficient : -100```<br>
```Inertial Coefficient : -5```<br>
```porous media in the flow direction : 0.05 (m)```<br>

Porous Jump를 계산하는 porousBafflePressure 경계조건은 아래 식을 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.2.png"><br>
</p>

BARAM을 실행하면 아래 과정을 따라서 case 파일을 만든다.<br>

●  New Case버튼 클릭<br>

●  Project Name : porousJump<br>

●  Flow Type : incompressible<br>

●  Multiphase Model : Off<br>

● Species Model : Not Include<br>

## 2) 격자
격자는 주어진 OpenFOAM의 polyMesh 폴더를 활용한다. <br>
상단 탭에서 File - Load Mesh - OpenFOAM 순서대로 클릭하고 polyMesh 폴더를 선택한다. <br>

## 3) 계산 조건
### (1) General
본 예제에서는 Default로 설정한다.<br>

### (2) Models
난류 모델은 𝑘 − ε 모델을 사용하고 나머지는 Default를 사용한다. <br>

### (3) Materials
본 예제에서는 공기를 작동 유체로 사용한다.<br>
물성치는 Default값을 사용한다.<br>

### (4) Cell Zone Conditions
Cell Zone Conditions은 Default 조건을 사용한다.<br>

### (5) Boundary Conditions
아래와 같이 경계면 타입과 경계값을 설정한다.<br>

**※plane_master, plane_slave는 plane의 앞, 뒷면이므로 Coupled Boundary로 설정해줘야 한다.<br>**

***●  duct : Wall***<br>
```Velocity Condition : No Slip```<br>

***●  inlet : Velocity Inlet***<br>
```Velocity Specification Method : Magnitude, Normal to Boundary```<br>
```Profile Type : Constant```<br>
```Velocity Magnitude : 10 (m/s)```<br>
```Turbulent Intensity : 1 (%)```<br>
```Turbulent Viscosity Ratio : 10 (m)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.3.png"><br>
</p>

***●  outlet : Pressure Outlet***<br>
```Total Pressure : 0 (Pa)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.4.png"><br>
</p>

***●  plane_master : Porous Jump***<br>
```Coupled Boundary : plane_slave```<br>
```Darcy Coefficient : -100```<br>
```Inertial Coefficient : -5```<br>
```Porous Media Thickness : 0.05```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.5.png"><br>
</p>

### (6) Numerical Conditions
Numerical Conditions은 다음과 같이 설정한다.<br>

●  Pressure-Velocity Coupling Scheme : SIMPLE<br>

●  Discretization Schemes<br>
```Momentum : Second Order Upwind```<br>
```Turbulence : First Order Upwind```<br>

●  Convergence Criteria<br>
```Pressure : 1e-6```<br>
```Momentum : 0.001```<br>
```Turbulence : 0.001```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.6.1.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.6.2.png"><br>
</p>

### (7) Initialization
●  X-Velocity : 10 (m/s)<br>

●  Pressure : 0 (Pa)<br>

●  Turbulence
```Scale of Velocity : 10 (m/s)```<br>
```Turbulent Intensity : 1 (%)```<br>
```Turbulent Viscosity Ratio : 10```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.7.png"><br>
</p>

### (8) Run
Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.<br>

●  Number of Iterations : 1000  <br>

●  Save Interval : 100  <br>

●  Data Write Format : Binary  <br>

●  Number of Cores : 1  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.8.png"><br>
</p>

계산이 완료된 모습

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.9.png"><br>
</p>

## 4) 후처리

### (1) 압력 분포
덕트 내부 압력 분포를 확인한다.<br>
paraview 아이콘을 클릭하여 paraview를 실행한다.<br>

Case Type을 Reconstructed Case로 변경한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.10.png"><br>
</p>

상단 툴바의 Slice 아이콘을 선택하고 Z Normal 버튼을 클릭한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.11.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.12.png"><br>
</p>

이후, 상단의 Solid Color를 p_rgh로 변경하여 덕트 내부 압력 분포를 확인한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.13.png"><br>
</p>