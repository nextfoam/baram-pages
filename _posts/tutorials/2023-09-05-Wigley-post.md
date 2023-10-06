---
layout: post
title: 11. Wigley Hull
category: tutorials
---

# Wigley Hull

* [격자 파일](https://drive.google.com/file/d/1kXbwOAFXs4Dn-U9USRq2yWB_7Ofk-hcf/view?usp=sharing)

## 1) 개요 
* 본 예제는 VOF(Volume of Fluid) 기법을 사용하여 선박 주위의 자유수면을 해석하는 예제이다.<br>

* 자유수면 계산을 위해 interNFoam 솔버를 사용하고, LTS(Local Time Step)기법을 사용하는 정상상태 계산이다.<br>

* 아래 그림에서 형상과 격자를 나타내었다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/wigley/22.1.png"><br>
</p>

계산 조건은 다음과 같다. <br>

●  solver : interFoam <br>

●  난류모델 : SST k-ω <br>

BARAM을 실행하면 아래 과정을 따라서 case 파일을 만든다.<br>

●  New Case버튼 클릭<br>

●  Project Name : Wigley<br>

●  Flow Type : incompressible<br>

●  Multiphase Model : Volume of Fluid<br>

●  Gravity : X: 0, Y: 0, Z: -9.81<br>

● Species Model : Not Include<br>

## 2) 격자


## 3) 계산 조건
### (1) General
Time은 Steady, Gravity는 (0 0 -9.81)로 설정한다.<br>
나머지는 Default로 설정한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/wigley/22.2.png"><br>
</p>

### (2) Models

난류 모델은 SST k-ω 모델을 사용한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/wigley/22.3.png"><br>
</p>

### (3) Materials

물성치는 다음과 같이 설정한다.<br>

***●  water***<br>
```Density : 10000```<br>
```Viscosity : 0.001```<br>


***●  air***<br>
```Density : 1.225```<br>
```Viscosity : 1.79e-5```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/wigley/22.4.png"><br>
</p>

### (4) Cell Zone Conditions
Cellzome에 2가지의 유체가 포함되어 있으므로 아래와 같이 Primary Material에 air, Secondary material은 water로 지정해준다.<br>
Surface Tension은 0으로 입력한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/wigley/22.5.png"><br>
</p>

### (5) Boundary Conditions
아래와 같이 경계면 타입과 경계값을 설정한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/wigley/22.6.png"><br>
</p>

***●  inlet : Velocity inlet***<br>
```Velocity magnitude : 1```<br>
```Turbulent Intensity : 1%```<br>
```Turbulent Viscosity Ratio : 10```<br>
```Volume Fraction (water) : 1```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/wigley/22.7.png"><br>
</p>

***●  outlet : Open Channel Outlet***<br>
```Mean Velocity (u<sub>∞</sub>) : 1```<br>
```Turbulent Intensity : 1%```<br>
```Turbulent Viscosity Ratio : 10```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/wigley/22.8.png"><br>
</p>

***●  atmosphere : pressure Outlet***<br>
```Total Pressure : 0```<br>

***●  bottom, midPlane, side : symmetry***<br>
```Total Pressure : 0```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/wigley/22.9.png"><br>
</p>

***●  hull : adiabaticWall***<br>

### (6) Numerical Conditions
Number of MULES iterations over the limiter를 제외한 모든 값은 전부 Default값로 설정한다.<br>
```Number of MULES iterations over the limiter : 10```

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/wigley/22.10.png"><br>
</p>

### (7) Monitoring
Add-Force 선택후, 관찰하고자 하는 영역은 hull으로 선택하여준다.<br>

```Lift Direction : 0 0 1```<br>
```Drag Direction : 1 0 0```<br>
```Boundaries : hull```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/wigley/22.11.png"><br>
</p>

### (8) Initialization

지정한 영역(Water) 외의 초기조건은 다음과 같이 입력한다.<br>

```velocity : (1 0 0)```<br>
```Pressure : 0```<br>
```Scale of Velocity : 1```<br>
```Turbulent Intensity : 1%```<br>
```Turbulent Viscosity Ratio : 10```<br>
```Volume Fraction - Liquid : 0```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/wigley/22.12.png"><br>
</p>

지정 영역(Water)의 초기조건을 주기위해 Initialization-Advanced-Section-Create 를 클릭한 후 Section Type : Hex 를 선택한다.<br>
생성할 영역의 초기조건들을 아래와 같이 입력한다.<br>

***●  region-1***<br>
```Min.point : (-100 -100 -100)```<br>
```Max.point : (100 100 0)```<br>
```Volume Fraction - Liquid : 1```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/wigley/22.13.png"><br>
</p>

하단의 Initialize 버튼을 클릭한 후, File - Save 버튼을 클릭하여 Case파일을 저장한다.<br>

### (9) Run

Run Conditions 에서 다음과 같이 설정 후 계산을 진행한다.<br>

```Number of iterations : 1000```<br>
```Number of Cores : 8```<br>