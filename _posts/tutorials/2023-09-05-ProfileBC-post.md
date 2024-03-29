---
layout: post
title: 09. Profile Boundary Condition
category: tutorials
---

# Profile Boundary Condition

## * [격자 파일 다운로드](https://drive.google.com/file/d/1pzp6DXomC0cyaxn0xzlpcneShrEkRW68/view?usp=sharing)

## 1) 개요
* 본 예제는 시간에 따라 입구의 속도와 온도가 변하는 경계조건과, 주어진 데이터를 사용하여 경계면에서 속도와 온도의 분포를 설정하는 예제이다.<br>

* OpenFOAM 튜토리얼에 있는 pitzDaily 격자를 사용한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.1.png"><br>
</p>

계산 조건은 다음과 같다. <br>

●  solver : buoyantPimpleNFoam (넥스트폼이 개발한 비압축성 유동 해석자) <br>

●  난류 모델 : 𝑘 − ε <br>

●  밀도 : Perfect Gas (Ideal Gas) <br>

●  점성 계수 : 1.79e-5𝑘𝑔/𝑚s <br>

●  Flow Type : Incompressible <br>

●  Solver Type : Pressure-based <br>

●  Multiphase Model : off <br>

●  Species Model : Not include <br>

## 2) 격자
격자는 주어진 OpenFOAM의 polyMesh 폴더를 활용한다. <br>
상단 탭에서 File - Load Mesh - OpenFOAM 순서대로 클릭한다. <br>

## 3) 계산 조건
### (1) General
Time advance는 Transient로 바꿔준다. <br>
나머지는 Default를 사용한다. <br>

### (2) Models
난류 모델은 𝑘 − ε 모델을 사용하고 Energy는 Include로 바꿔준다. <br>

### (3) Materials
본 예제에서는 공기를 작동 유체로 사용한다.<br>
유체의 이름과 물성치를 아래와 같이 변경한다. <br>

***●  air***<br>
```Density : Perfect Gas (m/s)```  <br>
```Specific Heat (Cp) : 1004J/kgK (m/s)```  <br>
```Viscosity : 1.79e-05𝑘𝑔/𝑚s```  <br>
```Thermal Conductivity : 0.0245W/mK```  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/Perfect Gas.png"><br>
</p>

### (4) Cell Zone Conditions
Cell Zone Conditions은 Default 조건을 사용한다.<br>

### (5) Boundary Conditions
아래와 같이 경계면 타입과 경계값을 설정한다.<br>

***●  inlet : Velocity Inlet***<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.3.png"><br>
</p>

```Velocity Specification Method : Magnitude, Normal to Boundary```<br>
```Velocity Profile Type : Temporal Distribution```<br>
```Piecewise Linear : 0 : 0   1```<br>
```		              1 : 0.1 2```<br>
```		              2 : 0.2 1.5```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.4.png"><br>
</p>

```Turbulent Intensity : 1 (%)```<br>
```Turbulent Viscosity Ratio : 10```<br>
```Temperature Profile Type : Temporal Distribution```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.5.png"><br>
</p>

***●  outlet : Pressure Outlet***<br>
```Total Pressure : 0 (Pa)```<br>

***●  upperWall, lowerWall : Wall***<br>
```Velocity Condition : No Slip```<br>
```Temperature : Adiabatic```<br>

***●  frontAndBack : empty***<br>


### (6) Numerical Conditions
Numerical Conditions은 Default 조건을 사용한다.<br>

### (7) Monitors
Monitors를 클릭하면 세부설정상자가 나온다.<br>
입구에서 유량과 온도 변화를 모니터링 한다.<br>
하단의 Add - Surfaces 를 누르면 Surface Monitor 창이 나온다.<br>
아래 그림과 같이 설정을 변경하면 된다.<br>

●  Surface Monitor 1  <br>
```Report Type : Mass Flow Rate```<br>
```Surface : inlet```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.6.png"><br>
</p>


●  Surface Monitor 2  <br>
```Report Type : Area-Weighted Average```<br>
```Field Variable : Temperature```<br>
```Surface : inlet```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.7.png"><br>
</p>

### (8) Initialization

Initial Contion은 초기값으로 x, y, z의 속도와 압력을 입력할 수 있다.<br>
난류 모델을 사용할 경우 Velocity Scale, Turbulent Intensity, Viscosity Ratio 값을 입력하면 k와 ε 값이 계산되어 사용된다. <br>

●  Velocity  <br>
```X-Velocity : 0 (m/s)``` <br>
```Y-Velocity : 0 (m/s)``` <br>
```Z-Velocity : 0 (m/s)``` <br>

●  Pressure  <br>
``` 0 (Pa)``` <br>

●  Temperature  <br>
``` 300 (K)``` <br>


●  Turbulence <br>
```Scale of Velocity : 1 (m/s)``` <br>
```Turbulent Intensity : 1 (%)``` <br>
```Turbulent Viscosity Ratio : 10``` <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.8.png"><br>
</p>

값을 입력하고 하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다. <br>

### (9) Run Conditions
Run Conditions에서는 Number of Iterations, Save Interval, Parallel 등을 설정한다. <br>

●  Run Conditions  <br>
```Time Step Size : 0.001``` <br>
```End Time : 1``` <br>
```Set Interval (Every) : 0.1``` <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.9.png"><br>
    그림 11.9
</p>

이후, Run - Start Calculation 버튼을 클릭한다. <br>
하단의 Residuals 탭을 클릭하면 아래와 같이 그래프를 확인할 수 있다. <br>
Monitor 탭을 클릭하면 입구의 온도와 유량의 변화를 확인할 수 있다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.10.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.11.png"><br>
</p>

## 4) 후처리
시간에 따른 온도 및 속도의 분포를 확인한다.<br>
External tools의 paraview 버튼을 눌러 paraview를 실행한다.<br>
상단의 Solid Color를 T로 변경한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.12.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.13.png"><br>
</p>

이후, Set Range를 눌러 온도 범위를 340 - 350K으로 조정한다.<br>
그리고 상단의 Play 버튼을 눌러 시간에 따른 온도 변화를 확인한다.<br>

아래 그림은 최종 순간에서 온도분포를 나타내는 그림이다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/profileBC/10.14.png"><br>
</p>