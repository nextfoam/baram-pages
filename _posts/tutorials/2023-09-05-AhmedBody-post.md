---
layout: post
title: 02. Ahmed Body
category: tutorials
---


# Ahmed Body 

### * [격자 파일 다운로드](https://drive.google.com/file/d/1qVQqF6oavui3NCoAQ2QCpSmo824CVbx_/view?usp=sharing)

## 1. 개요 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/intro.png"><br>
</p>

S.R. Ahmed는 단순화된 자동차 모형을 이용해 후방 경사각에 따른 유동 구조의 변화를 실험을 통해 관찰하였다. 이후 이 문제는 자동차 외부 공력해석의 검증용으로 많이 사용되고 있다. 이 에제는 후방 경사각도가 25인 경우에 속도 40m/s 조건에 대한 예제로 정상상태 비압축성 유동 조건을 사용한다. 

ref : _S.R. Ahmed, G. Ramm, Some Salient Features of the Time-Averaged Ground Vehicle Wake, SAE-Paper 840300, 1984_

계산 조건은 다음과 같다. <br>

●  solver : buoyantSimpleNFoam (넥스트폼이 개발한 정상상태 비압축성 해석 솔버) <br>

●  난류 모델 : Realizable 𝑘 − ε<br>

●  밀도 : 1.2𝑘𝑔/㎥ <br>

●  점성 계수 : 1.8e-5𝑘𝑔/𝑚s <br>

●  유동 조건 : inlet에서 40m/s  <br>

BARAM을 실행하면 아래 과정을 따라서 case 파일을 만든다.<br>

●  New Case버튼 클릭<br>

●  Project Name : ahmedBody<br>

●  Flow Type : incompressible<br>

●  Multiphase Model : Off<br>

● Species Model : Not Include<br>

## 2. 격자

 격자는 주어진 polyMesh 폴더를 활용한다. <br>
상단 탭에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.1.1.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.1.2.png"><br>
</p>

## 3. General

본 예제에서는 Default로 설정한다.<br>

## 4. Models

난류 모델은 Realizable 𝑘 − ε 모델을 사용하고 나머지는 Default를 사용한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.2.png"><br>
</p>

## 5. Materials

본 예제에서는 공기의 물성치를 다음과 같이 수정하여 사용한다. <br>

***●  air***<br>
```Density : 1.2𝑘𝑔/㎥ (m/s)```  <br>
```Viscosity : 1.8e-5𝑘𝑔/𝑚s```  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.3.png"><br>
</p>

## 6. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.<br>

***●  minx : velocity Inlet***<br>
```Velocity Specfication Method : Magnitude, Normal to Boundary```<br>
```Profile Type : Constant```<br>
```Velocity Magnitude : 40 (m/s)```  <br>
```Turbulent Intensity : 1 (%)```  <br>
```Turbulent Viscosity Ratio : 10```  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.4.png"><br>    
</p>

***●  maxx : Pressure Outlet***<br>
```Total Pressure : 0 (Pa)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.5.png"><br>
</p>

***●  miny : Wall (Velocity Condition : Translation Moving Wall)***<br>
```Velocity : (40, 0, 0)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.6.png"><br>
</p>

***●  bottom, leg, nose1, nose2, nose3, nose4, nose5, rear, side, slant, top : Wall***<br>
```Velocity Condition : No Slip```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.7.png"><br>
</p>

***●  minz, maxz, maxy : symmetry***<br>

## 7. Monitoring

본 예제에서는 자동차에 걸리는 공력 계수를 모니터링한다.<br>

Reference Values에 아래와 같이 입력한다.<br>

●  Area : 0.056 <br>

●  Density : 1.2 <br>

●  Length : 1 <br>

●  Pressure : 0 <br>

●  Velocity : 40 <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.8.png"><br>
</p>

이후 Monitors - Add - Forces를 선택하여 아래 그림과 같이 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.9.png"><br>
</p>

## 8. Numerical Conditions

본 예제에서는 아래와 같이 설정을 변경한다. <br>

●  Pressure-Velocity Coupling Scheme : SIMPLE <br>

●  Discretization Scheme  <br>
```Momentum : Second Order Upwind``` <br>
```Turbulence : First Order Upwind``` <br>

●  Under-Relaxation Factors  <br>
```Pressure : 0.3```<br>
```Momentum : 0.7```<br>
```Turbulence : 0.7```<br>
```Density : 0.9``` <br>

●  Convergence Criteria  <br>
```Pressure : 0.001``` <br>
```Momentum : 0.001``` <br>
```Turbulence : 0.001``` <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.10.1.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.10.2.png"><br>
</p>

## 9. Initialization

다음 값으로 Initial 값을 설정하면 된다.

●  Velocity  <br>
```X-Velocity : 40 (m/s)``` <br>
```Y-Velocity : 0 (m/s)``` <br>
```Z-Velocity : 0 (m/s)``` <br>

●  Pressure  <br>
``` 0 (Pa)``` <br>

●  Turbulence <br>
```Scale of Velocity : 40 (m/s)``` <br>
```Turbulent Intensity : 1 (%)``` <br>
```Turbulent Viscosity Ratio : 10``` <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.11.png"><br>
</p>

값을 입력하고 하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다. <br>

## 10. Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.<br>

●  Number of Iterations : 2,000  <br>

●  Save Interval : 300  <br>

●  Data Write Format : Binary  <br>

●  Number of Cores : 4  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.12.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.25.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.26.png"><br>
</p>

계산이 완료되면 아래와 같이 Residuals과 Force monitor의 그래프가 나오게 된다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.13.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.14.png"><br>
</p>

## 11. 후처리

### (1) 경계면 스칼라 분포
BARAM에서는 paraview를 이용하여 후처리를 진행한다.<br>
후처리 진행 시, External tools의 paraivew 버튼을 클릭하면 된다.<br>
본 예제에서는 유동장 내 압력 분포와 유선을 그려본다.<br>

Case Type을 Decomposed Case로 변경한다.<br>

● Mesh Regions에서 아래 경계면들을 선택한다.<br>
```Bottom, internalMesh, leg, miny, nose1, nose2, nose3, nose5, rear, side, slant, top```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.20.png"><br>
</p>

solid color를 p_rgh로 변경하고 단면에서 압력 분포를 확인한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.15.png"><br>
</p>

### (2) Streamline
차량 주변 유동의 steamline을 확인한다.<br>

아래 그림과 같이 extract block 기능을 활용하여 차량 벽면과 바닥면의 형상을 추출한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/21.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.24.png"><br>
</p>

p를 Solid Color로 변경한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.21.png"><br>
</p>

변경 후 모습<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.22.png"><br>
</p>

왼쪽 Pipeline Browser에서 baram.foam을 한번 클릭하여 활성화 한다.<br>
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.23.png"><br>
</p>

이후, Stream Tracer 버튼을 클릭한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.16.png"><br>
</p>

그 후, 설정을 아래와 같이 변경한다. <br>

●  Seed Type : Point Cloud  <br>

●  Center : (0.7, 0.1, 0.1)  <br>

●  Radius :  0.2 <br>

●  Number of Points : 100 <br>

●  Coloring : Vorticity <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.17.png"><br>
</p>

아래 그림과 같은 streamline 분포가 나온다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.18.png"><br>
</p>
