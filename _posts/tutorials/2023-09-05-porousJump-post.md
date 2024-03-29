---
layout: post
title: 07. Porous Jump
category: tutorials
---

# Porous Jump 

### * [격자 파일 다운로드](https://drive.google.com/file/d/1c7RgueGF8kfG_pqA0tGbU_TbPpZ99tNG/view?usp=sharing)

## 1. 개요 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.1.png"><br>
</p>

본 예제는 계산영역 내부에 있는  다공성 판이나 fan을 두께가 없는 경계면으로 모사할 수 있는 Porous Jump 경계조건 예제이다. 육면체 덕트 내부에 사각형의 면을 만들고 Porous Jump 경계조건을 사용하여 압력과 속도가 변하는 문제이다.

격자는 주어진 OpenFOAM 격자를 사용한다.

계산 조건은 다음과 같다.

+ solver : buoyantsimpleNFoam (넥스트폼이 개발한 비압축성 유동 해석 솔버)
+ 난류 모델 : $Realizable$ $k-\epsilon$ model
+ 밀도 : 1.225 $kg/m^3$
+ 점성 계수 : 1.79e-5 $kg/ms$
+ Porous 경계 조건
    + Darcy Coefficient : -100
    + Inertial Coefficient : -5
    + porous media in the flow direction : 0.05 m

Porous Jump를 계산하는 porousBafflePressure 경계조건은 아래 식을 사용한다.

<p align='left'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.2.png"><br>
</p>

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None, ‘Species’는 Not Include를 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/launcher.png"><br>
</p>

## 3. 격자

격자는 주어진 OpenFOAM의 polyMesh 폴더를 활용한다. 상단 탭에서 File - Load Mesh - OpenFOAM 순서대로 클릭하고 polyMesh 폴더를 선택한다. 

## 4. General

본 예제에서는 Default로 설정한다.

## 5. Models

난류 모델은 𝑘 − ε 모델을 사용하고 나머지는 Default를 사용한다. 

## 6. Materials

본 예제에서는 공기를 작동 유체로 사용한다. 물성치는 Default값을 사용한다.

## 7. Cell Zone Conditions

Cell Zone Conditions은 Default 조건을 사용한다.

## 8. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

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

## 9. Numerical Conditions

Numerical Conditions은 다음과 같이 설정한다.

+ Pressure-Velocity Coupling Scheme : SIMPLE

+ Discretization Schemes
    + Momentum : Second Order Upwind
    + Turbulence : First Order Upwind

+ Convergence Criteria
    + Pressure : 1e-6
    + Momentum : 0.001
    + Turbulence : 0.001

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.6.1.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.6.2.png"><br>
</p>

## 10. Initialization

+ X-Velocity : 10 (m/s)
+ Pressure : 0 (Pa)
+ Turbulence
    + Scale of Velocity : 10 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.7.png"><br>
</p>

## 11. Run

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

## 12. 후처리

덕트 내부 압력 분포를 확인한다. External tools의 paraview 버튼을 클릭하여 paraview를 실행한다.

Case Type을 Reconstructed Case로 변경한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousJump/9.10.png"><br>
</p>

상단 툴바의 Slice 아이콘을 선택하고 Z Normal 버튼을 클릭한다.

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
