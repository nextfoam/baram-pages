---
layout: post
title: 03. drivAer
category: tutorials
---


# drivAer 

## * [격자 파일 다운로드](https://drive.google.com/file/d/1uL_roJ1xnBsmG87HTwQ4fie4txDhjCjW/view?usp=sharing)

## 1) 개요 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/intro.png"><br>
</p>

__DrivAer__ 는 자동차 공학 분야에서 사용되는 차량 외부 디자인 및 공기역학 테스트를 위한 실제 차량 모델로 차량의 외부 형태와 공기역학적 특성을 시뮬레이션하고 평가하기 위해 많이 사용된다. 단순화된 모델과 매우 복잡한 양산차 사이의 격차를 줄이기 위해 도입된 모델로 여러 종류의 형상에 대한 CAD 파일과 실험결과들이 공개되어 있다.

이 예제는 사이드 미러와 바퀴가 포함된 fastback 모델을 사용한다.

https://www.epc.ed.tum.de/en/aer/research-groups/automotive/drivaer/

계산 조건은 다음과 같다. <br>

●  solver : buoyantSimpleNFoam (넥스트폼이 개발한 정상상태 비압축성 해석 솔버) <br>

●  난류 모델 : Realizable 𝑘 − ε<br>

●  밀도 : 1.205𝑘𝑔/㎥ <br>

●  점성 계수 : 1.82e-5𝑘𝑔/𝑚s <br>

●  유동 조건 : inlet에서 30m/s  <br>

BARAM을 실행하면 아래 과정을 따라서 case 파일을 만든다.<br>

●  New Case버튼 클릭<br>

●  Project Name : drivAer<br>

●  Flow Type : incompressible<br>

●  Multiphase Model : Off<br>

● Species Model : Not Include<br>

## 2) 격자
 격자는 주어진 polyMesh 폴더를 활용한다. <br>
상단 탭에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/1.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/2.png"><br>
</p>

## 3) 계산 조건
### (1) General
본 예제에서는 Default로 설정한다.<br>

### (2) Models
난류 모델은 Realizable 𝑘 − ε 모델을 사용하고 나머지는 Default를 사용한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/3.png"><br>
</p>

### (3) Materials
본 예제에서는 공기의 물성치를 다음과 같이 수정하여 사용한다. <br>

***●  air***<br>
```Density : 1.205𝑘𝑔/㎥ (m/s)```  <br>
```Viscosity : 1.82e-5𝑘𝑔/𝑚s```  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/4.png"><br>
</p>

### (4) Boundary Conditions
아래와 같이 경계면 타입과 경계값을 설정한다.<br>

***●  minX : velocity Inlet***<br>
```Velocity Specfication Method : Magnitude, Normal to Boundary```<br>
```Profile Type : Constant```<br>
```Velocity Magnitude : 30 (m/s)```  <br>
```Turbulent Intensity : 0.01 (%)```  <br>
```Turbulent Viscosity Ratio : 10```  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/5.png"><br>
</p>

***●  maxX : Pressure Outlet***<br>
```Total Pressure : 0 (Pa)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/6.png"><br>
</p>

***●  minY, maxY, maxZ : Symemtry***<br>

***●  minZ : Wall***<br>
```Velocity Condition : Translational Moving Wall```<br>
```Velocity```<br>
```(30, 0, 0)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/7.png"><br>
</p>

***●  body_no_wheel : Wall***<br>
```Velocity Condition : No Slip```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/8.png"><br>
</p>

