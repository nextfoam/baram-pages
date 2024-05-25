---
layout: post
title: 23. High Speed Turbulent Cavity Flow - DES Simulation Transonic Compressible Flow
category: tutorials
---

# High Speed Turbulent Cavity Flow  

<!--### * [격자 파일 다운로드](https://drive.google.com/file/d/1eL9zqfmXct3zMtJIJUuoap27afeMkdq2/view?usp=sharing) -->

## 1. 개요 

|[![include surface's own gap](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/intro.png "include surface's own gap")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/intro.png){:target="_blank"}|


DES 냔류 모델을 이용하여 마하수 0.85의 cavity 유동을 계산하는 예제이다. 아래 논문의 형상과 조건을 사용한다. Validation을 위한 계산은 아니며 튜토리얼의 특성상 성긴 격자를 이용하여 계산 방법을 보여주고자 한다.

  _Numerical Simulation of High-Speed Turbulent Cavity Flows, G.N.Barakos, S.J.Lawson, R.Steijil, P.Nayyar, Flow Turbulence Combust, 2009_

격자는 baramMesh 튜토리얼 중 3D Cavity에서 만들어진 백만개 정도의 격자를 사용한다.

솔버는 넥스트폼이 개발한 압력기반 열유동 해석 솔버인 buoyantPimpleNFoam을 사용한다.

출구와 측면의 경계조건은 압력파의 반사가 없는 waveTransmissive(non-reflecting) 조건을 사용한다.

계산 조건은 다음과 같다. 

+ solver : buoyantPimpleNFoam (넥스트폼이 개발한 비정상상태 열유동 해석 솔버)
+ 난류 모델 : DES 모델
+ 밀도 : Perfect Gas
+ 점성 계수 : 1.79e-5 $kg/ms$
+ 유동 조건 : 295.11 $m/s$

## 2. 프로그램의 구동 및 격자

프로그램 실행 후 launcher에서 'Open Case'를 선택하고 baramMesh에서 export한 폴더를 선택한다. 'Solver Type'은 Pressure-based, 'Multiphase Model'은 None', 'Species'는 Not Include를 선택한다.

|[![include surface's own gap](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/mesh.png "include surface's own gap")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/mesh.png){:target="_blank"}|

## 3. General

본 예제에서는 Transient 조건을 사용하고 Operating Pressure를 0으로 주고 절대압력을 사용한다. 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/trcavity/general.png"><br>
</p>

## 4. Models

난류 모델은 IDDES 모델을 사용하고 RANS 모델은 Spalart-Allmaras를 사용한다.

Energy를 include한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/tur.png"><br>
</p>

## 5. Materials

물성치는 다음과 같이 설정한다.

+ Density : Perfect Gas
+ Specific heat : 1006
+ Viscosity : 1.79e-05
+ Thermal Conductivity : 0.0245
+ Molecular Weight : 28.966

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/mat.png"><br>
</p>

## 6. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ forward : Velocity Inlet
    + Velocity Specification Method : Magnitude, Normal to Boundary
    + Velocity Magnitude : 295.11
    + Turbulence Specification Method : Modified Turbulent Viscosity
    + Modified Turbulent Viscosity : 0.05
    + Temperature : 300

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/inletbc.png">
</p>

+ back, left, right, up : Pressure Outlet
    + Total Pressure  : 101325
    + Non-Reflecting Boundary 옵션 사용

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/outletbc.png">
</p>

+ down : Wall
  + Velocity Condition : Slip

+ wall : Wall
  + Velocity Condition : No Slip


## 7. Numerical Conditions

다음과 같이 설정한다.

+ Pressure-Velocity Coupling : SIMPLE

+ Discretization Schemes
  + Time : First Order Implicit
  + Pressure : Linear
  + Momentum, Energy, Turbulence :Second Order Wpwind

+ Max Iteration per Time Step : 2

+ Number of Correctors : 1

+ Advanced - Limits
  + Minimum Static Temperature : 100
  + Maximum Static Temperature : 500


## 9. Monitoring

본 예제에서는 cavity 바닥면의 한 점에서의 압력을 모니터링한다. Add - Surface를 선택한다. 

좌표는 (2.286 1.2446 -0.1016)을 입력하고 Snap onto Boundary에 wall을 선택한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/monitor.png"><br>
</p>

## 10. Initialization

초기조건은 다음과 같이 설정한다.

+ Velocity : (295.11 0 0)
+ Pressure : 101325
+ Temperature : 300
+ Scale of velocity : 295.11  
+ Turbulent Viscosity Ratio : 10

Cavity 내부의 속도를 0으로 초기화한다. Advanced - Sections에서 Create - Hex 를 선택하고 최소/최대 좌표를 (1.8 1.16 -0.1016), (2.32 1.28 0)을 입력한다. Velcity를 선택하고 값은 (0 0 0)을 준다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/setField.png"><br>
</p>

Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다.

## 11. Run Conditions & RUN

병렬연산을 위해서는 메뉴의 Parallel을 실행하고 원하는 CPU 코어 개수를 입력한다.

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Time Stepping Method : Fixed
+ Time Step Size : 5e-6
+ End Time : 0.1
+ Save Interval : Every 0.0001 sec
+ Retain Only the Most Recent Files : 200

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/run.png"><br>
</p>


## 12. 후처리

External tools의 paraivew 버튼을 클릭하여 실행한다.

Case Type을 Decomposed Case로 변경한다.

단면의 속도 분포를 그리기 위해 Slice 를 선택하고 Mesh Regions에서 train_surface_0, ground, symmetry를 선택하고 Y Normal을 선택한다. Coloring을 p_rgh로 선택한다.

Coloring을 U로 선택한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/contour.png"><br>
</p>

