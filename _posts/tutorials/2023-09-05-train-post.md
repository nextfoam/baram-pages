---
layout: post
title: 14. High Speed Train
category: tutorials
---


# 고속열차 공력해석 

## 1) 개요 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/train/intro.png"><br>
</p>

고속열차는 마하수가 0.3~0.4 범위의 아음속 압축성 유동 영역에서 주행한다. CFD에서 저속 유동에서는 SIMPLE 게열의 압력기반 솔버를, 고속유동에서는 밀도기반의 솔버를 많이 사용한다. Baram의 비압축성 솔버인 buoyantSimpleNFoam의 아음속 압축성 유동영역에서 솔버의 안정성을 검증하기 위한 에제이다.

차량 연결부, 대차(바퀴), 판토그라프를 단순화한 고속철도 모델을 사용하였으며, 열차의 속도는 400 km/h이다. 

약 200만개 정도의 격자로 300번 정도의 iteration만에(8 코어 CPU에서 20분 정도에) 수렴된 결과를 얻을 수 있었다. OpenFOAM의 표준솔버인 buoyantSimpleFoam과 rhoSimpleFoam을 사용하여 해석한 결과와 비교했을 때 훨씬 뛰어난 수렴성을 보여준다.

계산 조건은 다음과 같다. <br>

●  solver : buoyantSimpleNFoam (넥스트폼이 개발한 정상상태 비압축성 해석 솔버)

●  난류 모델 : SST $k - \omega$ 모델

●  밀도 : Perfect Gas

●  점성 계수 : 1.79e-5 𝑘𝑔/𝑚s

●  유동 조건 : 400 km/h(111.11 m/s)

## 2) 프로그램의 구동 및 격자

프로그램 실행 후 launcher에서 ‘Open’을 선택하고 격자 생성 튜토리얼에서 만든 train 폴더를 선택한다. launcher에서 Incompressible, Multiphase off, Species off를 선택한다. 혹은 New Case를 선택하고 메뉴의 File - Load Mesh - OpenFOAM에서 train/case/constant 폴더를 선택한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/mesh.png"><br>
</p>

## 3) 계산 조건

### (1) General

본 예제에서는 Default 조건인 Steady로 설정한다.

### (2) Models

난류 모델은 SST $k - \omega$ 모델을 사용하고 나머지는 Default를 사용한다.

Energy를 include한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/tur.png"><br>
</p>

### (3) Materials

물성치는 다음과 같이 설정한다.

+ Density : Perfect Gas

+ Specific heat : 1006

+ Viscosity : 1.79e-05

+ Thermal Conductivity : 0.0245

+ Molecular Weight : 28.966

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/mat.png"><br>
</p>

### (4) Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ inlet : Velocity Inlet

  * Velocity

    * Specification Method : Magnitude, Normal to Boundary

    * Velocity Magnitude : 111.11

  * Turbulence

    * Specification Method : Intensity and Viscosity Ratio

    * Turbulent Intensity : 1

    * Viscosity ratio : 100

  * Temperature : 300

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/inletbc.png">
</p>

+ outlet : Pressure Outlet

  * Total Pressure  : 0

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/outletbc.png">
</p>

+ ground : Wall

  * Velocity Condition : Translational Moving Wall

  * Velocity : (111.11 0 0)

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/groundbc.png">
</p>

+ train_surface_0 : Wall

+ side, top, symmetry : Symmetry

### (5) Reference Value

Reference Value은 공력계수를 계산할 때 사용된다. 이 문제는 실험 데이터가 있는 문제가 아니기 때문에 정확한 값을 입력할 필요는 없으며 속도를 111.11 로 설정한다.

### (6) Numerical Conditions

다음과 같이 설정한다.

+ Pressure-Velocity Coupling : SIMPLEC

+ Discretization Schemes : Momentum, Energy, Turbulence 모두 Second Order Wpwind

+ Under-Relaxation Factors

  * Pressure : 0.8

  * Momentum, Energy, Turbulence : 0.9

  * Density : 1.0

+ Convergence Criteria

  * Pressure, Momentum, Turbulence : 1e-4

  * Energy : 1e-6

### (7) Monitoring

본 예제에서는 차량의 공력 계수를 모니터링한다. Add - Forces를 선택한다. 모두 디폴트 설정을 사용하고 Boundaries에 train_surface_0를 선택한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/monitor.png"><br>
</p>

### (8) Initialization

초기조건은 다음과 같이 설정한다.

+ Velocity : (111.11 0 0)

+ Pressure : 0

+ Scale of velocity : 111.11
  
+ Turbulent Intensity : 1

+ Turbulent Viscosity Ratio : 10

+ Temperature : 300

값을 입력하고 하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다.

### (9) Run Conditions & RUN

병렬연산을 위해서는 메뉴의 Parallel을 실행하고 원하는 CPU 코어 개수를 입력한다.

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Number of Iterations : 1000

+ Save Interval : 100

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/run.png"><br>
</p>

계산이 완료되면 아래와 같이 Residuals과 Force monitor의 그래프가 나타난다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/residual.png"><br>
</p>

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/force.png"><br>
</p>

## 4) 후처리

### (1) 경계면 스칼라 분포

External tools의 paraivew 버튼을 클릭하여 실행한다.

Case Type을 Decomposed Case로 변경한다.

차량 주변 압력 분포를 그리기 위해 Mesh Regions에서 train_surface_0, ground, symmetry를 선택하고 Coloring을 p_rgh로 선택한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/contour.png"><br>
</p>

