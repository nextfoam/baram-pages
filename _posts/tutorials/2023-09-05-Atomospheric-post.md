---
layout: post
title: 06. Atmosphere Boundary Conditions
category: tutorials
---

# Atmosphere Boundary Conditions 
 
### * [격자 파일 다운로드](https://drive.google.com/file/d/19kMYRiWaB84kaUzCoobMRZBKCc_uKxVU/view?usp=drive_link)

## 1. 개요 

|[![격자, 고도에 따른 $U$, $k$, $\epsilon$ 분포](https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.1.png "격자, 고도에 따른 $U$, $k$, $\epsilon$ 분포")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.1.png){:target="_blank"}|


본 예제는 대기 경계층 유동해석 예제이다. 해석 영역은 600m X 50m X 600m이며 대기경계층 조건으로 주어진 입구의 유동 분포가 출구까지 유지되는지를 확인한다.

격자는 주어진 OpenFOAM 격자를 사용한다

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

난류 모델은 $Standard$ $k-\epsilon$ 모델을 사용하고 나머지는 Default를 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.4.png"><br>
</p>

## 6. Materials

본 예제에서는 공기를 작동 유체로 사용한다. 물성치는 Default값을 사용한다.

## 7. Cell Zone Conditions

Cell Zone Conditions은 Default 조건을 사용한다.

## 8. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ inlet : ABL Inlet
  + Flow Direction : 1 0 0
  + Ground-Normal Direction : 0 0 1
  + Reference Flow Speed : 7 (m/s)
  + Reference Height : 9 (m)
  + Surface Roughness Length : 0.0002 (m)
  + Minimum z-coordinate : 0.0 (m)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.5.png"><br>
</p>

+ Sea : Wall
  + Velocity Condition : Atmospheric Wall

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.6.png"><br>
</p>

+ outlet : Pressure Outlet
  + Total Pressure : 0 (Pa)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.7.png"><br>
</p>

+ minY, maxY, sky : Symmetry

## 9. Numerical Conditions

Numerical Conditions은 다음과 같이 설정한다.

+ Pressure-Velocity Coupling Scheme : SIMPLE

+ Discretization Schemes
  + Pressure : Momentum Weighted Reconstruct
  + Momentum : Second Order Upwind
  + Turbulence : First Order Upwind

+ Convergence Criteria : 1e-6 (모든 값)

나머지는 Default 조건을 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.8.1.png"><br>
</p>


## 10. Initialization

+ X-Velocity : 7 (m/s)
+ Pressure : 0 (Pa)
+ Turbulence
  + Scale of Velocity : 7 (m/s)
  + Turbulent Intensity : 1 (%)
  + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.9.png"><br>
</p>

위 과정을 따라 초기화 후, File - save를 눌러 저장한다.

## 11. Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Number of Iterations : 1000
+ Save Interval : 100
+ Data Write Format : Binary


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.10.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/residual.png"><br>residual plot
</p>

## 12. 후처리

대기경계층 속도 분포와 Profile을 확인한다. External tools의 paraview 버튼을 눌러 Paraview를 실행한다.

Case Type을 Reconstructed Case로 변경한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.12.png"><br>
</p>

상단 툴바의 Solid Color를 U로 변경한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.13.png"><br>
</p>

상단 툴바에서 Slice 아이콘을 클릭하고 아래와 같이 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ABL/8.16.png"><br>
</p>


상단 툴바의 Plot Over Line 아이콘을 클릭하고 아래와 같이 입구와 출구에 각각 Line을 1개 생성한다.

입구, 출구의 라인을 이용하여 속도 프로파일이 그대로 유지되는지 정량적으로 확인한다.

1번 라인 (입구)

+ Point1 : 0 25 0
+ Point2 : 0 25 600
+ X Array Name : U_X
+ Series Parameters : Points_Z

2번 라인 (출구)

+ Point1 : 600 25 0
+ Point2 : 600 25 600
+ X Array Name : U_X
+ Series Parameters : Points_Z

Series Parameters에서 해당 Parameter의 색을 변경할 수 있다.

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
