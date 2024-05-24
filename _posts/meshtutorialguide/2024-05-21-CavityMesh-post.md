---
layout: post
title: 10. 3D Cavity
category: mesh
---


# 3D Cavity

## * [형상 파일](https://drive.google.com/file/d/1eJMxycnNdELkT0YJRAqvojJDZTsTstOE/view?usp=sharing) 

## 개요 

* 본 예제는 3차원 천음속 Cavity 유동 해석을 위한 격자 생성 예제이다.

* 풍동 내부에 Cavity 모델이 있으며 다음 논문에 있는 형상이다.
  
  _Numerical Simulation of High-Speed Turbulent Cavity Flows, G.N.Barakos, S.J.Lawson, R.Steijil, P.Nayyar, Flow Turbulence Combust, 2009_

* baramMesh를 실행하고 3D_Cavity라는 이름으로 project를 생성한다.

## 1. 형상정의 (Geometry)

형상은 주어진 7개의 stl 파일을 사용한다. 하단 탭에서 Import - Select를 선택하고 7개의 stl 파일을 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cavity/cavity-importSTL.png"  >
    <br> import stl files
</p>

cavity 모델과 원방 경계면의 6개 면으로 구성된다. 전체와 각 면들의 이름을 다음 그림과 같이 바꾸어 준다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cavity/cavity-geom.png"  >
    <br> 형상
</p>

격자를 조밀하게 생성할 영역에 육면체를 만든다. Cavity 부분과 모델의 벽면 근처에 다음과 같이 2개의 Hex 형상을 만들고, 모든 속성을 None으로 설정한다.

+ Hex_1 : cavity 주변
  + min (1.75 1.1 -0.2), max (2.5 1.3 0.1)
+ Hex_2 : 모델 벽면 주변
  + min (1 1 0), max (3 1.5 0.05)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cavity/cavity-refineZone.png"  >
    <br> Refine 영역 생성
</p>

## 2. 영역정의(Region)

Region에서는 Fluid의 영역을 지정한다.

상단 (+)버튼을 클릭하면 아래 그림과 같이 변경된다. 디스플레이 창에서 마우스를 움직여 중앙점을 계산영역 내부에 위치시킨다. Add Region에서 Type을 Fluid로 그대로 두고 Add 버튼을 누르면 설정이 완료된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cavity/cavity-region.png"  >
    <br> Region 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.


## 3. 배경격자(Base Grid)

Number of Cells per Direction에 36, 24, 26을 사용해서 격자 크기를 0.1 정도로 만든다. Generate 버튼을 누르면 Display Control에 boundary들이 생성되고 격자 모양을 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cavity/cavity-baseGrid.png"  >
    <br> Region 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.


## 4. 격자세분화(Castellation)

### surface/Feature Refinement

(+)를 눌러 항목을 추가한다. cavity 모델인 wall에 대해 다음과 같이 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cavity/cavity-wall.png"  >
    <br> Surface/Feature Refinement 설정
</p>

### Volume Refinement

(+)를 눌러 항목을 추가한다. Hex_1은 레벨 5로, Hex_2는 레벨 4로 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cavity/cavity-hex1.png"  >
    <br> Volume Refinement of Hex_1
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cavity/cavity-hex2.png"  >
    <br> Volume Refinement of Hex_2
</p>

나머지 설정은 디폴트를 사용하고 Refine 버튼을 누른다. 완료되면 아래 그림과 같이 Display Control을 통해 격자를 확인할 수 있다.


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cavity/cavity-refine.png"  >
    <br> Refinement 
</p>


작업이 완료되면 Next 버튼을 눌러 다음 단계로 넘어간다.



## 5. 형상구현(Snap)

Feature Snapping의 Feature Snap Type을 implicit으로 설정한다. 나머지 설정은 디폴트를 사용하고 Snap 버튼을 누른다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cavity/cavity-snap.png"><br>
</p>

## 6. 경계층격자(Boundary Layer)

Configurations의 (+) 버튼을 눌러 다음과 같이 설정한다.

+ Number of Layers : 5
+ Thickness Model Specification : First and Expansion
+ Size Specification : relative
+ First Layer Thickness : 0.1
+ Expansion Rate : 1.2
+ Min.Total Thickness : 0.3
+ Boundary : wall

나머지 설정은 디폴트를 사용하고 Refine 버튼을 누른다. 완료되면 아래 그림과 같이 Display Control을 통해 격자를 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cavity/cavity-layer-setup.png"  >
    <br> layer 설정

나머지 설정은 디폴트를 사용하여 실행한다. 완료되면 아래 그림과 같이 Display Control을 통해 격자를 확인할 수 있다.


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cavity/cavity-layer.png"  >
    <br> 최종 격자

Apply - Next 버튼을 눌러 다음 단계로 넘어간다.


## 7. 내보내기(Export)

마지막으로 cavityFlow이라는 이름으로 Export 하면 baramFlow v23에서 열 수 있는 Project 폴더, polyMesh 폴더 등이 생성된다.<br>
