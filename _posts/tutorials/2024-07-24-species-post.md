---
layout: post
title: 17. Species transport
category: tutorials
---

# Species transport 

### * [격자 파일 다운로드](https://drive.google.com/file/d/19BS3wUfZZeh8A8Mqx2B1gSMwbylE-xXS/view?usp=sharing)

### * [계산 파일 다운로드](https://drive.google.com/file/d/1VihUsXB47k3qHfJOZ6Lgm4THC3v6jsRw/view?usp=sharing)

|[![화학종분포](https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/intro1.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/intro1.png){:target="_blank"}|

본 예제는 비정상상태 화학종 혼압 해석 예제이다. 두 개의 입구가 있는 2차원 덕트의 위쪽 입구에는 공기, 아래쪽 입구에는 수증기가 유입된다.

계산 조건은 다음과 같다. 

+ solver : buoyantSimpleNFoam 
+ 난류 모델 : $Standard$ $k-\epsilon$ model
+ 입구 유동 속도 : 0.5 $m/s$

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None을 선택한다.


## 3. 격자

격자는 주어진 polyMesh 폴더를 활용한다. 상단 탭에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/mesh1.png"><br>
</p>

## 4. General

Time은 Transient로  설정한다.

Gravity는 (0 -9.81 0)으로 설정한다.


## 5. Models

Species를 더블 클릭하고 Include를 선택한다.

## 6. Materials

Materials 패널 오른쪽 상단의 (+)를 클릭하여 mixture를 추가한다. 아래 그림의 왼쪽과 같이 air와 waterVapor를 선택하고 'Create Mixture'를 클릭하면 오른쪽과 같이 mixture가 만들어진다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/material.png"><br>
</p>


## 7. Cell Zone Conditions

Cell Zone Conditions의 region0를 더블 클릭해서 Material을 mixture로 바꾼다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/cellzone.png"><br>
</p>

## 8. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ in-up : Velocity Inlet
    + Velocity Specification Method : Magnitudde, Normal to Boundary
    + Velocity Magnitude : 0.5 (m/s)
    + Turbulent Intensity : 0.1 (%)
    + Turbulent Viscosity Ratio : 1
    + mixture - air : 1
    + mixture - waterVapor : 0

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/inletBC1.png"><br>
</p>

+ in-down : Velocity Inlet
    + Velocity Specification Method : Magnitudde, Normal to Boundary
    + Velocity Magnitude : 0.5 (m/s)
    + Turbulent Intensity : 0.1 (%)
    + Turbulent Viscosity Ratio : 1
    + mixture - air : 0
    + mixture - waterVapor : 1
    + Temperature : 300
    
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/inletBC2.png"><br>
</p>


+ out : Pressure Outlet
  + Total Pressure : 0 (Pa)

+ down_surface, up : wall
  + noSlip

+ zMin, zMax : empty


## 9. Numerical Conditions

본 예제에서는 아래와 같이 설정을 변경한다.

+ Pressure-Velocity Coupling Scheme : SIMPLE

+ Discretization Scheme
    + Time : Second Order Implicit
    + Pressure : Linear
    + Momentum : Second Order Upwind
    + Turbulence : Second Order Upwind
    + Species : Second Order Upwind

+ Under-Relaxation Factors
    + Pressure : 0.3
    + Momentum : 0.7
    + Turbulence : 0.7
    + Species : 1

+ Convergence Criteria : 디폴트 값 사용

+ Max Iterations per Time Step : 100

+ Number of Correctors : 2

## 10. Initialization

다음과 같이 설정한다.

+ Velocity : (0.5 0 0)
+ Pressure : 0
+ Scale of Velocity : 0.5
+ Turbulent intensity : 0.1
+ Turbulent viscosity ratio : 1
+ mixture - air : 1
+ mixture - waterVapor : 0

하단의 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/init1.png"><br>
</p>

## 11. Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Time Stepping Method : Fixed
+ Time Step Size : 0.001
+ End Time : 10
+ Save Interval : 0.1

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fan/runCondition1.png"><br>
</p>


## 12. 후처리

External tools의 paraivew 버튼을 클릭하여 paraview를 실행한다.

Coloring을 waterVapor로 바꾸면 다음과 같이 결과를 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/pv2.png"><br>
</p>
