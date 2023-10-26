---
layout: post
title: Sirocco Fan
category: tutorials
---

# Sirocco Fan 

## * [격자 파일 다운로드](https://drive.google.com/file/d/1ziOkgB3Uv9I3V8o9oRJnribBkTqKcR93/view?usp=sharing)

## 1) 개요 
* 본 예제는 비정상상태 비압축성 유동해석 예제이다.<br>

* sirocco fan 내부에서 fan이 회전할 때 내부의 유동을 예측하는 문제이다. <br>

* 격자는 Ansys Fluent의 .cas 형식의 파일을 변환하여 사용하였다.<br>

* 그림 4.1에서 형상과 격자를 나타내었다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.1.png"><br>
    그림 4.1
</p>

계산 조건은 다음과 같다. <br>

●  solver : buoyantPimpleNFoam (넥스트폼이 개발한 동적격자 비압축성 유동 해석 솔버) <br>

●  난류 모델 : Realizable 𝑘 − ε<br>

●  밀도 : 1.225𝑘𝑔/㎥ <br>

●  점성 계수 : 1.79e-5𝑘𝑔/𝑚s <br>

●  임펠러 회전 수 : 2,000RPM  <br>

BARAM을 실행하면 아래 과정을 따라서 case 파일을 만든다.<br>

●  New Case버튼 클릭<br>

●  Project Name : slidingMesh<br>

●  Flow Type : incompressible<br>

●  Multiphase Model : Off<br>

● Species Model : Not Include<br>

## 2) 격자
격자는 주어진 Ansys의 .cas 파일을 활용한다. <br>
상단 탭에서 File - Load Mesh - Fluent Case (ASCII) 순서대로 클릭하고 siroccofan.cas 파일을 선택한다. <br>

## 3) 계산 조건
### (1) General
Time을 Transient로 변경한다.<br>
나머지는 Default로 설정한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.2.png"><br>
    그림 4.2
</p>

### (2) Models
난류 모델은 Realizable 𝑘 − ε 모델을 사용하고 나머지는 Default를 사용한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.3.png"><br>
    그림 4.3
</p>

### (3) Materials
본 예제에서 작동 유체는 공기이다.<br>
유체의 물성치는 Default 조건을 사용한다..<br>

### (4) Cell Zone Conditions
Cell Zone Conditions에서는 MRF, Sliding Mesh, Source 등을 설정할 수 있다.<br>
본 예제에서는 'rotating' Cell Zone에 Sliding Mesh 조건을 설정한다.<br>

rot 선택 - Multiple Reference Fram, MRF를 선택하고 아래 값들을 입력한다.<br>

***●  Sliding Mesh***<br>
```Rotating Speed : 2,000(RPM)```<br>
```Rotation-Axis Origin : (0, 0, 0)```<br>
```Rotation-Axis Direction : (0, 0, 1)```  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.4.png"><br>
    그림 4.4
</p>

### (5) Boundary Conditions
아래와 같이 경계면 타입과 경계값을 설정한다.<br>

**※interface-stat와 interface-rotating은 회전 경계면이다.<br>**

***●  interface-stat, interface-rotating : Interface - Internal Interface***<br>
```interface-stat : Internal Interface로 변경 후, Coupled Boundary는 interface-rotating 선택```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.5.png"><br>
    그림 4.5
</p>

***●  axis : Wall***<br>
```Velocity Condition : Rotational Moving Wall```<br>
```Speed : 2000 (RPM)```  <br>
```Rotation-Axis Origin : 0 0 0```  <br>
```Rotation-Axis Direction : 0 0 1```  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.6.png"><br>
    그림 4.6
</p>

***●  axis-r, blades : Wall***<br>
```Velocity Condition : Moving Wall```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.7.png"><br>
    그림 4.7
</p>

***●  externalwalls, walls : Wall***<br>
```Velocity Condition : No Slip```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.8.png"><br>
    그림 4.8
</p>

***●  inlet : Velocity Inlet***<br>
```Velocity Specification Method : Magnitudde, Normal to Boundary```<br>
```Profile Type : Constant```<br>
```Velocity Magnitude : 1 (m/s)```<br>
```Turbulent Intensity : 0.1 (%)```<br>
```Turbulent Viscosity Ratio : 10```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.9.png"><br>
    그림 4.9
</p>

***●  outlet : Pressure Outlet***<br>
```Total Pressure : 0 (Pa)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.10.png"><br>
    그림 4.10
</p>

### (6) Numerical Conditions
본 예제에서는 Default 조건을 사용한다. <br>

### (7) Initialization
Turbluent Intensity을 0.1 (%)로 변경하고 나머지는 Defalut 값을 사용한다.<br>
하단에 Initializer 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.11.png"><br>
    그림 4.11
</p>

### (8) Run
Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.<br>

●  Time Stepping Method : Fixed  <br>

●  Time Step Size : 0.0001  <br>

●  End Time : 0.3  <br>

●  Data Write Format : Binary  <br>

●  Number of Cores : 4  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.12.png"><br>
    그림 4.12
</p>

아래 그림은 계산중인 Residuals 그래프이다.
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.13.png"><br>
    그림 4.13
</p>

## 4) 후처리

### (1) 축 단면 스칼라 분포
Fan 내부의 압력 contours를 확인하는 과정을 진행한다.<br>
paraview 아이콘을 클릭하여 paraview를 실행한다.<br>

Case Type을 Decomposed Case로 변경한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.14.png"><br>
    그림 4.14
</p>

Slice 기능을 활용하여 용기 내부의 단면을 자른다.<br>

Z-normal 버튼을 클릭 후, Origin을 다음과 같이 변경한다.<br>
●  Origin : 0.06 -0.017 0.05  <br>
●  Normal : 0 0 1  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.15.png"><br>
    그림 4.15
</p>

아래 그림과 같이 fan 내부 속도 분포가 나오게 된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.16.png"><br>
    그림 4.16
</p>