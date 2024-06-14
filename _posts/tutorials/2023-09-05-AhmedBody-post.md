---
layout: post
title: 02. Ahmed Body - Incompressible External Aerodynamics
category: tutorials
---


# Ahmed Body 

### * [격자 파일 다운로드](https://drive.google.com/file/d/1qVQqF6oavui3NCoAQ2QCpSmo824CVbx_/view?usp=sharing)

## 1. 개요 

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/intro.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/intro.png){:target="_blank"}|


S.R. Ahmed는 단순화된 자동차 모형을 이용해 후방 경사각에 따른 유동 구조의 변화를 실험을 통해 관찰하였다. 이후 이 문제는 자동차 외부 공력해석의 검증용으로 많이 사용되고 있다. 이 예제는 후방 경사각도가 25°인 경우에 속도 40m/s 조건에 대한 예제로 정상상태 비압축성 유동 조건을 사용한다. 

ref : _S.R. Ahmed, G. Ramm, Some Salient Features of the Time-Averaged Ground Vehicle Wake, SAE-Paper 840300, 1984_

논문의 실험 결과 항력계수(Cd)는 0.285이며 계산 결과는 0.287로 0.7%의 차이를 보여준다.

계산 조건은 다음과 같다.

+ solver : buoyantSimpleNFoam (넥스트폼이 개발한 정상상태 비압축성 해석 솔버)
+ 난류 모델 : Realizable $k-\epsilon$ model
+ 밀도 : 1.2 $kg/m^3$
+ 점성 계수 : 1.8e-5 $kg/ms$
+ 유동 조건 : inlet에서 40 $m/s$

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None, ‘Species’는 Not Include를 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/launcher.png"><br>
</p>


## 3. 격자

격자는 주어진 polyMesh 폴더를 활용한다. 상단 탭에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.1.1.png"><br>
</p>


## 4. General

본 예제에서는 Default로 설정한다.

## 5. Models

난류 모델은 Realizable $k-\epsilon$ 모델을 사용하고 나머지는 Default를 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.2.png"><br>
</p>

## 6. Materials

본 예제에서는 공기의 물성치를 다음과 같이 수정하여 사용한다. 

+ air
    + Density : 1.2 𝑘𝑔/㎥ 
    + Viscosity : 1.8e-5 𝑘𝑔/𝑚s

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.3.png"><br>
</p>

## 7. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ minx : velocity Inlet
    + Velocity Specfication Method : Magnitude, Normal to Boundary
    + Profile Type : Constant
    + Velocity Magnitude : 40 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.4.png"><br>    
</p>

+ maxx : Pressure Outlet
    + Total Pressure : 0 (Pa)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.5.png"><br>
</p>

+ miny : Wall (Velocity Condition : Translation Moving Wall)
    + Velocity : (40, 0, 0) (m/s)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.6.png"><br>
</p>

+ bottom, leg, nose1, nose2, nose3, nose4, nose5, rear, side, slant, top : Wall
    + Velocity Condition : No Slip

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.7.png"><br>
</p>

+ minz, maxz, maxy : symmetry

## 8. Reference Values

공력계수 계산을 위한 Reference Value를 다음과 같이 설정한다.

+ Area : 0.056(kg/m<sup>2</sup>, 유동 방향에 수직한 단면적의 50%)
+ Density : 1.2 (kg/m<sup>3</sup>)
+ Length : 1 (m)
+ Pressure : 0 (Pa)
+ Velocity : 40 (m/s)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.8.png"><br>
</p>

## 9. Numerical Conditions

본 예제에서는 아래와 같이 설정을 변경한다.

+ Pressure-Velocity Coupling Scheme : SIMPLE

+ Discretization Scheme
    + Pressure : Momentum Weighted Reconstruct
    + Momentum : Second Order Upwind
    + Turbulence : Second Order Upwind

+ Under-Relaxation Factors
    + Pressure : 0.3
    + Momentum : 0.7
    + Turbulence : 0.7

+ Convergence Criteria
    + Pressure : 0.001
    + Momentum : 0.001
    + Turbulence : 0.001

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.10.1.png"><br>
</p>


## 10. Monitoring

본 예제에서는 자동차에 걸리는 공력 계수를 모니터링한다.

Monitors - Add - Forces를 선택하여 아래 그림과 같이 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.9.png"><br>
</p>

## 11. Initialization

다음 값으로 Initial 값을 설정한다.

+ Velocity
    + X-Velocity : 40 (m/s)
    + Y-Velocity : 0 (m/s)
    + Z-Velocity : 0 (m/s)

+ Pressure
    + 0 (Pa)

+ Turbulence
    + Scale of Velocity : 40 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.11.png"><br>
</p>

값을 입력하고 하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다.

## 12. Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Number of Iterations : 2000
+ Save Interval : 300
+ Data Write Format : Binary
+ 메뉴의 Parallel - Environment를 선택하고 Number of Cores는 4, Parallel Type은 Local Machine을 선택

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.12.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.25.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.26.png"><br>
</p>

계산이 완료되면 아래와 같이 Residuals과 Force monitor의 그래프를 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/residual.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/force.png"><br>
</p>

## 13. 후처리

### 경계면 스칼라 분포

BARAM에서는 ParaView를 이용하여 후처리를 진행한다. 후처리 진행 시, External tools의 ParaView 버튼을 클릭한다. 본 예제에서는 유동장 내 압력 분포와 유선을 그려본다.

Case Type을 Decomposed Case로 변경한다.

+ Mesh Regions에서 아래 경계면들을 선택한다.
    + Bottom, internalMesh, leg, miny, nose1, nose2, nose3, nose5, rear, side, slant, top

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.20.png"><br>
</p>

solid color를 p_rgh로 변경하고 단면에서 압력 분포를 확인한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.15.png"><br>
</p>

### Streamline

차량 주변 유동의 streamline을 확인한다.

아래 그림과 같이 extract block 기능을 활용하여 차량 벽면과 바닥면의 형상을 추출한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/drivAer/21.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.24.png"><br>
</p>

p를 Solid Color로 변경한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.21.png"><br>
</p>

변경 후 모습

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.22.png"><br>
</p>

왼쪽 Pipeline Browser에서 baram.foam을 한번 클릭하여 활성화 한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.23.png"><br>
</p>

이후, Stream Tracer 버튼을 클릭한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.16.png"><br>
</p>

그 후, 설정을 아래와 같이 변경한다.

+ Seed Type : Point Cloud
+ Center : (0.7, 0.1, 0.1)
+ Radius :  0.2
+ Number of Points : 100
+ Coloring : Vorticity

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.17.png"><br>
</p>

아래 그림과 같은 streamline 분포가 나온다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ahmedBody/2.18.png"><br>
</p>
