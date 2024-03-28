---
layout: post
title: 06. Atmosphere Boundary Conditions
category: tutorials
---

# Atmosphere Boundary Conditions 
 
### * [격자 파일 다운로드](https://drive.google.com/file/d/19kMYRiWaB84kaUzCoobMRZBKCc_uKxVU/view?usp=drive_link)

## 1. 개요 

+  본 예제는 대기 경계층 유동해석 예제이다.
+  해석 영역은 600m X 50m X 600m이다.
+  대기경계층 조건으로 주어진 입구의 속도 분포가 출구까지 유지되는지를 확인한다.
+  격자는 주어진 OpenFOAM 격자를 사용한다
+  아래 그림에서 형상과 격자를 나타내었다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.1.png"><br>
</p>

계산 조건은 다음과 같다. 

+ solver : buoyantSimpleNFoam (넥스트폼이 개발한 비압축성 유동 해석 솔버)
+ 난류 모델 : standard 𝑘 − ε model
+ 밀도 : 1.225 𝑘𝑔/㎥
+ 점성 계수 : 1.79e-5 𝑘𝑔/𝑚s
+ 유동 조건 : 대기경계층 속도 및 난류 조건

대기 경계층 조건은 OpenFOAM이 제공하는 조건으로 D.M. Hargreaves and N.G. Wright의 다음 논문의 식을 이용한다.

*"On the use of the k-epsilon model in commercial CFD software to model the neutral atmospheric boundary layer"*

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.2.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.3.png"><br>
</p>

BARAM을 실행하면 아래 과정을 따라서 case 파일을 만든다.

+ New Case버튼 클릭
+ Project Name : ABL
+ Flow Type : incompressible
+ Multiphase Model : Off
+ Species Model : Not Include

## 2. 격자

격자는 주어진 OpenFOAM의 polyMesh 폴더를 활용한다. <br>
상단 탭에서 File - Load Mesh - OpenFOAM 순서대로 클릭하고 polyMesh 폴더를 선택한다. <br>

## 3. General

본 예제에서는 Default로 설정한다.<br>

## 4. Models

난류 모델은 Standard 𝑘 − ε 모델을 사용하고 나머지는 Default를 사용한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.4.png"><br>
</p>

## 5. Materials

본 예제에서는 공기를 작동 유체로 사용한다.<br>
물성치는 Default값을 사용한다.<br>

## 6. Cell Zone Conditions

Cell Zone Conditions은 Default 조건을 사용한다.<br>

## 7. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.<br>

***●  inlet : ABL Inlet***<br>
```Flow Direction : 1 0 0```<br>
```Ground-Normal Direction : 0 0 1```<br>
```Reference Flow Speed : 7 (m/s)```<br>
```Reference Height : 9 (m)```<br>
```Surface Roughness Length : 0.0002 (m)```<br>
```Minimum z-coordinate : 0.0 (m)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.5.png"><br>
</p>

***●  Sea : Wall***<br>
```Velocity Condition : Atmospheric Wall```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.6.png"><br>
</p>

***●  outlet : Pressure Outlet***<br>
```Total Pressure : 0 (Pa)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.7.png"><br>
</p>

***●  minY, maxY, sky : Symmetry***<br>

## 8. Numerical Conditions

Numerical Conditions은 다음과 같이 설정한다.

+ Pressure-Velocity Coupling Scheme : SIMPLE
+ Discretization Schemes
  + Momentum : Second Order Upwind
  + Turbulence : First Order Upwind
+ Convergence Criteria : 1e-6 (모든 값)
+ 나머지는 Default 조건을 사용한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.8.1.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.8.2.png"><br>
</p>

## 9. Initialization

+ X-Velocity : 7 (m/s)
+ Pressure : 0 (Pa)
+ Turbulence
  + Scale of Velocity : 7 (m/s)
  + Turbulent Intensity : 1 (%)
  + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.9.png"><br>
</p>

위 과정을 따라 초기화 후, File - save를 눌러 저장한다.<br>

## 10. Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Number of Iterations : 1000
+ Save Interval : 100
+ Data Write Format : Binary
+ Number of Cores : 1  

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.10.png"><br>
</p>

계산이 완료된 모습

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.11.png"><br>
</p>

## 11. 후처리

대기경계층 속도 분포와 Profile을 확인한다.<br>
External tools의 paraview 버튼을 눌러 Paraview를 실행한다.<br>

Case Type을 Reconstructed Case로 변경한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.12.png"><br>
</p>

상단 툴바의 Solid Color를 U로 변경한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.13.png"><br>
</p>

상단 툴바에서 Slice 아이콘을 클릭하고 아래와 같이 설정한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.16.png"><br>
</p>


상단 툴바의 Plot Over Line 아이콘을 클릭하고 아래와 같이 입구와 출구에 각각 Line을 1개 생성한다.<br>
입구, 출구의 라인을 이용하여 속도 프로파일이 그대로 유지되는지 정량적으로 확인한다.<br>

1번 라인 (입구)<br>

●  Point1 : 0 25 0<br>

●  Point2 : 0 25 600<br>

●  X Array Name : U_X<br>

●  Series Parameters : Points_Z<br>

2번 라인 (출구)<br>

●  Point1 : 600 25 0<br>

●  Point2 : 600 25 600<br>

●  X Array Name : U_X<br>

●  Series Parameters : Points_Z<br>

Series Parameters에서 해당 Parameter의 색을 변경할 수 있다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.14.1.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.14.2.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.14.3.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.14.4.png"><br>
</p>

아래 그림과 같이 높이에 따른 속도 크기 분포를 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.15.png"><br>
</p>

위 그림에서 빨간선이 입구영역, 초록선이 출구영역에서 속도 프로파일이다.
