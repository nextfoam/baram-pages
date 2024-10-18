---
layout: post
title: 03. drivAer - Incompressible External Aerodynamics
category: tutorials
---


# drivAer 

### * [격자 파일 다운로드](https://drive.google.com/file/d/1uL_roJ1xnBsmG87HTwQ4fie4txDhjCjW/view?usp=sharing)

### * [계산 파일 다운로드](https://drive.google.com/file/d/1sug9iCm2bMCYez2AsrI164yn_xAm1IOX/view?usp=sharing)

## 1. 개요 

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/intro.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/intro.png){:target="_blank"}|

__DrivAer__ 는 자동차 공학 분야에서 사용되는 차량 외부 디자인 및 공기역학 테스트를 위한 실제 차량 모델로 차량의 외부 형태와 공기역학적 특성을 시뮬레이션하고 평가하기 위해 많이 사용된다. 단순화된 모델과 매우 복잡한 양산차 사이의 격차를 줄이기 위해 도입된 모델로 여러 종류의 형상에 대한 CAD 파일과 실험결과들이 공개되어 있다.

이 예제는 사이드 미러와 바퀴가 포함된 fastback 모델을 사용한다.

[https://www.epc.ed.tum.de/en/aer/research-groups/automotive/drivaer/](https://www.epc.ed.tum.de/en/aer/research-groups/automotive/drivaer/)

정상상태 비압축성 유동에서 moving ground, rotating wheel 조건을 사용한다.

논문의 실험 결과 저항계수(Cd)는 ASME는 0.247, SAE는 0.243이며 계산 결과는 Cd = 0.243으로 SAE 실험결과와 일치한다.

계산 조건은 다음과 같다. 

+ solver : buoyantSimpleNFoam (넥스트폼이 개발한 정상상태 비압축성 해석 솔버)
+ 난류 모델 : $Realizable$ $k-\epsilon$ model
+ 밀도 : 1.205 $kg/m^3$
+ 점성 계수 : 1.82e-5 $kg/ms$
+ 유동 조건 : inlet에서 30 $m/s$ 

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None을 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/launcher.png"><br>
</p>


## 3. 격자

격자는 주어진 polyMesh 폴더를 활용한다. 상단 탭에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/1.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/2.png"><br>
</p>

## 4. General

본 예제에서는 Default로 설정한다.

## 5. Models

난류 모델은 $Realizable$ $k-\epsilon$ 모델을 사용하고 나머지는 Default를 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/3.png"><br>
</p>

## 6. Materials

본 예제에서는 공기의 물성치를 다음과 같이 수정하여 사용한다. 

+ air
    + Density : 1.205𝑘𝑔/㎥ (m/s)
    + Viscosity : 1.82e-5𝑘𝑔/𝑚s

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/4.png"><br>
</p>

## 7. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ minX : velocity Inlet
    + Velocity Specfication Method : Magnitude, Normal to Boundary
    + Profile Type : Constant
    + Velocity Magnitude : 30 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/5.png"><br>
</p>

+ maxX : Pressure Outlet
    + Total Pressure : 0 (Pa)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/6.png"><br>
</p>

+ minY, maxY, maxZ : Symemtry

+ minZ : Wall
    + Velocity Condition : Translational Moving Wall
    + Velocity
    + (30, 0, 0)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/7.png"><br>
</p>

+ body_no_wheel : Wall
    + Velocity Condition : No Slip

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/8.png"><br>
</p>

+ Wheels_Front_Smooth : Wall
    + Velocity Condition : Rotational Moving Wall
    + Speed (RPM) : 898.8
    + Rotation-Axis Origin : (0.007, 0, 0)
    + Rotation-Axis Direction : (0, -1, 0)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/9.png"><br>
</p>

+ Wheels_Rear_Smooth : Wall
    + Velocity Condition : Rotational Moving Wall
    + Speed (RPM) : 898.8
    + Rotation-Axis Origin : (2.7932, 0, 0)
    + Rotation-Axis Direction : (0, -1, 0)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/10.png"><br>
</p>

## 8. Reference Values

공력계수 계산을 위한 Reference Value를 다음과 같이 설정한다.

+ Area : 1.08
+ Density : 1.205
+ Length : 4.6132
+ Pressure : 0
+ Velocity : 30

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/11.png"><br>
</p>

## 9. Numerical Conditions

본 예제에서는 아래와 같이 설정을 변경한다.

+ Pressure-Velocity Coupling Scheme : SIMPLEC

+ Discretization Scheme
    + Pressure : Momentum Weighted Reconstruct
    + Momentum : Second Order Upwind
    + Turbulence : Second Order Upwind

+ Under-Relaxation Factors
    + Pressure : 0.9
    + Momentum : 0.9
    + Turbulence : 0.9
    + Density : 0.9

+ Convergence Criteria
    + Pressure : 0.00001
    + Momentum : 0.001
    + Turbulence : 0.001

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/13.png"><br>
</p>


## 10. Monitoring

본 예제에서는 자동차에 걸리는 공력 계수를 모니터링한다.

이후 Monitors - Add - Forces를 선택하여 아래 그림과 같이 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/12.png"><br>
</p>

## 11. Initialization

다음 값으로 Initial 값을 설정하면 된다.

+ Velocity
    + X-Velocity : 30 (m/s)
    + Y-Velocity : 0 (m/s)
    + Z-Velocity : 0 (m/s)

+ Pressure
    + 0 (Pa)

+ Turbulence
    + Scale of Velocity : 30 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/15.png"><br>
</p>

값을 입력하고 하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다.

## 12. Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Number of Iterations : 2,000
+ Save Interval : 100
+ Data Write Format : Binary
+ 메뉴의 Parallel - Environment를 선택하고 Number of Cores는 4, Parallel Type은 Local Machine을 선택

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/16.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/28.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/29.png"><br>
</p>

계산이 완료되면 아래와 같이 Residuals과 Force monitor의 그래프가 나오게 된다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/residual.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/force.png"><br>
</p>

## 13. 후처리

### 경계면 스칼라 분포

External tools의 paraivew 버튼을 클릭하여 실행한다. 본 예제에서는 차량 주변 압력 분포와 유선을 그려본다.

Case Type을 Decomposed Case로 변경한다.

+ Mesh Regions에서 아래 경계면들을 선택한다.
    + Wheels_Front_Smooth, Wheels_Rear_Smooth, body_no_wheels

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/19.png"><br>
</p>

아래 그림과 같이 extract block 기능을 활용하여 차량 벽면과 바닥면의 형상을 추출한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/21.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/22.png"><br>
</p>

solid color를 p_rgh로 변경하고 단면에서 압력 분포를 확인한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/20.png"><br>
</p>

### Streamline

차량 주변 유동의 steamline을 확인한다.

p를 Solid Color로 변경한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/23.png"><br>
</p>

변경 후 모습

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/24.png"><br>
</p>

왼쪽 Pipeline Browser에서 baram.foam을 한번 클릭하여 활성화 한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/25.png"><br>
</p>

이후, Stream Tracer 버튼을 클릭한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.16.png"><br>
</p>

그 후, 설정을 아래와 같이 변경한다.

+ Seed Type : Point Cloud
+ Center : (-1.5, 0.1, 0.1)
+ Radius :  0.2
+ Number of Points : 100
+ Coloring : U

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/26.png"><br>
</p>

아래 그림과 같은 streamline 분포가 나온다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/27.png"><br>
</p>
