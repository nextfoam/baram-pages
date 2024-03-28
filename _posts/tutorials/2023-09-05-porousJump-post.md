---
layout: post
title: 07. Porous Jump
category: tutorials
---

# Porous Jump 

### * [격자 파일 다운로드](https://drive.google.com/file/d/1c7RgueGF8kfG_pqA0tGbU_TbPpZ99tNG/view?usp=sharing)

## 1. 개요 

+ 본 예제는 계산영역 내부에 porous media 혹은 fan을 두께가 없는 경계면으로 모사할 수 있는 Porous Jump 경계조건 예제이다.
+ 육면체 덕트 내부에 사각형의 면을 만들고 Porous Jump 경계조건을 사용하여 압력이 증가되고 속도가 높아지는 문제이다.
+ 격자는 주어진 OpenFOAM 격자를 사용한다.

아래 그림에 형상과 격자를 나타내었다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.1.png"><br>
</p>

계산 조건은 다음과 같다.

+ solver : buoyantsimpleNFoam (넥스트폼이 개발한 비압축성 유동 해석 솔버)
+ 난류 모델 : standard 𝑘 − ε model
+ 밀도 : 1.225𝑘𝑔/㎥
+ 점성 계수 : 1.79e-5𝑘𝑔/𝑚s
+ Porous 경계 조건
    + Darcy Coefficient : -100
    + Inertial Coefficient : -5
    + porous media in the flow direction : 0.05 m

Porous Jump를 계산하는 porousBafflePressure 경계조건은 아래 식을 사용한다.

<p align='left'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.2.png"><br>
</p>

BARAM을 실행하면 아래 과정을 따라서 case 파일을 만든다.

+ New Case버튼 클릭
+ Project Name : porousJump
+ Flow Type : incompressible
+ Multiphase Model : Off
+ Species Model : Not Include

## 2. 격자

격자는 주어진 OpenFOAM의 polyMesh 폴더를 활용한다. <br>
상단 탭에서 File - Load Mesh - OpenFOAM 순서대로 클릭하고 polyMesh 폴더를 선택한다. <br>

## 3. General

본 예제에서는 Default로 설정한다.<br>

## 4. Models

난류 모델은 𝑘 − ε 모델을 사용하고 나머지는 Default를 사용한다. <br>

## 5. Materials

본 예제에서는 공기를 작동 유체로 사용한다.<br>
물성치는 Default값을 사용한다.<br>

## 6. Cell Zone Conditions

Cell Zone Conditions은 Default 조건을 사용한다.<br>

## 7. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

**※plane_master, plane_slave는 plane의 앞, 뒷면이므로 Coupled Boundary로 설정해줘야 한다.<br>**

+ duct : Wall
    + Velocity Condition : No Slip

+ inlet : Velocity Inlet
    + Velocity Specification Method : Magnitude, Normal to Boundary
    + Profile Type : Constant
    + Velocity Magnitude : 10 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10 (m)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.3.png"><br>
</p>

+ outlet : Pressure Outlet
    + Total Pressure : 0 (Pa)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.4.png"><br>
</p>

+ plane_master : Porous Jump
    + Coupled Boundary : plane_slave
    + Darcy Coefficient : -100
    + Inertial Coefficient : -5
    + Porous Media Thickness : 0.05

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.5.png"><br>
</p>

## 8. Numerical Conditions

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

## 9. Initialization

+ X-Velocity : 10 (m/s)
+ Pressure : 0 (Pa)
+ Turbulence
    + Scale of Velocity : 10 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.7.png"><br>
</p>

## 10. Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Number of Iterations : 1000
+ Save Interval : 100
+ Data Write Format : Binary
+ Number of Cores : 1 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.8.png"><br>
</p>


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.9.png"><br>계산이 완료된 모습

</p>

## 4) 후처리

### (1) 압력 분포
덕트 내부 압력 분포를 확인한다.<br>
External tools의 paraview 버튼을 클릭하여 paraview를 실행한다.<br>

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
