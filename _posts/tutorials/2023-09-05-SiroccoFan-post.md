---
layout: post
title: 06. Sirocco Fan - Sliding mesh
category: tutorials
---

# Sirocco Fan 

### * [격자 파일 다운로드](https://drive.google.com/file/d/1479KBQebn3GnVG_X5KlY9JBejJn4dX3Q/view?usp=sharing)

### * [계산 파일 다운로드](https://drive.google.com/file/d/1n7kY5ZSO4I9PsH1TVDLI0nTRLrl8lRhh/view?usp=sharing)

## 1. 개요 

|[![격자 및 압력분포](https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/intro.png "격자 및 압력분포")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/intro.png){:target="_blank"}|

본 예제는 비정상상태 비압축성 유동해석 예제이다. 시로코팬 내부에서 입펠러가 회전할 때 내부의 유동을 예측하는 문제이다.

MRF 방법을 사용해서 정상상태 해석을 하고, 이 결과를 초기조건으로 sliding mesh 방법으로 비정상상태 계산을 한다.

계산 조건은 다음과 같다. 

+ solver : buoyantPimpleNFoam (넥스트폼이 개발한 동적격자 비압축성 유동 해석 솔버)
+ 난류 모델 : $Standard$ $k-\epsilon$ model
+ 밀도 : 1.225 $kg/m^3$
+ 점성 계수 : 1.79e-5 $kg/ms$
+ 임펠러 회전 수 : 2,000 RPM

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None을 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/launcher.png"><br>
</p>

## 3. 격자

격자는 fluent 격자를 변환하여 사용한다. 

메뉴에서 File-Load Mesh-Fluent(ASCII)를 선택하면 파일 선택창이 열린다. 다운로드한 siroccofan.msh 파일을 선택하면 아래와 같은 창이 열린다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/fluentToFoam.png"><br>
</p>

이 격자는 2개의 fluid와 rotating이라는 두 개의 cell zone을 갖고 있다. 이 두개의 cell zone과 region1, region2라는 두 개의 region이 표시되어 있다. region2 오른쪽의 (+) 아이콘을 누르면 region이 추가된다. multi-region 격자로 변환하기 위한 옵션이다. 이 문제는 multi-region 문제가 아니기 때문에 두 cel zone 모두 region1으로 두면 된다. region2 아래의 휴지통 아이콘을 눌러 region2를 삭제해도 된다. 

## 4. 정상상태 계산

### General

Time은 Steady, Gravity는 (0 0 ), Operating Conditions는 101325를 사용한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/general-steady.png"><br>
</p>

### Models

난류 모델은 $Standard$ $k-\epsilon$ 모델을 사용하고 나머지는 Default를 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.3.png"><br>
</p>

### Materials

본 예제에서 작동 유체는 공기이다. 유체의 물성치는 Default 조건을 사용한다.

### Cell Zone Conditions

Cell Zone Conditions에서 rotating을 더블 클릭하면 새로운 창이 열린다. 'MUltiple Reference Frame, MRF'를 선택하고 아래 값들을 입력한다.

+ Rotating Speed : 2,000(RPM)
+ Rotation-Axis Origin : (0, 0, 0)
+ Rotation-Axis Direction : (0, 0, 1)
+ Static Boundary : interface-rotating, interface-stat
    + MRF를 사용할 cell zone에 있는 경계면들 중 회전하지 않는 면들을 선택해 준다. 두 개의 interface 면들 중 하나는 해당 cell zone에 있고 나머지는 바깥에 있다. 보통은 어느 것이 해당되는지 알기 어렵기 때문에 두 개를 모두 선택하면 된다. 해당 cell zone 밖에 있는 경계면이 포함되어도 문제되지 않는다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/mrf.png"><br>
</p>

### Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ interface-stat, interface-rotating : Interface - Internal Interface
    + interface-stat : Internal Interface로 변경 후, Coupled Boundary는 interface-rotating 선택

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.5.png"><br>
</p>

+ axis : Wall
    + Velocity Condition : Rotational Moving Wall
    + Speed : 2000 (RPM)
    + Rotation-Axis Origin : 0 0 0
    + Rotation-Axis Direction : 0 0 1

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.6.png"><br>
</p>

+ axis-r, blades, externalwalls, walls : Wall
    + Velocity Condition : No Slip

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.8.png"><br>
</p>

+ inlet : Velocity Inlet
    + Velocity Specification Method : Magnitudde, Normal to Boundary
    + Profile Type : Constant
    + Velocity Magnitude : 1 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.9.png"><br>
</p>

+ outlet : Pressure Outlet
    + Total Pressure : 0 (Pa)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.10.png"><br>
</p>

### Numerical Conditions

디폴트 조건을 사용한다.

### Initialization

모두 디폴트 값을 사용한다.

하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/initial.png"><br>
</p>

### Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Number of Iteration : 1000
+ Save Interval : 100
+ 메뉴의 Parallel - Environment를 선택하고 원하는 코어수를 입력

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/run.png"><br>
</p>

유동이 비정상상태이기 때문에 residual이 수렴하지는 않지만, 비정상상태 계산을 위한 초기조건으로는 사용하기에 문제는 없다.

## 3. 비정상상태 계산

### General

Time을 Transient로 바꾼다. 다음과 같은 창이 나타난다. 정상상태 계산 결과를 비정상상태 계산의 초기조건으로 사용할 것인지를 묻는다. Yes를 선택하면 마지막으로 저장된 데이터가 초기조건으로 설정되고, 시간 0부터 계산이 시작된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/toTransient.png"><br>
</p>

### Cell Zone Conditions

'rotating' cell zone의 조건을 Sliding Mesh로 바꾼다. Static Boundary 설정 부분은 사라진다.

### Boundary Conditions

움직이는 벽면에 대한 경계조건을 다음과 같이 바꾸어 준다.

+ axis-r, blades : Wall
    + Velocity Condition : Moving Wall

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.7.png"><br>
</p>

### Numerical Conditions

디폴트 조건을 사용한다.

### Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Time Stepping Method : Fixed
+ Time Step Size : 0.0001
+ End Time : 0.3

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.12.png"><br>
</p>

아래 그림은 계산중인 Residuals 그래프이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.13.png"><br>
</p>

## 4. 후처리

Fan 내부의 압력 분포를 확인해본다. External tools의 paraivew 버튼을 클릭하여 paraview를 실행한다.

Case Type을 Decomposed Case로 변경한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.14.png"><br>
</p>

Slice 기능을 활용하여 용기 내부의 단면을 자른다.

Z-normal 버튼을 클릭 후, Origin을 다음과 같이 변경한다.

+ Origin : 0.06 -0.017 0.05
+ Normal : 0 0 1

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.15.png"><br>
</p>

아래 그림과 같이 fan 내부 속도 분포가 나오게 된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.16.png"><br>
</p>
