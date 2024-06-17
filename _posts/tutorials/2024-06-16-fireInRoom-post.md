---
layout: post
title: 15. Fire in Room - User Defined Scalar, Heat source
category: tutorials
---

# 실내 화재 해석 

### * [격자 파일 다운로드](https://drive.google.com/file/d/1ySpMPSdtioU4DSJrWAKJEsCT0wihKo44/view?usp=sharing)

## 1. 개요 

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/fireInRoom/intro.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/fireInRoom/intro.png){:target="_blank"}|

실내의 화재를 시뮬레이션하는 문제이다. 화학종과 연소 반응은 계산하지 않고, 화재성장곡선을 이용해서 시간에 따른 발열량과 연소가스 생성량을 에너지방정식과 사용자 정의 스칼라 방정식의 소스로 사용해서 계산한다. 테이블 아래쪽의 육면체 셀존에 소스항을 준다.

화재성장곡선은 다음과 같은 2차 함수를 사용하고 25초 동안 계산한다. 

$S_h = 1000 \cdot t^2$

$S_{gas} = 5 \cdot 10^{-6} \cdot t^2$

계산 조건은 다음과 같다. 

+ solver : buoyantSimpleNFoam (넥스트폼이 개발한 정상상태 비압축성 해석 솔버)
+ 난류 모델 : $standard$ $k-\epsilon$ 모델
+ 밀도 : Perfect Gas
+ 점성 계수 : 1.79e-5 $kg/ms$

## 2. 프로그램의 구동 및 격자

프로그램 실행 후 launcher에서 'New Case'를 선택하고 이름을 지정한다. 'Solver Type'은 Pressure-based, 'Multiphase Model'은 None', 'Species'는 Not Include를 선택한다.

격자는 주어진 OpenFOAM의 polyMesh 폴더를 사용한다.

상단 탭에서 File - Load Mesh - OpenFOAM을 순서대로 클릭하고 polyMesh 폴더를 선택한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fireInRoom/mesh.png"><br>
</p>

## 3. General

Time은 Transient를 선택하고 Gravity는 (0 0 -9.81)을 입력한다.


## 4. Models

난류 모델은 $Standard$ $k-\epsilon$ 모델을 사용한다.

Energy를 include한다.

User-defined Scalar를 추가한다. Field Name은 gas로 주고 diffusivity는 'Laminar and Turbulent Viscosity'를 선택하고 'Laminar/Turbulent Viscosity Coefficient'는 모두 1로 준다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fireInRoom/uds.png"><br>
</p>

## 5. Materials

물성치는 다음과 같이 설정한다.

+ Density : Perfect Gas
+ Specific heat : 1006
+ Viscosity : 1.79e-05
+ Thermal Conductivity : 0.0245
+ Molecular Weight : 28.966

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/mat.png"><br>
</p>

## 6. Cell Zone Conditions

Hex_1에 Energy와 gas의 source term을 설정한다. 

+ Specification Method는 모두 Value for Entire Cell Zone을 선택한다.
+ Temporal Profile Type은 모두 Polynomial을 선택한다. Edit 버튼을 눌러 (0 1 2)에 Energy는 (0 0 1000)을 gas는 (0 0 5e-6)을 입력한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fireInRoom/cellZone.png"><br>
</p>

## 7. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ room : Wall, desk_surface
    + Velocity Condition : No Slip
    + Temperature : Adiabatic

+ door_surface, outlet : Pressure Outlet
    + Total Pressure  : 0

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/train/outletbc.png">
</p>

## 8. Numerical Conditions

Max Iteration per Time Step은 20, Number of Correctors는 2를 입력하고 나머지는 디폴트를 사용한다.


## 9. Initialization

초기조건은 다음과 같이 설정한다.

+ Velocity : (0 0 0)
+ Pressure : 0
+ Temperature : 300
+ Scale of velocity : 1  
+ Turbulent Intensity : 1
+ Turbulent Viscosity Ratio : 10
+ User-defined Scalars - gas : 0

값을 입력하고 하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다.

## 10. Run Conditions & RUN

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Time Stepping Method : Adaptive
+ Courant Number : 4
+ End Time : 25
+ Save Interval : 0.2

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fireInRoom/run.png"><br>
</p>


## 11. 후처리

External tools의 paraivew 버튼을 클릭하여 실행한다. Coloring은 gas를 선택한다. Play를 누르면 시간에 따른 gas의 분포를 확인할 수 있다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/fireInRoom/contour.png"><br>
</p>

