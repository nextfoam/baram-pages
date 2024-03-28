---
layout: post
title: 18. Batch Run - RAE2822 Transonic airfoil
category: tutorials
---

## * [격자 파일 다운로드](https://drive.google.com/file/d/1VgU-XnPKYDr6JGAYo_OU1RzIdPf_dCTQ/view?usp=sharing)

# 1) 개요

본 예제는 Batch Run 예제이다. RAE2822 천음속 에어포일의 받음각 변화에 따른 유동해석을 batch run으로 진행한다. 격자는 RAE2822 transonic airfoil 튜토리얼의 격자를 사용한다.

계산조건은 다음과 같다.

+ 난류 : Inviscid(Euler)
+ 마하수 : 1.5
+ 원방경계 압력 : 100000 Pa
+ 원방경계 온도 : 288 K
+ 받음각 : -20~20도, 2도 간격으로 계산


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/RAE2822/rae-mesh.png"  width=30%>,<img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/RAE2822/rae-pContour.png"  width=47.5%> 
    <br> 격자 및 압력분포
</p>

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

난류 모델에서 Inviscid를 선택한다.

## (3) Materials

Density는 Perfect Gas, Viscosity는 Sutherland를 선택한다. 나머지는 디폴트 조건을 사용한다.
<br>

## (4) 사용자 변수 선언

Batch Run을 위해 필요한 사용자 변수는 받음각, 속도, 항력방향, 양력방향 등이 있으며 다음과 같이 정의한다.

+ AOA : 받음각, 변수로 사용되지는 않지만 다른 변수르 계산할 때 사용된다.
+ UX, UY : x,y 방향 속도, 초기조건 설정에 사용된다.
+ DRAGDIR_X : farfield Riemann 경계조건의 flow direction과 monitors의 drag direction에 사용된다.
+ DRAGDIR_Y : monitors의 drag direction에 사용된다.
+ LIFTDIR_X, LIFTDIR_Y : monitors의 lift direction에 사용된다.

[Solution - Run]으로 가서 변수를 선언한다.

'User Parameters'의 Edit 버튼을 눌러 창이 열리면 'Parameter Values' 옆의 (+)를 눌러 아래 그림과 같이 하나씩 추가한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/batchRun-RAE2822/batchRAE-editParameter.png" width=40%> 
    <br> 사용자 변수 선언
</p>


## (5) Boundary Conditions

경계조건은 다음과 같이 설정한다.

* wing
  + Wall - No slip, adiabatic 

* farfield_in, farfield_out
  + Far-Field Riemann 
  + Flow Direction : X-Component는 $DRAGDIR_X, Y-Component는 $DRAGDIR_Y 
  + Mach Number : 1.5
  + Static Pressure : 100000
  + Static Temperature : 288  
  
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/batchRun-RAE2822/batchRAE-farfield.png" width=40%> 
    <br> farfield Riemann 경계조건
</p>

+ frontAndBackPlanes
  + Empty
  
## (6) Reference Values

+ Area, Length : 0.3048(에어포일의 길이)
+ Density : 1.21(farfield condition)
+ Pressure : 100000(farfield condition)
+ Velocity : 288(farfield condition)

## (7) Numerical Conditions

Formulation은 Implicit, Flux Type은 Roe-FDS를 사용한다. Entropy Fix Coefficient는 0.5를 사용한다. 

Discretization Schemes에서 Flow와 Turbulence 모두 Second Order Upwind를 사용한다.

나머지는 모두 디폴트를 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/RAE2822/rae-nume.png" width=40%> 
    <br> 수치해석 조건
</p>

## (8) Monitors

Add - Forces를 선택하고 다음과 같이 설정한다.

+ Lift Direction : ($LIFTDIR_X, $LIFTDIR_Y, 0)
+ Drag Direction : ($DRAGDIR_X, $DRAGDIR_Y, 0)
+ Boundaries : wing

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/batchRun-RAE2822/batchRAE-monitor.png" width=30%> 
    <br> 수치해석 조건
</p>

## (9) Initialization

초기조건은 다음과 같이 설정한다.

+ Velocity : ($UX, $UY, 0)
+ Pressure : 100000
+ Temperature : 288

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/batchRun-RAE2822/batchRAE-init.png" width=40%> 
    <br> 수치해석 조건
</p>

## (10) Run Conditions

'Run Conditions'는 다음과 같이 설정한다.

+ Number of Iterations : 3000
+ Courant Number : 1000
+ Save Interval : 500

# 4) Run

'Switch To Batch Running Mode' 버튼을 누르면 아래 그림과 같이 Batch Cases 설정 부분이 나타난다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/batchRun-RAE2822/batchRAE-batchCases.png" width=40%> 
    <br> 수치해석 조건
</p>

각 변수의 조건을 설정한 파일을 import 버튼을 눌러 선택하면 조건들이 표시된다. 조건을 설정 파일은 csv(comma separated values) 혹은 xlsx 파일 형식을 사용할 수 있다.

이 예제에서는 아래 그림과 같은 엑셀 파일이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/batchRun-RAE2822/batchRAE-excel.png" width=80%> 
    <br> 수치해석 조건
</p>

[엑셀파일 다운로드](https://drive.google.com/file/d/1KOb8dQ3D1b2gYoWnwmkhgfGxySfArUBP/view?usp=sharing)


Import 버튼을 누르고 위 파일을 선택하면 Batch Cases 부분이 다음 그림과 같이 바뀐다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/batchRun-RAE2822/batchRAE-batchCases1.png" width=40%> 
<br> 수치해석 조건
</p>

마우스의 드래그 앤 드롭을 이용햇서 전체 case를 선택하고 오른쪽 마우스 버튼을 눌러 'Schedule Calculation'을 선택하면 'Calc.' column에 체크 표시가 나타난다. 체크 표시가 된 것들만 계산된다. 

Start Calculation을 누르면 순차적으로 계산이 시작된다. 

제일 왼쪽 colume에 현재 계산중인 케이스에 화살표가 나타난다. 계산이 완료된 케이스는 Result colume에 초록색으로 표시되며, 계산 중 발산한 경우는 빨간색으로 표시된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/batchRun-RAE2822/batchRAE-run.png" width=80%> 
    <br> Residual 그래프
</p>



# 5) 후처리

계산이 끝난후 Batch Cases에서 케이스를 선택하고 마우스 오른쪽 버튼으로 Load를 선택하면 해당 케이스의 결과가 활성화 되고 residual과 모니터 그래프를 확인할 수 있다. External tools의 paraview 버튼을 클릭하여 paraview를 실행하고 압력을 선택하면 다음과 같은 분포를 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/batchRun-RAE2822/batchRAE-paraview.png" width=80%> 
    <br> 받음각 -20도 경우의 압력 분포
</p>


