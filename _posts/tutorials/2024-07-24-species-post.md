---
layout: post
title: 17. Species transport
category: tutorials
---

# Species transport 

### * [격자 다운로드](https://drive.google.com/file/d/1sDcHeUHm-75ncU0OFG4O7xQHAxy2Vufj/view?usp=sharing)

|[![화학종분포](https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/intro.png "화학종분포 (중) Sct=0.7,(하) Sct=0.1")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/intro.png){:target="_blank"}|

본 예제는 정상상태 화학종 혼압 해석 예제이다. OpenFOAM 튜토리얼에 있는 pitzDaily 격자를 이용하여 산소와 질소가 평행하게 유입될때 화학종의 분포를 확인하는 문제이다. 위의 그림에서 가운데 그림은 turbulent Schmidt number가 0.7인 경우의 결과이며 아래 그림은 0.1인 경우의 결과이다.

계산 조건은 다음과 같다. 

+ solver : buoyantSimpleNFoam 
+ 난류 모델 : $Standard$ $k-\epsilon$ model
+ 밀도 : perfectGas
+ 입구 유동 속도 : 1 $m/s$

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None을 선택한다.


## 3. 격자

격자는 주어진 polyMesh 폴더를 활용한다. 상단 탭에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/mesh.png"><br>
</p>

## 4. General

모두 디폴트 조건을 사용한다.


## 5. Models

Energy를 더블 클릭하고 Include를 선택한다.

Species를 더블 클릭하고 Include를 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/models.png"><br>
</p>

## 6. Materials

Materials 패널 오른쪽 상단의 (+)를 클릭하여 mixture를 추가한다. 아래 그림의 가운데와 같이 oxygen과 nitrogen을 선택하고 'Create Mixture'를 클릭하면 오른쪽과 같이 mixture가 만들어진다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/material-maxture.png"><br>
</p>

Mixture의 편집 버튼을 누르고 Density Spec.을 'Perfect Gas'로 바꾸어 준다. 그러면 nitrogen과 oxygen의 Density도 Perfect Gas로 바뀐다.


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/mixture-prop.png"><br>
</p>

Mixture 내부 nitrogen의 편집 버튼을 누르고 Name을 nitrogen에서 N2로 바꾼다.

Mixture 내부 oxygen의 편집 버튼을 누르고 Name을 oxygen에서 O2로 바꾼다.


## 7. Cell Zone Conditions

Cell Zone Conditions의 region0를 더블 클릭해서 Material을 mixture로 바꾼다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/cellzone.png"><br>
</p>

## 8. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ inlet : Velocity Inlet
    + Velocity Specification Method : Magnitudde, Normal to Boundary
    + Profile Type : Constant
    + Velocity Magnitude : 1 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10
    + mixture - O2 : 1
    + mixture - N2 : 0
    + Temperature : 300

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/inletBC.png"><br>
</p>

+ inlet : Velocity Inlet
    + Velocity Specification Method : Magnitudde, Normal to Boundary
    + Profile Type : Constant
    + Velocity Magnitude : 1 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10
    + mixture - O2 : 0
    + mixture - N2 : 1
    + Temperature : 300

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/verticalBC.png"><br>
</p>


+ outlet : Pressure Outlet
  + Total Pressure : 0 (Pa)

+ upperWall, lowerWall : wall
  + noSlip, adiabatic

+ frontAndBack : empty


## 9. Numerical Conditions

본 예제에서는 아래와 같이 설정을 변경한다.

+ Pressure-Velocity Coupling Scheme : SIMPLE

+ Discretization Scheme
    + Pressure : Linear
    + Momentum : Second Order Upwind
    + Turbulence : Second Order Upwind
    + Energy : Second Order Upwind
    + Species : Second Order Upwind

+ Under-Relaxation Factors
    + Pressure : 0.3
    + Momentum : 0.7
    + Turbulence : 0.7
    + Energy : 1
    + Species : 1

+ Convergence Criteria
    + Pressure : 0.0001
    + Momentum : 0.001
    + Turbulence : 0.001
    + Energy : 0.000001
    + Species : 0.001



## 10. Initialization

다음과 같이 설정한다.

+ Velocity : (1 0 0)
+ Pressure : 0
+ Temperature : 300
+ Scale of Velocity : 1
+ Turbulent intensity : 1
+ Turbulent viscosity ratio : 10
+ mixture - O2 : 1
+ mixture - N2 : 0

하단의 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/init.png"><br>
</p>

## 11. Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Number of Iterations : 1000
+ Save Interval : 100
+ Retain Only the Most Recent Files : 1
+ Data Write Format : Binary

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fan/runCondition.png"><br>
</p>

아래 그림은 계산이 종료된 상태의 Residuals 그래프이다.

|[![residual](https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/run.png "residual")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/run.png){:target="_blank"}|


## 12. 후처리

External tools의 paraivew 버튼을 클릭하여 paraview를 실행한다.

Coloring을 O2로 바꾸면 다음과 같이 결과를 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/species/pv1.png"><br>
</p>