***●  Wheels_Front_Smooth : Wall***<br>
```Velocity Condition : Rotational Moving Wall```<br>
```Speed (RPM) : 898.8```<br>
```Rotation-Axis Origin : (0.007, 0, 0)```<br>
```Rotation-Axis Direction : (0, -1, 0)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/9.png"><br>
</p>

***●  Wheels_Rear_Smooth : Wall***<br>
```Velocity Condition : Rotational Moving Wall```<br>
```Speed (RPM) : 898.8```<br>
```Rotation-Axis Origin : (2.7932, 0, 0)```<br>
```Rotation-Axis Direction : (0, -1, 0)```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/10.png"><br>
</p>

### (5) Monitoring
본 예제에서는 자동차에 걸리는 공력 계수를 모니터링한다.<br>

Reference Values에 아래와 같이 입력한다.<br>

●  Area : 1.08 <br>

●  Density : 1.205 <br>

●  Length : 4.6132 <br>

●  Pressure : 0 <br>

●  Velocity : 40 <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/11.png"><br>
</p>

이후 Monitors - Add - Forces를 선택하여 아래 그림과 같이 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/12.png"><br>
</p>

### (6) Numerical Conditions
본 예제에서는 아래와 같이 설정을 변경한다. <br>

●  Pressure-Velocity Coupling Scheme : SIMPLEC <br>

●  Discretization Scheme  <br>
```Momentum : Second Order Upwind``` <br>
```Turbulence : Second Order Upwind``` <br>

●  Under-Relaxation Factors  <br>
```Pressure : 0.9```<br>
```Momentum : 0.9```<br>
```Turbulence : 0.9```<br>
```Density : 0.9``` <br>

●  Convergence Criteria  <br>
```Pressure : 0.00001``` <br>
```Momentum : 0.001``` <br>
```Turbulence : 0.001``` <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/13.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/14.png"><br>
</p>

### (8) Initialization
다음 값으로 Initial 값을 설정하면 된다.

●  Velocity  <br>
```X-Velocity : 30 (m/s)``` <br>
```Y-Velocity : 0 (m/s)``` <br>
```Z-Velocity : 0 (m/s)``` <br>

●  Pressure  <br>
``` 0 (Pa)``` <br>

●  Turbulence <br>
```Scale of Velocity : 30 (m/s)``` <br>
```Turbulent Intensity : 1 (%)``` <br>
```Turbulent Viscosity Ratio : 10``` <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/15.png"><br>
</p>

값을 입력하고 하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다. <br>

### (9) Run
Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.<br>

●  Number of Iterations : 2,000  <br>

●  Save Interval : 100  <br>

●  Data Write Format : Binary  <br>

●  Number of Cores : 4  <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/16.png"><br>
</p>

계산이 완료되면 아래와 같이 Residuals과 Force monitor의 그래프가 나오게 된다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/17.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/18.png"><br>
</p>

## 4) 후처리

### (1) 경계면 스칼라 분포
External tools의 paraivew 버튼을 클릭하여 실행한다.<br>
본 예제에서는 차량 주변 압력 분포와 유선을 그려본다.<br>

Case Type을 Decomposed Case로 변경한다.<br>

● Mesh Regions에서 아래 경계면들을 선택한다.<br>
```Wheels_Front_Smooth, Wheels_Rear_Smooth, body_no_wheels```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/19.png"><br>
</p>

아래 그림과 같이 extract block 기능을 활용하여 차량 벽면과 바닥면의 형상을 추출한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/21.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/22.png"><br>
</p>

solid color를 p_rgh로 변경하고 단면에서 압력 분포를 확인한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/20.png"><br>
</p>

### (2) Streamline
차량 주변 유동의 steamline을 확인한다.<br>

p를 Solid Color로 변경한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/23.png"><br>
</p>

변경 후 모습<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/24.png"><br>
</p>

왼쪽 Pipeline Browser에서 baram.foam을 한번 클릭하여 활성화 한다.<br>
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/25.png"><br>
</p>

이후, Stream Tracer 버튼을 클릭한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.16.png"><br>
</p>

그 후, 설정을 아래와 같이 변경한다. <br>

●  Seed Type : Point Cloud  <br>

●  Center : (-1.5, 0.1, 0.1)  <br>

●  Radius :  0.2 <br>

●  Number of Points : 100 <br>

●  Coloring : U <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/26.png"><br>
</p>

아래 그림과 같은 streamline 분포가 나온다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/27.png"><br>
</p>