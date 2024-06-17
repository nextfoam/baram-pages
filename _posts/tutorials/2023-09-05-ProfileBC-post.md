---
layout: post
title: 10. Time dependent Boundary Condition
category: tutorials
---

# Time dependen Boundary Condition

### * [격자 파일 다운로드](https://drive.google.com/file/d/1pzp6DXomC0cyaxn0xzlpcneShrEkRW68/view?usp=sharing)

## 1. 개요

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.1.png"><br>
</p>

본 예제는 시간에 따라 입구의 속도와 온도가 변하는 경계조건을 설정하는 예제이다.

OpenFOAM 튜토리얼에 있는 pitzDaily 격자를 사용한다.

계산 조건은 다음과 같다. 

+ solver : buoyantPimpleNFoam (넥스트폼이 개발한 비압축성 유동 해석자)
+ 난류 모델 : $Standard$ $k-\epsilon$
+ 밀도 : Perfect Gas (Ideal Gas)
+ 점성 계수 : 1.79e-5 $kg/ms$

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None, ‘Species’는 Not Include를 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/launcher.png"><br>
</p>


## 3. 격자

격자는 주어진 OpenFOAM의 polyMesh 폴더를 활용한다. 상단 탭에서 File - Load Mesh - OpenFOAM 순서대로 클릭한다. 

## 4. General

Time advance는 Transient로 바꿔준다. 나머지는 Default를 사용한다.

## 5. Models

난류 모델은 $Standard$ $k-\epsilon$ 모델을 사용하고 Energy는 Include로 바꿔준다.

## 6. Materials

본 예제에서는 공기를 작동 유체로 사용한다. 유체의 이름과 물성치를 아래와 같이 변경한다. 

+ Density : Perfect Gas (m/s)
+ Specific Heat (Cp) : 1004 $J/kgK$ (m/s)
+ Viscosity : 1.79e-05 $kg/ms$
+ Thermal Conductivity : 0.0245 $W/mK$

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/Perfect Gas.png"><br>
</p>

## 7. Cell Zone Conditions

Cell Zone Conditions은 Default 조건을 사용한다.

## 8. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ inlet : Velocity Inlet
    + Velocity Specification Method : Magnitude, Normal to Boundary
    + Velocity Profile Type : Temporal Distribution
        + piecewise linear : (0, 1) (0.1 2) (0.2 1.5)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10
    + Temperature Profile Type : Temporal Distribution
        + piecewise linear : (0, 300) (0.1 400) (0.2 350)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.3.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.4.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.5.png"><br>
</p>

+ outlet : Pressure Outlet
    + Total Pressure : 0 (Pa)

+ upperWall, lowerWall : Wall
    + Velocity Condition : No Slip
    + Temperature : Adiabatic

+ frontAndBack : empty

## 9. Numerical Conditions

Numerical Conditions은 Default 조건을 사용한다.

## 10.  Monitors

Monitors를 클릭하면 세부설정상자가 나온다. 입구에서 유량과 온도 변화를 모니터링 한다. 

하단의 Add - Surfaces 를 누르면 Surface Monitor 창이 나온다. 아래 그림과 같이 설정을 변경한다.

+ Surface Monitor 1
    + Report Type : Mass Flow Rate
    + Surface : inlet

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.6.png"><br>
</p>

+ Surface Monitor 2
    + Report Type : Area-Weighted Average
    + Field Variable : Temperature
    + Surface : inlet

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.7.png"><br>
</p>

## 11. Initialization

Initial Contion은 초기값으로 x, y, z의 속도와 압력을 입력할 수 있다.

난류 모델을 사용할 경우 Velocity Scale, Turbulent Intensity, Viscosity Ratio 값을 입력하면 k와 ε 값이 계산되어 사용된다.

+ Velocity
    + X-Velocity : 0 (m/s)
    + Y-Velocity : 0 (m/s)
    + Z-Velocity : 0 (m/s)

+ Pressure
    + 0 (Pa)

+ Temperature : 300 (K)

+ Turbulence
    + Scale of Velocity : 1 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.8.png"><br>
</p>

값을 입력하고 하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다.

## 12. Run Conditions

Run Conditions에서는 Number of Iterations, Save Interval, Parallel 등을 설정한다. 

+ Run Conditions
    + Time Step Size : 0.001
    + End Time : 1
    + Set Interval (Every) : 0.1

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.9.png"><br>
    그림 11.9
</p>

이후, Run - Start Calculation 버튼을 클릭한다.

하단의 Residuals 탭을 클릭하면 아래와 같이 그래프를 확인할 수 있다.

Monitor 탭을 클릭하면 입구의 온도와 유량의 변화를 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.10.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.11.png"><br>
</p>

## 13. 후처리

시간에 따른 온도 및 속도의 분포를 확인한다. External tools의 paraview 버튼을 눌러 paraview를 실행한다.

상단의 Solid Color를 T로 변경한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.12.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.13.png"><br>
</p>

이후, Set Range를 눌러 온도 범위를 340 - 350K으로 조정한다.

그리고 상단의 Play 버튼을 눌러 시간에 따른 온도 변화를 확인한다.

아래 그림은 최종 순간에서 온도분포를 나타내는 그림이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.14.png"><br>
</p>
