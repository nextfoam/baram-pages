---
layout: post
title: 21. Supersonic Flow around Space Shuttle - density based solver
category: tutorials
---

# Space shuttle supersonic flow

### * [격자 파일 다운로드](https://drive.google.com/file/d/12oc-gY76vct8fNCBbF4dNbAVqmuVCNVP/view?usp=sharing)

## 1. 개요

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/ss/ss-mesh.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/ss/ss-mesh.png){:target="_blank"}|


본 예제는 밀도기반 솔버를 사용하는 정상상태 압축성 초음속 유동해석 예제이다.

계산 조건은 다음과 같다.

+ solver : TSLAeroFoam
+ 난류모델 : kOmegaSST
+ 마하수 : 3
+ 받음각 : 15 degree
+ 원방경계 압력 : 100000 Pa
+ 원방경계 온도 : 288 K

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 'New'를 선택한다. Launcher에서 'Solver Type'은 Density-based를, 'Multiphase Model'은 None, 'Species'는 Not Include를 선택한다.

<p align='center'>
   <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/RAE2822/launcher-densityBased.png"> 
    <br> launcher 설정
</p>

## 3. 격자

격자는 주어진 polyMesh 폴더를 사용한다. 상단 메뉴에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.2.png"><br>
</p>


## 4. General

Operating Conditions에 0을 입력한다. 

## 5. Models

난류 모델은 $SST k - \omega$ 모델을 선택한다.

## 6. Materials

Density는 Perfect Gas, Viscosity는 Sutherland를 선택한다. 나머지는 디폴트 조건을 사용한다.
<br>

## 7. Boundary Conditions

경계조건은 다음과 같이 설정한다.

* spaceShuttle
  + Wall - No slip, adiabatic 

+ maxy 
  + symmetry
  
* minx, maxx, miny, minz, maxz
  + Far-Field Riemann 
  + Flow Direction : 받음각 15에 해당하는 방향, (0.965926, 0, 0.258819) 
  + Mach Number : 3
  + Static Pressure : 100000
  + Static Temperature : 288  
  + Turbulence : intensity and viscosity ratio(0.1 and 1)
  
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ss/ss-farfield.png"> 
    <br> farfield Riemann 경계조건
</p>

  
## 8. Reference Values

+ Area, Length : 1
+ Density : 1.2097(farfield condition)
+ Pressure : 100000(farfield condition)
+ Velocity : 1020.5933(farfield condition)


## 9. Numerical Conditions

Formulation은 Implicit, Flux Type은 Roe-FDS를 사용한다. Entropy Fix Coefficient는 0.5를 사용한다. 

Discretization Schemes에서 Flow와 Turbulence 모두 Second Order Upwind를 사용한다.

Convergence Criteria에서 Density의 값을 1e-5으로 설정한다

나머지는 모두 디폴트를 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/RAE2822/rae-nume.png"> 
    <br> 수치해석 조건
</p>

## 10. Monitors

Add - Forces를 선택하고 다음과 같이 설정한다.

+ Lift Direction : (-0.258819, 0, 0.965926)
+ Drag Direction : (0.965926, 0, 0.258819)
+ Boundaries : spaceShuttle


## 11. Initialization

초기조건은 다음과 같이 설정한다.

+ Velocity : (985.817, 0, 264.149)
+ Pressure : 100000
+ Temperature : 288
+ Turbulence
  + Scale of Velocity : 1020.5933
  + Turbulent Intensity : 0.1
  + Turbulent Viscosity Ratio : 1 


## 12. Run Conditions

'Run Conditions'는 다음과 같이 설정한다.

+ Number of Iterations : 3000
+ Courant Number : 0.1
+ Save Interval : 500

## 13. Run

Start Calculation을 누르면 계산이 시작된다.

초음속 유동의 경우 Courant Number를 높게 시작하면 초기에 발산하는 경우가 많아 작은 값으로 시작한 후 계산이 어느 정도 안정되면 조금씩 높여주면 수렴 속도를 높일 수 있다. 계산 중 Run Condition에서 값을 수정하고 Run에서 Update Configuration 버튼을 누르면 적용된다. 이 예제에서는 0.1로 시작해서 200번 iteration 정도에서 값을 1로 높여주고 400번 정도에서 100으로 높여주었다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ss/ss-run.png"> 
    <br> Residual 그래프
</p>



## 14. 후처리

External tools의 paraview 버튼을 클릭하여 paraview를 실행하고 압력을 선택하면 다음과 같은 분포를 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/ss/ss-paraview.png"> 
    <br> 압력 분포
</p>


