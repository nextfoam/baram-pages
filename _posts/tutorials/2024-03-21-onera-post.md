---
layout: post
title: 26. ONERA M6 Transonic Wing - density based solver
category: tutorials
---

# ONERA M6 Transonic Wing

### * [격자 파일 다운로드](https://drive.google.com/file/d/1JxCKWMaAFoi--1_VFXkVVIhtus1N0ntG/view?usp=sharing)

### * [계산 파일 다운로드](https://drive.google.com/file/d/1mzvMV6pzZt09v1p06xbuY8sdcII3JMhJ/view?usp=sharing)

## 1. 개요

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/onera/onera-mesh.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/onera/onera-mesh.png){:target="_blank"}|


본 예제는 밀도기반 솔버를 사용하는 정상상태 압축성 유동해석 예제이다. ONERA M6 wing의 validation 문제로 아래 사이트의 계산 조건을 사용한다.

[https://www.grc.nasa.gov/WWW/wind/valid/m6wing/m6wing.html](https://www.grc.nasa.gov/WWW/wind/valid/m6wing/m6wing.html)


|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/onera/cp0.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/onera/cp0.png){:target="_blank"}|

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/onera/cp1.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/onera/cp1.png){:target="_blank"}|

<p align='center'>날개의 span 방향 각 섹션의 압력계수</p>


격자는 정렬격자로 만들어진 격자를 OpenFOAM으로 변환한 것을 사용한다. 

계산 조건은 다음과 같다.

+ solver : TSLAeroFoam
+ 난류모델 : kOmegaSST
+ 마하수 : 0.8395
+ 받음각 : 3.06 degree
+ 원방경계 압력 : 315979 Pa
+ 원방경계 온도 : 255.56 K
+ 난류 조건 : k=2.714, $\omega$=131360

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 'New'를 선택한다. 'Solver Type'은 Density-based를, 'Multiphase Model'은 None을 선택한다.

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

* Wall-wing-1, Wall-wing-2
  + Wall - No slip, adiabatic 

+ sym-1, sym-2, sym-3, sym-4 
  + symmetry
  
* inlet-1, inlet-2, outer-1, outer-2, outlet-1, outlet-2
  + Far-Field Riemann 
  + Flow Direction : 받음각 3.06에 해당하는 방향, (0.998574, 0.053382, 0) 
  + Mach Number : 0.8395
  + Static Pressure : 315980
  + Static Temperature : 255.56  
  + Turbulence : k and omega(k = 2.714, omega = 131360)
  
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/onera/onera-farfield.png"> 
    <br> farfield Riemann 경계조건
</p>



## 8. Numerical Conditions

Formulation은 Implicit, Flux Type은 Roe-FDS를 사용한다. Entropy Fix Coefficient는 0.5를 사용한다. 

Discretization Schemes에서 Flow와 Turbulence 모두 Second Order Upwind를 사용한다.

Convergence Criteria에서 Density의 값을 1e-5으로 설정한다

나머지는 모두 디폴트를 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/RAE2822/rae-nume.png"> 
    <br> 수치해석 조건
</p>

## 9. Monitors

Add - Forces를 선택하고 다음과 같이 설정한다.

+ Lift Direction : (-0.053382, 0.998574, 0)
+ Drag Direction : (0.998574, 0.053382, 0)
+ Boundaries : wall-wing-1, wall-wing-2


## 10. Initialization

초기조건은 다음과 같이 설정한다.

+ Velocity : (268.647, 14.361, 0)
+ Pressure : 315980
+ Temperature : 255.56
+ Turbulence
  + Scale of Velocity : 269.031
  + Turbulent Intensity : 0.1
  + Turbulent Viscosity Ratio : 1 


## 11. Run Conditions

'Run Conditions'는 다음과 같이 설정한다.

+ Number of Iterations : 3000
+ Courant Number : 1000
+ Save Interval : 500

## 12. Run

Start Calculation을 누르면 계산이 시작된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/onera/onera-run.png"> 
    <br> Residual 그래프
</p>



## 13. 후처리

External tools의 paraview 버튼을 클릭하여 paraview를 실행하고 압력을 선택하면 다음과 같은 분포를 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/onera/onera-paraview.png"> 
    <br> 압력 분포
</p>


