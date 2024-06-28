---
layout: post
title: 13. Propeller - Sliding mesh
category: tutorials
---

# Propeller 

## 1. 개요 

|[![속도분포](https://github.com/nextfoam/baram-pages/raw/main/screenshots/propeller/intro.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/propeller/intro.png){:target="_blank"}|

본 예제는 OpenFOAM의 pimpleFoam tutorial에 있는 propeller 문제를 BaramFlow로 계산하는 예제이다. Sliding mesh 기법을 사용하여 프로펠러의 회전에 따른 유동을 예측하는 문제이다.

계산 조건은 다음과 같다. 

+ solver : buoyantPimpleNFoam (넥스트폼이 개발한 비압축성 유동 해석 솔버)
+ 난류 모델 : $Realizable$ $k-\epsilon$ model
+ 밀도 : 1000 $kg/m^3$
+ 점성 계수 : 0.001 $kg/ms$
+ 프로펠러 회전 수 : 1432 RPM
+ 입구 속도 : 5 m/s

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None, ‘Species’는 Not Include를 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/launcher.png"><br>
</p>

## 3. 격자

격자는 [baramMesh Propeller 튜토리얼](https://baramcfd.org/mesh/2024/06/17/propellerMesh-post/)에서 만든 격자를 사용한다.

메뉴에서 File - Load Mesh - OpenFOAM을 클릭하고 constant 혹은 polyMesh 폴더를 선택한다. 

## 4. General

Time을 Transient로 변경한다. 나머지는 Default로 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.2.png"><br>
</p>

## 5. Models

난류 모델은 $Realizable$ $k-\epsilon$ 모델을 사용하고 Near-Wall Treatment는 Enhanced Wall Treatment를 선택한다. 나머지는 Default를 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/propeller/tur.png"><br>
</p>

## 6. Materials

Name을 water로 변경하고 Density는 1000, viscosity는 0.001을 입력한다.

## 7. Cell Zone Conditions

Cell Zone Conditions에서는 MRF, Sliding Mesh, Source 등을 설정할 수 있다. 본 예제에서는 'cellZone'에 Sliding Mesh 조건을 설정한다.

Sliding Mesh를 선택하고 아래 값들을 입력한다.

+ Sliding Mesh
    + Rotating Speed : 1432(RPM)
    + Rotation-Axis Origin : (0 0 0)
    + Rotation-Axis Direction : (-1 0 0)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/propeller/cellZone.png"><br>
</p>

## 8. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ cellZone_surface, cellZone_surface_slave : Interface - Internal Interface
    + cellZone_surface : Internal Interface로 변경 후, Coupled Boundary는 cellZone_surface_slave 선택

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/propeller/interface.png"><br>
</p>

+ propeller, stem : Wall
    + Velocity Condition : Moving Wall

+ wall : Wall
    + Velocity Condition : Slip

+ inlet : Velocity Inlet
    + Velocity Specification Method : Magnitudde, Normal to Boundary
    + Profile Type : Constant
    + Velocity Magnitude : 5 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/propeller/inlet.png"><br>
</p>

+ outlet : Pressure Outlet
    + Total Pressure : 0 (Pa)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/propeller/outlet.png"><br>
</p>

## 9. Numerical Conditions

Max Iterations per Time Step을 20, Number of Correctors를 2로 설정한다. 나머지는 Default 조건을 사용한다.

## 10. Initialization

X-Velocity는 5, Scale of Velocity는 5, 나머지는 Defalut 값을 사용한다.

하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다. 

## 11. Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Time Stepping Method : Fixed
+ Time Step Size : 1e-5
+ End Time : 0.1
+ Save Interval : 0.001
+ Data Write Format : Binary
+ 메뉴의 Parallel - Environment를 선택하고 Number of Cores는 8, Parallel Type은 Local Machine을 선택


