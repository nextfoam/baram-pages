---
layout: post
title: 05. Sirocco Fan - Sliding mesh
category: tutorials
---

# Sirocco Fan 

### * [격자 파일 다운로드](https://drive.google.com/file/d/1ziOkgB3Uv9I3V8o9oRJnribBkTqKcR93/view?usp=sharing)

## 1. 개요 

|[![격자 및 압력분포](https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.1.png "격자 및 압력분포")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.1.png){:target="_blank"}|

본 예제는 비정상상태 비압축성 유동해석 예제이다. 시로코팬 내부에서 입펠러가 회전할 때 내부의 유동을 예측하는 문제이다.

격자는 Ansys Fluent의 .cas 형식의 파일을 변환하여 사용한다.

계산 조건은 다음과 같다. 

+ solver : buoyantPimpleNFoam (넥스트폼이 개발한 동적격자 비압축성 유동 해석 솔버)
+ 난류 모델 : $Standard$ $k-\epsilon$ model
+ 밀도 : 1.225 $kg/m^3$
+ 점성 계수 : 1.79e-5 $kg/ms$
+ 임펠러 회전 수 : 2,000 RPM

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 ‘New’를 선택한다. Launcher에서 ‘Solver Type’은 Pressure-based를, ‘Multiphase Model’은 None, ‘Species’는 Not Include를 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixingPipe/launcher.png"><br>
</p>

## 3. 격자

격자는 주어진 Ansys의 .cas 파일을 활용한다. 상단 탭에서 File - Load Mesh - Fluent (ASCII)를 클릭하고 siroccofan.cas 파일을 선택한다. 

## 4. General

Time을 Transient로 변경한다. 나머지는 Default로 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.2.png"><br>
</p>

## 5. Models

난류 모델은 $Standard$ $k-\epsilon$ 모델을 사용하고 나머지는 Default를 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.3.png"><br>
</p>

## 6. Materials

본 예제에서 작동 유체는 공기이다. 유체의 물성치는 Default 조건을 사용한다.

## 7. Cell Zone Conditions

Cell Zone Conditions에서는 MRF, Sliding Mesh, Source 등을 설정할 수 있다. 본 예제에서는 'rotating' Cell Zone에 Sliding Mesh 조건을 설정한다.

Sliding Mesh를 선택하고 아래 값들을 입력한다.

+ Sliding Mesh
    + Rotating Speed : 2,000(RPM)
    + Rotation-Axis Origin : (0, 0, 0)
    + Rotation-Axis Direction : (0, 0, 1)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.4.png"><br>
</p>

## 8. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ interface-stat와 interface-rotating은 회전 경계면이다.

+ interface-stat, interface-rotating : Interface - Internal Interface
    + interface-stat : Internal Interface로 변경 후, Coupled Boundary는 interface-rotating 선택

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.5.png"><br>
</p>

+ axis : Wall
    + Velocity Condition : Rotational Moving Wall
    + Speed : 2000 (RPM)
    + Rotation-Axis Origin : 0 0 0
    + Rotation-Axis Direction : 0 0 1

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.6.png"><br>
</p>

+ axis-r, blades : Wall
    + Velocity Condition : Moving Wall

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.7.png"><br>
</p>

+ externalwalls, walls : Wall
    + Velocity Condition : No Slip

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.8.png"><br>
</p>

+ inlet : Velocity Inlet
    + Velocity Specification Method : Magnitudde, Normal to Boundary
    + Profile Type : Constant
    + Velocity Magnitude : 1 (m/s)
    + Turbulent Intensity : 1 (%)
    + Turbulent Viscosity Ratio : 10

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.9.png"><br>
</p>

+ outlet : Pressure Outlet
    + Total Pressure : 0 (Pa)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.10.png"><br>
</p>

## 9. Numerical Conditions

본 예제에서는 Default 조건을 사용한다.

## 10. Initialization

모두 Defalut 값을 사용한다.

하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.11.png"><br>
</p>

## 11. Run

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Time Stepping Method : Fixed
+ Time Step Size : 0.0001
+ End Time : 0.3
+ Data Write Format : Binary
+ 메뉴의 Parallel - Environment를 선택하고 Number of Cores는 4, Parallel Type은 Local Machine을 선택

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.12.png"><br>
</p>

아래 그림은 계산중인 Residuals 그래프이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.13.png"><br>
</p>

## 12. 후처리

Fan 내부의 압력 분포를 확인해본다. External tools의 paraivew 버튼을 클릭하여 paraview를 실행한다.

Case Type을 Decomposed Case로 변경한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.14.png"><br>
</p>

Slice 기능을 활용하여 용기 내부의 단면을 자른다.

Z-normal 버튼을 클릭 후, Origin을 다음과 같이 변경한다.

+ Origin : 0.06 -0.017 0.05
+ Normal : 0 0 1

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.15.png"><br>
</p>

아래 그림과 같이 fan 내부 속도 분포가 나오게 된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/4.16.png"><br>
</p>
