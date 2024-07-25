---
layout: post
title: 07. Vortex shedding of 2d cylinder
category: tutorials
---

# Vortex shedding of 2d cylinder 

### * [격자 파일 다운로드](https://drive.google.com/file/d/1KwU6-RFIv__nr8ovKGfNDX7g9ewrBJTy/view?usp=sharing)

## 1. 개요 

|[![격자 및 속도분포](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.1.png "격자 및 속도분포")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.1.png){:target="_blank"}|


본 예제는 2차원 비정상상태 층류 유동해석 예제로, 레이놀즈 수 100인 2차원 실린더 주변의 와류 진동(vortex shedding) 문제이다.

OpenFOAM에서 2차원 문제의 격자는 높이 방향으로 하나의 격자를 갖는 3차원 격자를 사용한다. 이 때 높이 방향의 최대 최소면의 경계조건은 empty로 처리한다.

격자는 Ansys Fluent .msh 형식의 파일을 사용한다. OpenFOAM의 격자 변환 유틸리티로 Fluent의 msh 파일을 변환하면 z축으로 한 증의 격자를 갖는 3차원 격자가 만들어진다.

계산 조건은 다음과 같다. 

+ solver : buoyantPimpleNFoam (넥스트폼이 개발한 비압축성 유동 해석 솔버)
+ 난류 모델 : laminar
+ Reynolds No. : 100

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None을 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/launcher.png"><br>
</p>

## 3. 격자

격자는 주어진 Ansys의 .msh 파일을 활용한다. 상단 탭에서 File - Load Mesh - Fluent (ASCII)를 클릭하고 cylinder.msh 파일을 선택한다. 

## 4. General

Time을 Transient로 변경한다. 나머지는 Default로 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.2.png"><br>
</p>

## 5. Models

난류 모델은 Laminar 모델을 사용하고 나머지는 Default를 사용한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.3.png"><br>
</p>

## 6. Materials

본 예제에서는 $U$ = 1 $m/s$ 조건을 사용한다. 이 때 레이놀즈 수가 100이 되는 조건으로 물성치를 설정한다.

+ 밀도 : 1 $kg/m^3$
+ 점성 계수 : 0.01 $kg/ms$ 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.4.png"><br>
</p>

## 7. Cell Zone Conditions

Cell Zone Conditions은 Default 조건을 사용한다.

## 8. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ cylinder : Wall
    + Velocity Condition : No Slip

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.5.png"><br>
</p>

+ sym : Symmetry

+ out : Pressure Outlet
    + Total Pressure : 0 (Pa)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.6.png"><br>
</p>

+ in : Velocity Inlet
    + Velocity Specification Method : Magnitudde, Normal to Boundary
    + Profile Type : Constant
    + Velocity Magnitude : 1 (m/s)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.7.png"><br>
</p>

+ frontAndBackPlanes : Empty

## 9. Reference Values

본 예제에서는 cylinder의 Drag Coefficient와 Lift Coefficient를 확인한다. 이를 위해 Reference Values를 아래와 같이 설정한다.

+ Area : 1
+ Density : 1
+ Length : 1
+ Pressure : 0
+ Velocity : 1 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.8.png"><br>
</p>

## 10. Numerical Conditions

Numerical Conditions은 다음과 같이 설정한다.

+ Use Momentum Predictor : 활성화

+ Discretization Schemes
    + Time : Second Order Implicit
    + Pressure : Momentum Weighted Reconstruct
    + Momentum : Second Order Upwind

+ Max iterations per Time Step : 10
+ Number of Correctors : 2

나머지는 Default 조건을 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.9.png"><br>
</p>

## 11. Monitoring

본 예제에서는 cylinder에 작용하는 Drag/Lift Coefficient와 cylinder중심에서 1m 떨어진 지점의 속도/압력을 모니터링 한다.

__cylinder에 작용하는 Drag/Lift Coefficient__

+ Add - Forces 버튼을 선택한다.
+ Force Monitoring은 아래와 같이 설정한다.
    + Write Interval : 1
    + Lift Direction : 0 1 0
    + Drag Direction : 1 0 0
    + Center of Rotation : 0 0 0
    + Boundaries : cylinder

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.10.1.png"><br>
</p>

__cylinder중심에서 1m 떨어진 지점의 속도, 압력__

+ Add - Points 버튼을 선택한다.
+ Point Monitoring은 아래와 같이 설정한다.
    + Write Interval : 1
    + Field : Pressure
    + Coordinate : 1 0 0

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.10.2.png"><br>
</p>

같은 방식으로 동일한 지점의 Velocity Magnitude 모니터링도 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.10.3.png"><br>
</p>

## 12. Initialization

X-Velocity에 1을 입력하고 나머지 값들은 Default값을 사용한다. 

하단에 Initialize 버튼을 클릭한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.11.png"><br>
</p>

## 13. Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Time Stepping Method : Adaptive
+ Max Courant Number : 1
+ End Time : 150
+ Save Interval : 0.5
+ Data Write Format : Binary
+ Number of Cores : 4 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.12.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.18.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.19.png"><br>
</p>


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.13.1.png"><br>계산이 완료된 Residuals
</p>


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cylinder/5.13.2.png"><br>모니터링되는 항력계수, 양력계수, 속도, 압력 그래프
</p>

## 14. 후처리

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
