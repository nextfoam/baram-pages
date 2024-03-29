---
layout: post
title: 12. Cantilever Beam
category: tutorials
---
# Cantilever Beam 

### * [격자 파일 다운로드](https://drive.google.com/file/d/14Fl8OJUSvlWhayietAzy_dCwoqhMXoX9/view?usp=sharing)

## 1. 개요 

본 예제는 정상상태 비압축성 유동해석 예제이다. 입구 영역에서 유입되는 공기에 의해 외팔보가 (Cantilever Beam) 변형되는 정도를 확인하는 1way FSI (Fluid Structure Interaction) 예제이다.

외팔보는 두께 5mm, 길이 50mm, 높이 150mm이다. 절반만 모델링하여 Symmetry 경계 조건을 부여한다.

아래 그림에서 형상과 격자를 나타내었다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/1.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/2.png"><br>
</p>

계산 조건은 다음과 같다. 

+ solver : buoyantSimpleNFoam (넥스트폼이 개발한 정상상태 비압축성 해석 솔버)
+ 난류 모델 : $Standard$ $k-\epsilon$
+ 밀도 : 1.225 $kg/m^3$
+ 점성 계수 : 1.79e-5 $kg/ms$
+ 유동 조건 : inlet에서 80 $m/s$

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None, ‘Species’는 Not Include를 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/launcher.png"><br>
</p>

## 3. 격자

격자는 주어진 polyMesh 폴더를 활용한다. 상단 탭에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다.

## 4. General

본 예제에서는 Default로 설정한다.

## 5. Models

본 예제에서 사용하는 난류 모델은 Default인 $Standard$ $k-\epsilon$ 모델로 설정한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/3.png"><br>
</p>

## 6. Materials

본 예제에서는 공기의 물성치를 Default로 설정한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/4.png"><br>
</p>

## 7. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ Hex6_1_xMin : velocity Inlet
    + Velocity Specfication Method : Magnitude, Normal to Boundary
    + Profile Type : Constant
    + Velocity Magnitude : 80 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/5.png"><br>
</p>

+ Hex6_1_zMax : velocity Inlet
    + Velocity Specfication Method : Component
    + Profile Type : Constant
    + X-Velocity : 80 (m/s)
    + Y-Velocity : 0 (m/s)
    + Z-Velocity : 0 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/Hex6_1_zMax.png"><br>
</p>

+ Hex6_1_xMax : Pressure Outlet
    + Total Pressure : 0 (Pa)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/6.png"><br>
</p>

+ Hex6_1_yMin, Hex6_1_yMax : Symemtry

+ cantileverBeam_surface_0 : Wall
    + Velocity Condition : No Slip

## 8. Monitoring

본 예제에서는 Cantilever 전면에 걸리는 압력을 모니터링한다. Monitors - Add - Forces - Select에서 cantileverBeam_surface_0을 선택한다.

이후, Surface Montior는 아래 그림과 같이 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/7.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/8.png"><br>
</p>

## 9. Numerical Conditions

본 예제에서는 아래와 같이 설정을 변경한다. 

+ Pressure-Velocity Coupling Scheme : SIMPLEC

+ Discretization Scheme
    + Momentum : Second Order Upwind
    + Turbulence : First Order Upwind

+ Under-Relaxation Factors
    + Pressure : 0.9
    + Momentum : 0.9
    + Turbulence : 0.9
    + Density : 0.9

+ Convergence Criteria
    + Pressure : 0.001
    + Momentum : 0.001
    + Turbulence : 0.001

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/9.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/10.png"><br>
</p>

## 10. Initialization

다음과 같이 Initial 값을 설정하면 된다.

+ Velocity
    + X-Velocity : 80 (m/s)
    + Y-Velocity : 0 (m/s)
    + Z-Velocity : 0 (m/s)

+ Pressure
    + 0 (Pa)

+ Turbulence
    + Scale of Velocity : 80 (m/s)
    + Turbulent Intensity : 0.1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/11.png"><br>
</p>

값을 입력하고 하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다.

## 11. Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Number of Iterations : 1,000
    + Save Interval : 100
    + Data Write Format : Binary
    + 메뉴의 Parallel - Environment를 선택하고 Number of Cores는 4, Parallel Type은 Local Machine을 선택

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/12.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/13.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/14.png"><br>
</p>

계산이 완료되면 아래와 같이 Residuals과 Forcegit monitor의 그래프가 나온다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/15.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/16.png"><br>
</p>

## 12. 후처리

External tools의 paraivew 버튼을 클릭하여 실행한다. 본 예제에서는 외팔보 주변 압력장을 그려본다.

Case Type을 Decomposed Case로 변경한다.

Slice 버튼을 눌러 단면을 자른다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/17.png"><br>
</p>

축 방향은 Y Normal로 변경, Origin은 (200, 115, 125)로 변경한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/18.png"><br>
</p>

이후 상단의 p를 p_rgh로 변경한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/19.png"><br>
</p>

아래 그림과 같은 외팔보 주변 압력 분포가 나오게 된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/20.png"><br>
</p>
