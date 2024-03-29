---
layout: post
title: 13. Porous Media
category: tutorials
---

# Porous Media

## 1. 개요 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/intro.png"><br> 형상 및 유동장
</p>

본 에제는 porous media 조건을 사용한 유동해석 예제이다. 상부 왼쪽에서 유동이 유입되고 porous 영역을 지나 아래로 유동이 흐르는 문제이다.(위 그림 왼쪽에서 파란색 부분이 porous 영역)

OpenFOAM의 porous media 모델은 porous 영역에서 불연속적인 속도 분포가 나타나고 압력손실도 입력 조건과 조금 다른 결과를 보이는 문제가 있다. 아래 그림의 왼쪽이 Baram-v23의 결과이며, 오른쪽이 OpenFOAM 2306의 standard 솔버를 사용한 결과이다. 

Baram이 사용하는 NextFOAM에서는 porous 영역에서 압력의 interpolation 방법을 개선하여 이 문제를 해결하였다(이에 대한 자세한 내용은 아래 링크의 문서를 참고). 결과의 정확성과 함께 수렴성도 많이 좋아진 것을 확인할 수 있다.

### * [Porous Media 참고 문헌](https://nextfoam.co.kr/proc/DownloadProc.php?fName=231101140051_yvpJhMF0nY.pdf&realfName=10thOKUCC_OpenFOAM%EC%82%AC%EC%86%8C%ED%95%9C%EB%AC%B8%EC%A0%9C%EB%93%A4.pdf)

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/res.png"><br> 결과 (좌)Baram v23, (우) openfoam 2306 standard solver
</p>

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/residual-1.png"><br> Residual (좌)Baram v23, (우) openfoam 2306 standard solver
</p>
<br/>

## 2. 프로그램의 구동

프로그램 실행 후 launcher에서 'Open'을 선택하고 격자 생성 튜토리얼에서 만든 porous 폴더를 선택한다(혹은 New Case를 선택하고 메뉴의 File - Load Mesh - OpenFOAM에서 porous/case/constant 폴더를 선택한다).

Launcher에서 'Flow Type'은 Incompressible, 'Multiphase Model'은 None, Gravity는 (0 0 0), 'Species'는 Not Include를 선택한다.


## 3. General

정상상태 계산이기 때문에 모든 설정은 디폴트 조건을 사용한다. 

## 4. Models

난류 모델은 standard $k-\epsilon$ 모델을 사용하고 나머지는 Default를 사용한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousMedia/turbulence.png"><br> Turbulence Model 설정
</p>
<br/>

## 5. Materials

디폴트 조건인 air를 사용한다.

## 6. Cell Zone Conditions

Cell Zone Conditions에는 region0에 porousZone이 있다. 이것을 더블 클릭하면 설정창이 열린다. Zone Type을 'Porous Zone'으로 선택하면 아래쪽에 세부 설정 부분이 나타나는데 다음과 같이 설정한다.

+ Model : Power Law
+ C0 : 5000
+ C1 : 1.9

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousMedia/cellZone.png"><br> Cell Zone Conditions 설정
</p>

## 7. Boundary Conditions

경계조건은 다음과 같이 설정한다.

+ inlet
    + type : Velocity Inlet
    + Velocity magnitude : 1
    + Turbulent Intensity : 1
    + Turbulent Viscosity Ratio : 10 
 
 <p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousMedia/inlet.png"><br> inlet 경계조건
 </p>

+ outlet
    + type : Pressure Outlet
    + Total Pressure : 0 
  
   <p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousMedia/outlet.png"><br> outlet 경계조건
   </p>

나머지는 모두 디폴트 조건인 wall을 사용한다.


## 8. Numerical Conditions

Convergence Criteria의 Pressure를 0.0001로 설정하고 나머지는 Default 조건을 사용한다.

## 9. Initialization

초기조건은 모두 디폴트 조건을 사용한다.

## 10. Run Conditions & Run

'Run Conditions'는 디폴트를 사용한다. 

병렬연산을 위해서는 메뉴의 Parallel을 실행하고 원하는 CPU 코어 개수를 입력한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousMedia/parallel.png"><br> 병렬연산 설정
</p>

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousMedia/residual.png"><br> 계산중인 화면
</p>

## 11. 후처리

External tools의 paraview 버튼을 클릭하여 paraview를 실행한다.

병렬연산인 경우 Case Type을 Decomposed Case로 변경한다.

<p style="text-align: left">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousMedia/slice.png"> Slice를 선택한다.
</p>

Pipeline Browser에서 Y Normal을 선택하고, Coloring을 U로 선택하면 다음과 같은 그림을 확인할 수 있다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/porousMedia/post.png"> <br> 중앙 단면의 속도 분포
</p>




