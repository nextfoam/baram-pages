---
layout: post
title: 01. Mixing Pipe
category: tutorials
---

# Mixing Pipe 

* [격자 파일](https://drive.google.com/file/d/12CyYZO_FSl7Baz-MmbtXnBst02EGg5Tg/view?usp=sharing)

## 1) 개요 
* 본 예제는 정상상태 비압축성 유동해석 예제이다.<br>

* 입구 2개, 출구 1개로 이루어진 원형 파이프 내부 유동의 혼합을 예측한다.<br>

* 아래 그림에서 형상과 격자를 나타내었다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.1.png"><br>
</p>

계산 조건은 다음과 같다. <br>

●  solver : buoyantSimpleNFoam (넥스트폼이 개발한 정상상태 비압축성 해석 솔버) <br>

●  난류 모델 : Realizable 𝑘 − ε<br>

●  밀도 : 1.225𝑘𝑔/㎥ <br>

●  점성 계수 : 1.79e-5𝑘𝑔/𝑚s <br>

●  유동 조건 : in-1의 속도는 5m/s, in-2의 속도는 10m/s, outlet은 pressure oulet  <br>

BARAM을 실행하면 아래 과정을 따라서 case 파일을 만든다.<br>

●  New Case버튼 클릭<br>

●  Project Name : mixingPipe<br>

●  Flow Type : incompressible<br>

●  Multiphase Model : Off<br>

● Species Model : Not Include<br>

## 2) 격자
 격자는 주어진 polyMesh 폴더를 활용한다. <br>
상단 탭에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.2.png"><br>
</p>

**※ 주의 사항 : 여기서 polyMesh폴더를 선택한다.** <br>
**BARAM은 OpenFOAM 솔버를 기반으로 한다. 그리고 OpenFOAM의 격자는 항상 polyMesh 폴더로 되어 있다.** <br>

## 3) 계산 조건
### (1) General
General에서는 Time, Gravity, Operating Pressure등을 설정할 수 있다. 본 예제에서는 Default로 설정한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.3.png"><br>
</p>

### (2) Models
Models에서는 turbulence, Energy, Incompressible/Compressible, Multiphase 등을 설정할 수 있다.<br>
본 예제에서는 Realizable 𝑘 − ε 모델을 사용한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.4.png"><br>
</p>

### (3) Materials
Materials에서는 작동 유체의 물성치 등을 설정할 수 있다. 지금 예제에서는 공기의 물성치를 그대로 사용한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.5.png"><br>
</p>

### (4) Cell Zone Conditions
Cell Zone Conditions에서는 Source, MRF, Sliding Mesh등을 설정할 수 있다. 본 예제에서는 Default로 설정한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.6.png"><br>
</p>

### (5) Boundary Conditions
여러 경계면의 경계값을 설정할 수 있다. 각 경계면을 설정하면 해당 경계면이 하얀색으로 변한다. <br>
또한, 경계면을 마우스 오른쪽 버튼으로 클릭하면 경계면 타입을 변경할 수 있다. 각 경계면의 경계 조건을 아래와 같이 변경하면 된다. <br>

***●  in-1 & in-2 : Velocity Inlet  <br>***

***●  out : Pressure Outlet  <br>***

***●  wall : wall (Default) <br>***

또한, 경계 값은 다음과 같이 설정한다. <br>

***●  in-1***<br>
```Velocity Magnitude : 5 (m/s)```  <br>
```Turbulent Intensity : 0.1 (%)```  <br>
```Turbulent Viscosity Ratio : 10```  <br>

***●  in-2***<br>
```Velocity Magnitude : 10 (m/s)```  <br>
```Turbulent Intensity : 0.1 (%)```  <br>
```Turbulent Viscosity Ratio : 10```  <br>

***●  out***<br>
```Total Pressure : 0 (Pa)```  <br>

***●  wall <br>***
```Velocity Condition : No Slip``` <br>

### (6) Numerical Conditions
Discretization, Relaxation factors, Convergence criteria, Pressure-Velocity coupling등 항목을 설정할 수 있다. <br>
본 예제에서는 아래와 같이 설정을 변경한다. <br>

●  Pressure-Velocity Coupling Scheme : SIMPLEC <br>

●  Discretization Scheme  <br>
```Momentum : Second Order Upwind``` <br>
```Turbulence : First Order Upwind``` <br>

●  Under-Relaxation Factors  <br>
```Pressure, Momentum, Turbulence, Density : 0.9``` <br>

●  Convergence Criteria  <br>
```Pressure : 0.0001``` <br>
```Momentum : 0.001``` <br>
```Turbulence : 0.001``` <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.7.1.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.7.2.png"><br>
</p>

### (7) Monitoring
본 예제에서는 (0, 0, 1) 즉, 출구 중심부에서 압력을 모니터링 한다.<br>
Solution - Monitors를 선택한다. <br>
Monitors 창에서 하단에 Add - Points를 클릭한다. <br>
아래 그림과 같이 설정을 변경하면 된다. <br>

●  Point Monitor  <br>
```Write Interval : 1``` <br>
```Field : p``` <br>
```Coordinate : (0, 0, 1)``` <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.8.png"><br>
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

●  Turbulence <br>
```Scale of Velocity : 5 (m/s)``` <br>
```Turbulent Intensity : 0.1 (%)``` <br>
```Turbulent Viscosity Ratio : 10``` <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.9.png"><br>
</p>

값을 입력하고 하단에 Initializer 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다. <br>

### (9) Run
Run Conditions에서는 Number of Iterations, Save Interval, Parallel 등을 설정한다. <br>
본 예제에서는 모든 값을 Default로 설정한다. <br>
이후, Run - Start Calculation 버튼을 클릭한다.

## 4) 후처리
BARAM에서는 paraview를 이용하여 후처리를 진행한다.<br>
후처리 진행 시, paraivew 아이콘을 클릭하면 된다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.10.png"><br>
</p>

paraview를 초기 실행 시, 필요한 기능에 대한 설명은 다음과 같다.<br>

●  Skip Zero Time : 초기값을 제외한 결과를 보여준다.<br>

●  Case Type : cpu 개수에 따른 설정이다.<br>
```Reconstructed Case : 1core 계산 혹은 Parallel로 계산을 진행했지만 reconstructPar를 진행한 OpenFOAM case``` <br>
```Decomposed Case : Parallel 계산을 진행한 case``` <br>

●  Mesh Regions : 보고 싶은 Internal mesh, 경계면 등을 설정할 수 있다.<br>

●  Cell Arrays : 보고 싶은 물리량을 설정할 수 있다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.11.png"><br>
</p>

### (1) 경계면 스칼라 분포
벽면에 걸리는 압력을 확인해보는 과정을 진행한다.<br>
초기 설정을 아래와 같이 해준다.<br>

●  Skip Zero Time : 비활성화<br>

●  Mesh Regions : internalMesh - 활성화<br>

●  나머지 : Default<br>

p_rgh는 상대 압력, p는 절대 압력을 나타낸다.<br>
p_rgh를 선택하면 벽면에 걸리는 압력의 크기를 확인할 수 있다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.12.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.13.png"><br>
</p>


### (2) 축단면 스칼라 분포
Pipe 내부 높이에 따른 압력 분포를 확인해본다.

slice 버튼을 클릭한다.
그 후, 방향을 Z-normal로 바꾸고 pipe 내부 압력을 확인한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.14.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.15.png"><br>
</p>