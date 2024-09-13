---
layout: post
title: 20. Non-Newtonian Blood Flow
category: tutorials
---

# 비뉴턴유체 혈관 유동 - FDA Nozzle 

### * [격자 파일 다운로드](https://drive.google.com/file/d/1fq6KLFt2mpidQchHwQ9j9mRgty5rlr3G/view?usp=sharing)

## 1. 개요 

|[![include surface's own gap](https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/intro.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/intro.png){:target="_blank"}|

‘FDA’s Nozzle Challenge’는 미국 식품의약청이 주관한 시뮬레이션 검증을 위한 벤치마크 테스트 프로그램이다. 이 프로그램에서 혈액 운반 의료기기의 특성을 반영하는 소형 노즐에 대한 실험 및 시뮬레이션 연구가 진행되었고, 관련 논문 중 Trias 등의 다음 논문을 참고했습니다.

_Trias, Miquel, Antonio Arbona, Joan Massó, Borja Miñano, and Carles Bona. “FDA’s nozzle numerical simulation challenge: non-Newtonian fluid effects and blood damage.” PloS one 9, no. 3 (2014): e92638._

노즐 목 직경을 기준으로 Reynolds number는 500이며, 비뉴턴유체 점성은 Carreau 모델을 사용합니다.

## 2. 프로그램의 구동 및 격자

프로그램 실행 후 launcher에서 'Open'을 선택하고 [격자 생성 튜토리얼](............)'에서 만든 폴더를 선택한다.(혹은 New Case를 선택하고 메뉴의 File-Load Mesh - OpenFOAM 에서 &lt;caseName&gt;/case/constant 폴더를 선택한다.

형상과 격자는 다음과 같다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/fda-diagram.png"><br>
</p>

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/fda-mesh.png"><br>
</p>

## 3. General

Time은 Steady를, Gravity는 (0 0 0)을 사용한다.

Operating Pressure는 101325를 사용한다.

## 4. Models

난류 모델은 Laminar를 사용하고 나머지는 디폴트를 사용한다.

## 5. Materials

Materials Configuration의 (+)를 클릭하여 waterLiquid를 추가한다. 

waterLiquid 편집창을 열고 다음과 같이 설정한다.

+ Name : blood
+ Density : 1056
+ Viscosity : Carreau

Carreau 옆의 Edit 버튼을 눌러 계수를 다음과 같이 입력한다.

+ Zero shear viscosity : 0.0001515
+ Infinite shear viscosity : 3.3144e-6
+ Relaxation time = 8,2
+ Power-law index = 0.2128
+ Linearity deviation, a = 0.64

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/material.png"><br>
</p>

## 6. Cell Zone Conditions

region0를 더블 클릭하면 설정창이 나타난다. Material을 blood로 선택한다.


## 7. Boundary Conditions

아래와 같이 경계면 타입과 경계값을 설정한다.

+ in : Velocity Inlet
  + Velocity magnitude : 0.04607

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/bc-in.png">
</p>

+ outlet : Pressure Outlet
  + Total Pressure : 0

+ wall, wall1, wall2 : Wall
  + Velocity : No Slip

+ back, front : Wedge


## 8. Numerical Conditions

Convergence Criteria에서 Pressure와 Momentum의 값을 1e-6으로 입력한다.

나머지는 모두 디폴트를 사용한다.

## 9. Initialization

초기조건은 다음과 같이 설정한다.

+ Velocity : (0.04607 0 0)
+ Pressure : 0

값을 입력하고 하단에 Initialize 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다.

## 10. Run Conditions & RUN

Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.

+ Number of Iterations : 2000
+ Save Interval : 500


계산이 완료되었을 때의 Residuals 그래프는 다음과 같다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/residual.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/residual.png){:target="_blank"}|


## 12. 후처리

External tools의 paraivew 버튼을 클릭하여 실행한다.

Coloring을 U로 선택한다.

축에서 속도 그래프를 확인하기 위해 Fileters 메뉴에서 'Plot Over Line'을 선택한다.

Line Parameters에서 Point1은 (-0.1 0 0.001), Point2는 (0.1 0 0.001)을 입력한다. 

X Axis Parameters에서 Use Index for XAxis를 비활성화하고, X Array Name은 Point_X를 선택한다.

Series Parameters에서 U_X를 선택하고 Apply 버튼을 누르면 아래와 같은 그래프를 확인할 수 있다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/paraview.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/paraview.png){:target="_blank"}|

File 메뉴의 'Save Data'를 실행하면, 축에서 속도를 데이터 파일로 얻을 수 있다. 아래 그림은 이 데이터를 실험결과와 점성을 상수로 준 경우의 결과와 비교하여 그린 것이다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/result.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/result.png){:target="_blank"}|

