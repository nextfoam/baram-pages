---
layout: post
title: 12. Atmosphere Boundary Conditions
category: tutorials
---
# Cantilever Beam 

## * [격자 파일 다운로드](https://drive.google.com/file/d/14Fl8OJUSvlWhayietAzy_dCwoqhMXoX9/view?usp=sharing)

## 1) 개요 
* 본 예제는 정상상태 비압축성 유동해석 예제이다.<br>

* 입구 영역에서 유입되는 공기에 의해 외팔보가 (Cantilever Beam) 변형되는 정도를 확인하는 1way FSI (Fluid Structure Interaction) 예제이다.<br>

* 외팔보는 두께 5mm, 길이 50mm, 높이 150mm이다. 절반만 모델링하여 Symmetry 경계 조건을 부여한다.<br>

* 아래 그림에서 형상과 격자를 나타내었다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/1.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/2.png"><br>
</p>

계산 조건은 다음과 같다. <br>

●  solver : buoyantSimpleNFoam (넥스트폼이 개발한 정상상태 비압축성 해석 솔버) <br>

●  난류 모델 : Standard 𝑘 − ε<br>

●  밀도 : 1.225𝑘𝑔/㎥ <br>

●  점성 계수 : 1.79e-5𝑘𝑔/𝑚s <br>

●  유동 조건 : inlet에서 80m/s  <br>

BaramFlow를 실행하면 아래 과정을 따라서 case 파일을 만든다.<br>

●  New Case버튼 클릭<br>

●  Project Name : cantileverBeam<br>

●  Flow Type : incompressible<br>

●  Multiphase Model : Off<br>

● Species Model : Not Include<br>

## 2) 격자
 격자는 주어진 polyMesh 폴더를 활용한다. <br>
상단 탭에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다. <br>

## 3) 계산 조건
### (1) General
본 예제에서는 Default로 설정한다.<br>

### (2) Models
본 예제에서 사용하는 난류 모델은 Default인 Standard 𝑘 − ε 모델로 설정한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/3.png"><br>
</p>

### (3) Materials
본 예제에서는 공기의 물성치를 Default로 설정한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/4.png"><br>
</p>

### (4) Boundary Conditions
아래와 같이 경계면 타입과 경계값을 설정한다.<br>

***●  Hex6_1_xMin : velocity Inlet***<br>
```Velocity Specfication Method : Magnitude, Normal to Boundary```<br>
```Profile Type : Constant```<br>
```Velocity Magnitude : 80 (m/s)```  <br>
```Turbulent Intensity : 1 (%)```  <br>
```Turbulent Viscosity Ratio : 10```  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/5.png"><br>
</p>

***●  Hex6_1_zMax : velocity Inlet***<br>
```Velocity Specfication Method : Component```<br>
```Profile Type : Constant```<br>
```X-Velocity : 80 (m/s)```  <br>
```Y-Velocity : 0 (m/s)```  <br>
```Z-Velocity : 0 (m/s)```  <br>
```Turbulent Intensity : 1 (%)```  <br>
```Turbulent Viscosity Ratio : 10```  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/Hex6_1_zMax.png"><br>
</p>

***●  Hex6_1_xMax : Pressure Outlet***<br>
```Total Pressure : 0 (Pa)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/6.png"><br>
</p>

***●  Hex6_1_yMin, Hex6_1_yMax : Symemtry***<br>

***●  cantileverBeam_surface_0 : Wall***<br>
```Velocity Condition : No Slip```<br>

### (5) Monitoring
본 예제에서는 Cantilever 전면에 걸리는 압력을 모니터링한다.<br>

Monitors - Add - Forces - Select에서 cantileverBeam_surface_0을 선택한다.<br>

이후, Surface Montior는 아래 그림과 같이 설정한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/7.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/8.png"><br>
</p>

### (6) Numerical Conditions
본 예제에서는 아래와 같이 설정을 변경한다. <br>

●  Pressure-Velocity Coupling Scheme : SIMPLEC <br>

●  Discretization Scheme  <br>
```Momentum : Second Order Upwind``` <br>
```Turbulence : First Order Upwind``` <br>

●  Under-Relaxation Factors  <br>
```Pressure : 0.9```<br>
```Momentum : 0.9```<br>
```Turbulence : 0.9```<br>
```Density : 0.9``` <br>

●  Convergence Criteria  <br>
```Pressure : 0.001``` <br>
```Momentum : 0.001``` <br>
```Turbulence : 0.001``` <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/9.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/10.png"><br>
</p>

### (8) Initialization
다음과 같이 Initial 값을 설정하면 된다.

●  Velocity  <br>
```X-Velocity : 80 (m/s)``` <br>
```Y-Velocity : 0 (m/s)``` <br>
```Z-Velocity : 0 (m/s)``` <br>

●  Pressure  <br>
``` 0 (Pa)``` <br>

●  Turbulence <br>
```Scale of Velocity : 80 (m/s)``` <br>
```Turbulent Intensity : 0.1 (%)``` <br>
```Turbulent Viscosity Ratio : 10``` <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/11.png"><br>
</p>

값을 입력하고 하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다. <br>

### (9) Run
Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.<br>

●  Number of Iterations : 1,000  <br>

●  Save Interval : 100  <br>

●  Data Write Format : Binary  <br>

●  Number of Cores : 8  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/12.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/13.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/14.png"><br>
</p>

계산이 완료되면 아래와 같이 Residuals과 Force monitor의 그래프가 나오게 된다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/15.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/16.png"><br>
</p>

## 4) 후처리

### (1) 경계면 스칼라 분포
External tools의 paraivew 버튼을 클릭하여 실행한다.<br>
본 예제에서는 외팔보 주변 압력장을 그려본다.<br>

Case Type을 Decomposed Case로 변경한다.<br>

Slice 버튼을 눌러 단면을 자른다.<br>


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/17.png"><br>
</p>

축 방향은 Y Normal로 변경, Origin은 (200, 115, 125)로 변경한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/18.png"><br>
</p>

이후 상단의 p를 p_rgh로 변경한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/19.png"><br>
</p>

아래 그림과 같은 외팔보 주변 압력 분포가 나오게 된다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/cantilever/20.png"><br>
</p>
