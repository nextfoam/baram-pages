---
layout: post
title: 18. Supersonic Nozzle - density based solver
category: tutorials
---

## * [격자 파일 다운로드](https://drive.google.com/file/d/1Z5d0Ic9GsMxF1fPr8rSCpv9juU223xuM/view?usp=sharing)

# 1) Sunersonic Nozzle 개요

본 예제는 밀도기반 솔버를 사용하는 축대칭 초음속 노즐 유동해석 예제이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/nozzle/nozzle-mesh.png"  width=45%>,<img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/nozzle/nozzle-mach.png"  width=46%> 
    <br> 격자 및 마하수분포
</p>

계산 조건은 다음과 같다.

+ solver : TSLAeroFoam
+ 난류모델 : kOmegaSST
+ 노즐 입구 전압력 : 4e+5 Pa
+ 노즐 입구 온도 : 3000 K
+ 원방경계 압력 : 1e+4 Pa
+ 원방경계 온도 : 300 K

# 2) 프로그램의 구동

프로그램 실행 후 launcher에서 'New'를 선택한다. Launcher에서 'Flow Type'은 Compressible, 'Solver Type'은 Density-based를, 'Multiphase Model'은 None, 'Species'는 Not Include를 선택한다.

<p align='center'>
   <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/RAE2822/launcher-densityBased.png"  width=40%> 
    <br> launcher 설정
</p>

# 3) 격자

격자는 주어진 polyMesh 폴더를 사용한다. 상단 메뉴에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.2.png"><br>
</p>

# 4) 계산조건

## (1) General

Operating Conditions에 0을 입력한다. 

## (2) Models

난류 모델은 $SST k - \omega$ 모델을 선택한다.

## (3) Materials

Density는 Perfect Gas, Viscosity는 Sutherland를 선택한다. 나머지는 디폴트 조건을 사용한다.
<br>

## (4) Boundary Conditions

경계조건은 다음과 같이 설정한다.

* inlet
  + Pressure Inlet
  + Total Pressure : 400000
  + Temperature : 3000
  + Turbulence : intensity and viscosity ratio(0.1 and 1)
+ inletAir
  + Pressure Inlet
  + Total Pressure : 10000
  + Temperature : 300 K
  + Turbulence : intensity and viscosity ratio(0.1 and 1)
+ outlet
  + Pressure Outlet
  + Total Pressure : 10000
+ nozzle
  + Wall - no slip, adiabatic
+ top 
  + symmetry
  
* bottomEmptyFaces, topEmptyFaces
  + Wedge 
  
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/nozzle/nozzle-inlet.png" width=40%> 
    <br> farfield Riemann 경계조건
</p>

  
## (5) Numerical Conditions

Formulation은 Implicit, Flux Type은 Roe-FDS를 사용한다. Entropy Fix Coefficient는 0.5를 사용한다. 

나머지는 모두 디폴트를 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/nozzle/nozzle-nume.png" width=40%> 
    <br> 수치해석 조건
</p>

## (6) Monitors

노즐 입구에서의 유량을 모니터링 한다. Add - Surface를 선택하고 다음과 같이 설정한다.

+ Report Type : Mas Flow Rate)
+ Surface : inlet)


## (7) Initialization

초기조건은 다음과 같이 설정한다.

+ Velocity : (0, 0, 0)
+ Pressure : 10000
+ Temperature : 300
+ Turbulence
  + Scale of Velocity : 100
  + Turbulent Intensity : 0.1
  + Turbulent Viscosity Ratio : 1 

노즐 유동이 지나는 영역과 외부 영역의 유동 변수들의 차이가 크기 때문에 계산 초기에 솔버가 불안정하다. 이 문제를 해결하기 위해 노즐 유동 부분의 초기값을 별도로 설정한다.

Initialization-Advanced-Section-Create 를 클릭한 후 다음과 같이 설정한다.

+ region1 - Hex
  + Min. point : (-0.15, -0.1, -0.1)
  + Max. point : (2, 0.065 0.1)
  + Velocity를 선택하고 (100, 0, 0)을 입력
  + Pressure를 선택하고 400000를 입력
  + Temperature를 선택하고 3000을 입력

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/nozzle/nozzle-setFields.png" width=32%>,<img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/nozzle/nozzle-setFields1.png" width=50%> 
    <br> Section 설정 및 압력 초기조건
</p>

## (9) Run Conditions

'Run Conditions'는 다음과 같이 설정한다.

+ Number of Iterations : 100000
+ Courant Number : 1000
+ Save Interval : 500

# 4) Run

Start Calculation을 누르면 계산이 시작된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/nozzle/nozzle-run.png" width=80%> 
    <br> Residual 그래프
</p>



# 5) 후처리

External tools의 paraview 버튼을 클릭하여 paraview를 실행하고 마하수를 선택하면 다음과 같은 분포를 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/nozzle/nozzle-paraview.png" width=80%> 
    ><br> 압력 분포
</p>


