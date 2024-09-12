---
layout: post
title: 01. Mixing Pipe - Incompressible Internal Flow
category: tutorials
---

# Mixing Pipe 

### * [격자 파일 다운로드](https://drive.google.com/file/d/12CyYZO_FSl7Baz-MmbtXnBst02EGg5Tg/view?usp=sharing)

## 1. 개요 

|[![격자 및 속도분포](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.1.png "격자 및 속도분포")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.1.png){:target="_blank"}|


본 예제는 정상상태 비압축성 유동해석 예제이다. 2개의 입구와 1개의 출구로 이루어진 원형 파이프 내부 유동의 혼합을 예측한다.

계산 조건은 다음과 같다. 

+ solver : buoyantSimpleNFoam (넥스트폼이 개발한 정상상태 비압축성 해석 솔버)
+ 난류 모델 : Standard $k-\epsilon$ model
+ 밀도 : 1.225 $kg/m^3$
+ 점성 계수 : 1.79e-5 $kg/ms$
+ 유동 조건 : 면적이 넓은 입구(in-1)의 속도는 5m/s, 면적이 좁은 입구(in-2)의 속도는 10m/s, outlet은 대기압 조건

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None을 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/launcher.png"><br>
</p>

## 3. 격자

격자는 주어진 polyMesh 폴더를 활용한다. 상단 탭에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.2.png"><br>
</p>

_※ 주의 사항 : OpenFOAM 격자를 읽을 때는 "polyMesh" 혹은 "constant" 폴더를 선택한다. OpenFOAM의 격자는 region이 하나인 경우 constant 폴더 아래의 polyMesh라는 폴더이며, region이 여러 개인 multi-region일 때는 여러 개의 polyMesh 폴더가 constant 폴더 아래의 region명 폴더에 있다._


## 4. General

General에서는 Time, Gravity, Operating Pressure등을 설정할 수 있다. 본 예제에서는 Default로 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.3.png"><br>
</p>

## 5. Models

Models에서는 turbulence, Energy, Species, User-defined Scalar를 설정할 수 있다. Multiphase, Solver type 등은 launcher에서 설정한다.

본 예제에서는 Standard $k-\epsilon$ 모델을 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.4.png"><br>
</p>

## 6. Materials

Materials에서는 작동 유체의 물성치를 설정할 수 있다. 지금 예제에서는 공기의 물성치를 그대로 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.5.png"><br>
</p>

## 7. Cell Zone Conditions

Cell Zone Conditions에서는 Source, MRF, Sliding Mesh등을 설정할 수 있다. 본 예제에서는 Default로 설정한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.6.png"><br>
</p>

## 8. Boundary Conditions

여러 경계면의 경계값을 설정할 수 있다. 각 경계면을 선택하면 해당 경계면이 붉은색으로 변한다. 

경계면을 마우스 오른쪽 버튼으로 클릭하면 경계면 타입을 변경할 수 있고, 더블 클릭하거나 아래의 'Edit' 버튼을 누르면 값을 설정할 수 있는 창이 열린다.

각 경계조건은 다음과 같이 설정한다.

+ in-1 : Velocity Inlet
    + Velocity Magnitude : 5 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10
      
+ in-2 : Velocity Inlet
    + Velocity Magnitude : 10 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10
      
+ out : Pressure Outlet
    + Total Pressure : 0 (Pa)
      
+ wall
    + Velocity Condition : No Slip

## 9. Numerical Conditions

Discretization, Relaxation factors, Convergence criteria, Pressure-Velocity coupling등 항목을 설정할 수 있다.

본 예제에서는 아래와 같이 설정을 변경한다.

+ Pressure-Velocity Coupling Scheme : SIMPLEC

+ Discretization Scheme
    + Pressure : Momentum Weighted Reconstruct
    + Momentum : Second Order Upwind
    + Turbulence : Second Order Upwind

+ Under-Relaxation Factors
    + Pressure, Momentum, Turbulence : 0.9

+ Convergence Criteria
    + Pressure : 0.0001
    + Momentum : 0.001
    + Turbulence : 0.001

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.7.1.png"><br>
</p>


## 10. Monitoring

본 예제에서는 (0, 0, 1) 위치에서 압력을 모니터링 한다.

Solution - Monitors를 선택하고 창 하단의 Add - Points를 클릭해서 아래 그림과 같이 설정한다.

+ Point Monitor
    + Write Interval : 1
    + Field : Pressure
    + Coordinate : (0, 0, 1) (m)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.8.png"><br>
</p>

## 11. Initialization

Initial Condition은 초기값으로 x, y, z의 속도와 압력을 입력할 수 있다.

난류 모델을 사용할 경우 Velocity Scale, Turbulent Intensity, Viscosity Ratio 값을 입력하면 $k$와 $\epsilon$ 값이 계산되어 사용된다. 

+ Velocity
    + X-Velocity : 0 (m/s)
    + Y-Velocity : 0 (m/s)
    + Z-Velocity : 0 (m/s)

+ Pressure
    + 0 (Pa)

+ Turbulence
    + Scale of Velocity : 5 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.9.png"><br>
</p>

값을 입력하고 하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다.

## 12. Run

Run Conditions에서는 Number of Iterations, Save Interval, Parallel 등을 설정한다.

본 예제에서는 모든 값을 Default로 설정한다. 

이후, Run - Start Calculation 버튼을 클릭한다.

|[![residual & monitoring 그래프](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/residual.png "residual & monitoring 그래프")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/residual.png){:target="_blank"}|
<p align='center'>residual & monitoring 그래프</p>

## 13 후처리

BARAM에서는 ParaView를 이용하여 후처리를 진행한다. 후처리 진행 시, External tools의 ParaView 버튼을 클릭하면 된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.10.png"><br>
</p>

ParaView를 초기 실행 시, 필요한 기능에 대한 설명은 다음과 같다.

+ Skip Zero Time : 초기값을 제외한 결과를 보여준다.

+ Case Type : cpu 개수에 따른 설정이다.
    + Reconstructed Case : 1core 계산 혹은 Parallel로 계산을 진행했지만 reconstructPar를 진행한 OpenFOAM case
    + Decomposed Case : Parallel 계산을 진행한 case

+ Mesh Regions : 보고 싶은 Internal mesh, 경계면 등을 설정할 수 있다.

+ Cell Arrays : 보고 싶은 물리량을 설정할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.11.png"><br>
</p>

### 경계면 스칼라 분포

벽면에 걸리는 압력 분포를 그려본다. 초기 설정을 아래와 같이 해준다.

+ Skip Zero Time : 비활성화
+ Mesh Regions : internalMesh - 활성화
+ 나머지 : Default

p_rgh는 압력에서 중력에 의한 항($\rho gh$)을 뺀 값으로 이 문제와 같이 중력을 고려하지 않은 경우는 압력과 같은 값이다. p_rgh는 operating pressure 기준의 상대압이고 p는 절대압력이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.12.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.13.png"><br>
</p>


### 축단면 스칼라 분포

Pipe 내부의 압력 분포를 확인해본다.

slice 버튼을 클릭하고 방향을 Y-normal로 바꿔서 pipe 내부 압력을 확인한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.14.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.15.png"><br>
</p>
