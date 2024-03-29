---
layout: post
title: 15. Rotating Fan in Room
category: tutorials
---

# Rotating Fan in Room

## 1. 개요 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/room/room-intro.png" ><br>
</p>

본 예제는 sliding mesh를 이용한 계산 예제이다.

실내에 100 RPM으로 회전하는 팬이 창을 통해 유동이 흐르는 간단한 문제이다.

계산 조건은 다음과 같다.

+ solver : buoyantSimpleNFoam (넥스트폼이 개발한 정상상태 비압축성 해석 솔버)
+ 난류 모델 : $Standard$ $k-\epsilon$
+ 팬 회전 속도 : 100 RPM  

## 2. 프로그램의 구동

BaramFlow 실행 후 launcher에서 ‘Open’을 선택하고 [격자 생성 튜토리얼](https://baramcfd.org/mesh/2024/03/21/fanInRoomMesh-post/)에서 만든 폴더를 선택한다(혹은 New Case를 선택하고 메뉴의 File - Load Mesh - OpenFOAM에서 \<caseName>/case/constant 폴더를 선택한다).

Launcher에서 ‘Solver Type’은 Pressure Based, ‘Multiphase Model’은 None, Gravity는 (0 0 0), ‘Species’는 Not Include를 선택한다.  
<br/>

## 3. General

비정상상태 등온 단상유동 계산이다. Time은 Transient로 설정하고, Gravity는 설정할 필요 없다. Operationg conditions는 디폴트 101325를 사용한다.

## 4. Models

난류 모델은 Standard $k-\epsilon$ 모델을 사용하고 나머지는 디폴트를 사용한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixer/3.3.png"><br> 난류 모델 설정
</p>

## 5. Materials

본 예제의 작동유체는 공기이다. 디폴트 값을 사용한다.

## 6. Cell Zone Conditions

cellZone의 AMI를 더블 클릭하면 설정 창이 열린다. Zone Type을 Sliding Mesh로 주고 다음과 같이 설정한다.

+ Rotating Speed : 100
+ Rotation Axis Origin : (-3 2 2.6)
+ Rotation Axis Direction : (0 0 1)

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/room/room-cellZone.png" >
    <br> Cell Zone설정
</p>

## 7. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ desk_surface_0, door, room : Wall - No Slip

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/room/room-noSlip.png" >
</p> 

+ fan_surface_0 : Wall - Moving Wall

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/room/room-movingWall.png" >
</p>

+ outlet : Pressure Outlet - Total Pressure = 0

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/room/room-outlet.png" >
</p>

+ AMI_surface_0, AMI_surface_0_slave : interface - Internal Interface

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/room/room-interface.png" >
</p>

전체 설정을 완료하면 아래 그림과 같이 된다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/room/room-bc.png" >
    <br> 경계조건 설정
</p>  

## 8. Numerical Conditions

본 예제에서는 아래와 같이 설정을 변경한다. 

+ Pressure-Velocity Coupling Scheme : SIMPLE

+ Use Momentum Predictor : On

+ Discretization Schemes
  * Time : First Order Implicit
  * Pressure : Linear
  * Momentum : Second Order Upwind
  * Turbulence : First Order Upwind

+ Under-Relaxation Factors : 모두 1로 설정

* Max Iteration per Time Step : 3

* Number of Correctors : 1

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/room/room-nume.png" >
    <br> 수치해석 조건 설정
</p>  

## 9. Initialization

초기값은 디폴트 값을 그대로 사용한다. 하단의 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 저장한다.

## 10. Run Conditions & Run

Run Conditions은 다음과 같이 설정한다.

+ Time Stepping Method : Adaptive
+ Couraant Number : 1
+ EndTime : 1
+ Save Interval : 0.02

Run에서 Start Calculation 버튼을 누르면 계산이 시작된다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/room/room-residual.png">
    <br> Residual plot
</p>  


