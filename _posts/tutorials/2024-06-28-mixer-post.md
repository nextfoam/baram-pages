---
layout: post
title: 05. Mixer - MRF, Rotational periodic interface
category: tutorials
---

# Mixer - MRF, Rotational periodic interface

### * [격자 파일 다운로드](https://drive.google.com/file/d/1hDPj81oeEhsQD86Uu9fUZmnIaglgth7c/view?usp=sharing)

### * [계산 파일 다운로드](https://drive.google.com/file/d/1UBi_opGRIYnGxDFeFihTukVEDOI52h2m/view?usp=sharing)

## 1. 개요 

|[![속도/압력 분포](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixer/intro.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixer/intro.png){:target="_blank"}|

본 예제는 다순한 형상의 믹서를 MRF를 이용하여 계산하는 예제이다. MRF 모델을 사용하면 정상상태 계산을 할 수 있으며, 임펠러 날개 하나를 기준으로 회전 주기조건을 사용할 수 있어 계산 비용을 크게 줄일 수 있다. 

계산 조건은 다음과 같다. 

+ solver : buoyantPimpleNFoam (넥스트폼이 개발한 비압축성 유동 해석 솔버)
+ 난류 모델 : $Standard$ $k-\epsilon$ model
+ 밀도 : 1000 $kg/m^3$
+ 점성 계수 : 0.001 $kg/ms$
+ 프로펠러 회전 수 : 100 RPM

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None, ‘Species’는 Not Include를 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/launcher.png"><br>
</p>

## 3. 격자

격자는 주어진 polyMesh 폴더를 활용한다. 상단 탭에서 File - Load Mesh - OpenFOAM을 클릭하고 polyMesh 폴더를 선택한다. 

## 4. General

모두 Default를 사용한다.

## 5. Models

모두 Default를 사용한다.

## 6. Materials

Name을 water로 변경하고 Density는 1000, viscosity는 0.001을 입력한다.

## 7. Cell Zone Conditions

'cellZone'에 Multiple Reference Frame, MRF를 선택하고 아래 값들을 입력한다.

+ Multiple Reference Frame
    + Rotating Speed : 100(RPM)
    + Rotation-Axis Origin : (0 0 0)
    + Rotation-Axis Direction : (0 0 1)
    + Static Boundary : periodic1, periodic2

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixer/cellZone.png"><br>
</p>

## 8. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ periodic1, periodic2 : Interface - Rotational Periodic
    + periodic1 : Rotational Periodic으로 변경 후, Coupled Boundary는 periodic2 선택. Rotation-Axis Origin은 (0 0 0), Rotation-Axis Direction은 (0 0 1)을 입력

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixer/interface.png"><br>
</p>

+ impeller, impeller_slave : Thermo-Coupled Wall
    + impeller : Thermo-Coupled Wall로 변경 후, Coupled Boundary는 impeller_slave를 선택

+ wall, hub, hub_rot : Wall
    + Velocity Condition : noSlip

+ top : symmetry


## 9. Numerical Conditions

모두 Default를 사용한다.


## 10. Initialization

모두 Default를 사용한다.


## 11. Run

Run Conditions에서 Number of Iteration을 3000으로 설정하고 계산을 진행한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixer/residual.png"><br>
</p>


