---
layout: post
title: 20. Cavitation of NACA66 hydrofoil
category: tutorials
---

# Caviation of NACA66 hydrofoil

### * [격자 파일 다운로드](https://drive.google.com/file/d/1a6uUi1CKbzZEYa9e4R3-ABR8ZY6LOtKq/view?usp=sharing)

### * [계산 파일 다운로드](https://drive.google.com/file/d/1iaVyUwowI6nrSYlnIkcniAcM3aiDFBXu/view?usp=sharing)

## 1. 개요 

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/cav-contour.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/cav-contour.png){:target="_blank"}|

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/cav-Cp.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/cav-Cp.png){:target="_blank"}|

NACA66 익형 주위의 캐비테이션 해석 검증 문제입니다.

캐비테이션 문제 검증용으로 많이 사용되는 아래 논문의 형상 및 조건을 사용하였습니다.

Viscous and Nuclei Effects on Hydrodynamic Loadings and Cavitation of NACA66(MOD) Foil section, Y.T.Shen, P.E. Dimotakis, J. Fluids Eng. sep. 1989

속도는 2.01 m/s 이며, 캐비테이션 수는 0.84 입니다.

캐비테이션 모델은 Schnerr-Sauer를 사용하였으며 계수들은 다음과 같습니다.

* Evaporation Coefficient : 1
* Condensation Coefficient : 1
* Bubble Diameter : 2e-6
* Bubble Number Density : 1.6e+9
* Vapor pressure : 2420 Pa

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 'New Case'를 선택하고 메뉴의 File - Load Mesh - OpenFOAM에서 다운로드 받은 polyMesh 폴더를 선택한다.

'Solver Type'은 Pressure-based, 'Multiphase Model'은 Volume of Fluid', Gravity는 (0 0 0)으로 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/launcher.png"><br> launcher 설정
</p>
<br>

## 3. General

Time 을 Transient로 변경하고 나머지는 디폴트를 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/general.png"><br> General 설정
</p>

## 4. Models

디폴트 난류 모델인 $standard$ $k-\epsilon$ 을 사용한다.

## 5. Materials

본 예제는 이상유동이므로 두 개의 유체가 필요하다. Material Configuration 부분의 상단 오른쪽의 (+)를 누르면 유체를 추가할 수 있다. waterLiquid와 waterVapor를 추가한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/material.png"><br> Materials 설정
</p>

## 6. Cell Zone Conditions

Cell Zone Conditions에는 region0가 있다.(multi-region일 때는 여러개의 region이 표시된다.) region의 유체를 설정한다. region0를 더블 클릭하면 설정창이 열린다. Primary Material은 waterVapor, Secondary material은 waterLiquid로 지정한다. Surface Tension은 0.07을 사용한다.

Cavitation 옵션을 켠다. Model은 Schnerr-Sauer를 선택하고 Vaporization Pressure는 2430을 입력한다. Model Constants 는 다음의 값을 사용한다.

* Evaporation Coefficient : 1
* Condensation Coefficient : 1
* Bubble Diameter : 2.0e-06
* Bubble Number Density : 1.6e+9

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/region.png"><br> Cell Zone Conditions 설정
</p>

## 7. Boundary Conditions

경계조건은 다음과 같이 설정한다.

+ B\_INLET
    + type : Velocity Inlet
    + Velocity Magnitude : 2.01
    + Turbulent Intensity : 1
    + Turbulent Viscosity Ratio : 10
    + Volume Fraction(water) : 1
  
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/inlet.png"><br> water-in 경계조건
</p>

+ B\_OUTLET
    + type : Pressure Outlet
    + Pressure : 4113.788
  
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/outlet.png"><br> water-in 경계조건
</p>

+ B\_SYM
    + type : Symmetry
  
+ FOIL\_DOWN, FOIL\_UP
    + type : Wall
  
+ EMPTY
    + type : Empty


## 8. Numerical Conditions

수치해석 조건은 다음과 같이 설정한다.

+ Pressure-Velocity Coupling Scheme : SIMPLE(디폴트)

+ Use Momentum Predictor : On(디폴트)

+ Discretization Schemes
    + Time : First Order Implicit
    + Pressure : Momentum Weighted Reconstruct
    + Momentum : Second Order Upwind
    + Turbulence : First Order Upwind
    + Volume Fraction : Second Order Upwind

+ Under-Relaxation Factors : 디폴트 값 사용

+ Improve Stability : Off(디폴트)

+ Max Iteration per Time Step : 10

+ Number of Correctors : 2

+ Multiphase와 Convergence Criteria : 디폴트 사용
  
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/numerical.png"><br> Numerical Conditions
</p>

## 9. Initialization

초기조건은 다음과 같이 입력한다.

+ velocity : (2.01 0 0)
+ Pressure : 4113.788
+ Scale of Velocity : 2.01
+ Turbulent Intensity : 1
+ Turbulent Viscosity Ratio : 10
+ Volume Fraction(water) : 1

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/initial.png"><br> 초기조건 설정
</p>

하단의 Initialize 버튼을 클릭한 후, File - Save 버튼을 클릭하여 설정을 저장한다.


## 10. Run Conditions & Run

Run Conditions 에서 다음과 같이 설정 후 계산을 진행한다.

+ Time Stepping Method : Fixed
+ Time Step Size : 0.01
+ End time : 10
+ Save Interval : 0.5

병렬연산을 위해서는 메뉴의 Parallel을 실행하고 원하는 CPU 코어 개수를 입력한다.

'Start Calculation' 버튼을 눌러 계산을 시작한다.

## 11. 후처리

External tools의 paraview 버튼을 클릭하여 paraview를 실행한다.

병렬로 계산했다면 Case Type을 Decomposed Case로 변경한다.

Coloring을 p_rgh 혹은 alpha.waterLiquid를 선택하면 압력과 체적분율을 확인할 수 있다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/cav-contour.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavitation/cav-contour.png){:target="_blank"}|

하이드로포일 표면의 압력데이터를 얻으려면 원하는 경계면(FOIL\-UP)만 선택하고, 메뉴의 File-Save Data를 실행하면 csv 형식의 데이터 파일을 얻을 수 있다.




