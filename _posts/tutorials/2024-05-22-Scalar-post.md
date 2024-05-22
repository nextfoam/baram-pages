---
layout: post
title: 22. Air age in Mixing Pipe - User-defined Scalars
category: tutorials
---

# Air Age in Mixing Pipe 

### * [케이스 파일 다운로드](https://drive.google.com/file/d/1sNnqoJQ2h7BQXPoa3C_sVRCixTKJN841/view?usp=sharing)

## 1. 개요 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/scalar/postprocess.png"><br>
    [공기 연령 분포]
</p>

본 예제는 정상상태 비압축성 유동해석 예제이다. 2개의 입구와 1개의 출구로 이루어진 원형 파이프 내부 유동의 혼합을 예측한다.
이 때, 파이프 내부 공기 연령을 계산한다.

계산 조건은 다음과 같다. 

+ solver : buoyantSimpleNFoam (넥스트폼이 개발한 정상상태 비압축성 해석 솔버)
+ 난류 모델 : Standard $k-\epsilon$ model
+ 밀도 : 1.225 $kg/m^3$
+ 점성 계수 : 1.79e-5 $kg/ms$
+ 유동 조건 : 면적이 넓은 입구(in-1)의 속도는 5m/s, 면적이 좁은 입구(in-2)의 속도는 10m/s, outlet은 대기압 조건

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 '01.mixingPipe' project를 선택 후, ‘Open’을 클릭한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/scalar/open.png"><br>
</p>

## 3. User-defined Scalars

이미 유동 해석 계산이 완료된 케이스 파일에 User-Defined Scalar를 추가하여 공기 연령을 계산한다.

Setup - Models - User-defined Scalars를 클릭하고 아래 그림과 같이 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/scalar/scalarDefine.png"><br>
</p>

## 4. Cell Zone Conditions

Cell Zone Conditions에서 region0를 클릭하여 아래 그림과 같이 airAge에 대해 소스를 추가한다.

+ airAge
    + Specification Method : Value per Unit Volume
    + Value : 1.225

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/scalar/cellzoneConditions.png"><br>
</p>

## 5. Numerical Conditions

Discretization, Relaxation factors, Convergence criteria, Pressure-Velocity coupling등 항목을 설정할 수 있다.

본 예제에서는 아래와 같이 설정을 변경한다.

+ Pressure-Velocity Coupling Scheme : SIMPLEC

+ Discretization Scheme
    + Pressure : Momentum Weighted Reconstruct
    + Momentum : Second Order Upwind
    + Turbulence : Second Order Upwind
    + Scalar : Second Order Upwind

+ Under-Relaxation Factors
    + Pressure, Momentum, Turbulence, Scalar : 0.9

+ Convergence Criteria
    + Pressure : 0.00001
    + Momentum, Turbulence, Scalar : 0.0001

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/scalar/numericalCondition1.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/scalar/convergenceCriteria.png"><br>
</p>

여기까지 진행 후, File - save 버튼을 눌러 Project를 저장한다.<br>

## 6. Run

Run Conditions에서 Number of Iteraions를 2000으로 수정한다. 

이후, Run - Start Calculation 버튼을 클릭한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/scalar/residuals.png"><br>
</p>

## 7. Post Processing

BARAM에서는 ParaView를 이용하여 후처리를 진행한다. 후처리 진행 시, External tools의 ParaView 버튼을 클릭하면 된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.10.png"><br>
</p>

ParaView를 초기 실행 시, 필요한 기능에 대한 설명은 다음과 같다.

+ Skip Zero Time : 초기값을 제외한 결과를 보여준다.

+ Case Type : cpu 개수에 따른 설정이다.
    + Reconstructed Case : 1core 계산 혹은 Parallel로 계산을 진행했지만 reconstructPar를 진행한 OpenFOAM case
    + Decomposed Case : Parallel 계산을 진행한 case

+ Mesh Regions : 보고 싶은 Internal mesh, 경계면 등을 설정할 수 있다.

+ Cell Arrays : 보고 싶은 물리량을 설정할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/1.11.png"><br>
</p>


### 축단면 스칼라 분포 (Air Age)

Pipe 내부의 압력 분포를 확인해본다.

slice 버튼을 클릭하고 방향을 Y-normal로 바꿔서 pipe 내부 압력을 확인한다.

물리량을 airAge로 변경하여 파이프 단면에서 공기 연령을 그린다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/scalar/slice.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/scalar/paraview.png"><br>
</p>


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/scalar/airAge.png"><br>
</p>