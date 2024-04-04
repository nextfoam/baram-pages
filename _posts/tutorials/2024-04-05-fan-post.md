---
layout: post
title: 04. Fan - Multiple Reference Frame
category: tutorials
---

# Fan 

### * [격자 파일 다운로드](https://drive.google.com/file/d/1bsWn_brltH32gsHBgw4J4cae8lVzQbJK/view?usp=sharing)

## 1. 개요 

|[![격자 및 속도분포](https://github.com/nextfoam/baram-pages/raw/main/screenshots/fan/intro.png "격자 및 압력분포")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/fan/intro.png){:target="_blank"}|

본 예제는 정상상태 비압축성 유동해석 예제이다. 단순한 형상의 팬 내부에서 입펠러가 회전할 MRF(Multiple Reference Frame)를 사용하여 유동을 예측하는 문제이다.

격자는 Ansys Fluent의 .msh 형식의 파일을 변환하여 사용한다.

계산 조건은 다음과 같다. 

+ solver : buoyantSimpleNFoam 
+ 난류 모델 : $Standard$ $k-\epsilon$ model
+ 밀도 : 1.225 $kg/m^3$
+ 점성 계수 : 1.79e-5 $kg/ms$
+ 임펠러 회전 수 : 1,000 RPM
+ 입구 유동 속도 : 10 $m/s$

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None, ‘Species’는 Not Include를 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/launcher.png"><br>
</p>

## 3. 격자

격자는 주어진 Ansys의 .msh 파일을 활용한다. 상단 탭에서 File - Load Mesh - Fluent (ASCII)를 클릭하고 fan.msh 파일을 선택한다. 

## 4. General

모두 디폴트 조건을 사용한다.


## 5. Models

모두 디폴트 조건을 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.3.png"><br>
</p>

## 6. Materials

본 예제에서 작동 유체는 공기이다. 유체의 물성치는 디폴트 조건을 사용한다.

## 7. Cell Zone Conditions

Cell Zone Conditions에서는 MRF, Sliding Mesh, Source 등을 설정할 수 있다. 본 예제에서는 'rotating' Cell Zone에 Multiple Reference Frame, MRF 조건을 사용한다.

Multiple Reference Frame, MRF를 선택하고 아래 값들을 입력한다.

+ Multiple Reference Frame, MRF
    + Rotating Speed : 1000(RPM)
    + Rotation-Axis Origin : (0 0 0)
    + Rotation-Axis Direction : (0 0 1)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fan/mrf.png"><br>
</p>

## 8. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ blade, casing
    + Velocity Condition : No Slip

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.8.png"><br>
</p>

+ inlet : Velocity Inlet
    + Velocity Specification Method : Magnitudde, Normal to Boundary
    + Profile Type : Constant
    + Velocity Magnitude : 10 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fan/inletBC.png"><br>
</p>

+ outlet : Pressure Outlet
    + Total Pressure : 0 (Pa)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.10.png"><br>
</p>

## 9. Numerical Conditions

본 예제에서는 아래와 같이 설정을 변경한다.

+ Pressure-Velocity Coupling Scheme : SIMPLEC

+ Discretization Scheme
    + Pressure : Linear
    + Momentum : Second Order Upwind
    + Turbulence : First Order Upwind

+ Under-Relaxation Factors
    + Pressure : 0.9
    + Momentum : 0.9
    + Turbulence : 0.9

+ Convergence Criteria
    + Pressure : 0
    + Momentum : 0.001
    + Turbulence : 0.001    + 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fan/nume.png"><br>
</p>

## 10. Initialization

모두 디폴트 값을 사용한다.

하단의 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.11.png"><br>
</p>

## 11. Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Number of Iterations : 5000
+ Save Interval : 100
+ Retain Only the Most Recent Files, 1
+ Data Write Format : Binary
+ 메뉴의 Parallel - Environment를 선택하고 Number of Cores는 8, Parallel Type은 Local Machine을 선택

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fan/runCondition.png"><br>
</p>

아래 그림은 계산이 종료된 상태의 Residuals 그래프이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fan/run.png"><br>
</p>

## 12. 후처리

Fan 내부의 압력 분포를 확인해본다. External tools의 paraivew 버튼을 클릭하여 paraview를 실행한다.

Case Type을 Decomposed Case로 변경한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fan/pv1.png"><br>
</p>

Slice 기능을 활용하여 용기 내부의 단면을 자른다.

Z-normal 버튼을 클릭 후, Origin의 z 값에 0.01을 입력한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fan/pv2.png"><br>
</p>

아래 그림과 같이 fan 내부 속도 분포가 나오게 된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fan/pv3.png"><br>
</p>
