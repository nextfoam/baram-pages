---
layout: post
title: 23. High Speed Turbulent Cavity Flow - DES Simulation Transonic Compressible Flow
category: tutorials
---

# High Speed Turbulent Cavity Flow  

### * [격자 파일 다운로드](https://drive.google.com/file/d/1u__XyUIi_xiL5-LmuT9OaBNda7s7qpDk/view?usp=sharing)

## 1. 개요 

|[![include surface's own gap](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/2d-pressureContour.png "include surface's own gap")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/2d-pressure.avi){:target="_blank"}|


아음속 2차원 cavity 유동을 계산하는 예제이다. 

형상과 유동 조건은 다음과 같다.

+ L/D = 2 (Cavity의 길이와 높이의 비율)
+ Mach Number = 0.6
+ Reynolds Number = 2.75e+5
+ Prandtl Number = 0.7

격자는 matlab으로 만든 plot3d 형식의 격자를 변환하였다. 

솔버는 넥스트폼이 개발한 압력기반 열유동 해석 솔버인 buoyantPimpleNFoam을 사용한다.

출구와 상면의 경계조건은 압력파의 반사가 없는 waveTransmissive(non-reflecting) 조건을 사용한다.

계산 조건은 다음과 같다. 

+ solver : buoyantPimpleNFoam (넥스트폼이 개발한 비정상상태 열유동 해석 솔버)
+ 난류 모델 : $SST$ $k-\omega$ 모델
+ 밀도 : Perfect Gas
+ 입구 온도 : 300 K
+ 입구 압력 : 101325 Pa

## 2. 프로그램의 구동 및 격자

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None을 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/launcher.png"><br>
</p>

격자는 주어진 polyMesh 폴더를 활용한다. 상단 탭에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다. 

|[![include surface's own gap](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/2d-mesh.png "include surface's own gap")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/2d-mesh.png){:target="_blank"}|

## 3. General

본 예제에서는 Transient 조건을 사용한다. 중력은 고려하지 않고 Operating Pressure는 101325를 사용한다. 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/2d-general.png"><br>
</p>

## 4. Models

난류 모델은 $SST$ $k-\omega$ 모델을 사용한다.

Energy를 include한다.


## 5. Materials

물성치는 다음과 같이 설정한다.

+ Density : Perfect Gas
+ Specific heat : 1006
+ Viscosity : 0.00178 (Reynolds 수를 맞추기 위한 값)
+ Thermal Conductivity : 2.562 (Prandtl 수를 맞추기 위한 값)
+ Molecular Weight : 28.966

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/2d-material.png"><br>
</p>

## 6. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ inlet : Velocity Inlet
    + Velocity Specification Method : Magnitude, Normal to Boundary
    + Velocity Magnitude : 208.31
    + Turbulence Specification Method : Intensity and Viscosity Ratio
    + Turbulent Intensity : 1
    + Turbulent Viscosity Ratio : 10
    + Temperature : 300

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/2d-inletbc.png">
</p>

+ outlet, top : Pressure Outlet
    + Total Pressure  : 0
    + Non-Reflecting Boundary 옵션 사용

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/2d-outletbc.png">
</p>

+ cavityFront, cavityBottom, cavityRear, frontBottom, rearBottom : Wall
  + Velocity Condition : No Slip

+ frontPlane, backPlane : Empty


## 7. Numerical Conditions

다음과 같이 설정한다.

+ Pressure-Velocity Coupling : SIMPLE

+ Discretization Schemes
  + Time : Second Order Implicit
  + Pressure : Momentum Weighted Reconstruct
  + Momentum, Energy, Turbulence : Second Order Wpwind

+ Max Iteration per Time Step : 20

+ Number of Correctors : 2

+ Under-Relaxation Factors
  + Pressure : 0.3 / 1
  + Momentum, Turbulence : 0.7 / 1
  + Energy, Density : 1 / 1


## 9. Monitoring

본 예제에서는 cavity 중앙의 점에서 압력을 모니터링한다. Add - Point를 선택한다. 

좌표는 (0 -0.5 0.25)를 입력한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/2d-monitor.png"><br>
</p>

## 10. Initialization

초기조건은 다음과 같이 설정한다.

+ Velocity : (208.31 0 0)
+ Pressure : 0
+ Temperature : 300
+ Scale of velocity : 208.31  
+ Turbulent Intensity : 1
+ Turbulent Viscosity Ratio : 10

Cavity 내부의 속도를 0으로 초기화한다. Advanced - Sections에서 Create - Hex 를 선택하고 최소/최대 좌표를 (-1 -1 -1), (1 0 1)을 입력한다. Velcity를 선택하고 값은 (0 0 0)을 준다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/2d-setField.png"><br>
</p>

Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다.

## 11. Run Conditions & RUN

병렬연산을 위해서는 메뉴의 Parallel을 실행하고 원하는 CPU 코어 개수를 입력한다.

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Time Stepping Method : Fixed
+ Time Step Size : 1e-5
+ End Time : 0.5
+ Save Interval : Every 0.002 sec

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/2d-run.png"><br>
</p>


## 12. 후처리

External tools의 paraivew 버튼을 클릭하여 실행한다.

Coloring을 U로 선택하면 다음과 같은 그림을 확인할 수 있다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cavity/2d-contour.png"><br>
</p>

