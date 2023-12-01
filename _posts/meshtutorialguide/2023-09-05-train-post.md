---
layout: post
title: 08. High Speed Train
category: mesh
---

# 고속열차

## 1) 개요 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/train/intro.png"><br>
</p>

고속열차는 마하수가 0.3~0.4 범위의 아음속 압축성 유동 영역에서 주행한다. CFD에서 저속 유동에서는 SIMPLE 게열의 압력기반 솔버를, 고속유동에서는 밀도기반의 솔버를 많이 사용한다. Baram의 비압축성 솔버인 buoyantSimpleNFoam의 아음속 압축성 유동영역에서 솔버의 안정성을 검증하기 위한 에제이다.

차량 연결부, 대차(바퀴), 판토그라프를 단순화한 고속철도 모델을 사용하였으며, 열차의 속도는 400 km/h이다. 

약 200만개 정도의 격자로 300번 정도의 iteration만에(8 코어 CPU에서 20분 정도에) 수렴된 결과를 얻을 수 있었다. OpenFOAM의 표준솔버인 buoyantSimpleFoam과 rhoSimpleFoam을 사용하여 해석한 결과와 비교했을 때 훨씬 뛰어난 수렴성을 보여준다.

격자 생성을 위한 형상 파일은 아래의 링크에서 다운 받을 수 있다.

### * [형상 파일 링크](https://drive.google.com/file/d/1r9S6y9TAx7m2eyg59KGejgYFvIazv1Px/view?usp=sharing) 


## 2) 형상 (Geometry)

차량은 stl 파일을 사용한다. 전체 영역 설정을 위한 Hex6와 차량 주위에 격자를 조밀하게 만들기 위해 하나의 Hex를 사용하여 다음 그림과 같이 구성한다. 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/train/geom.png"><br> Geomerty 설정
</p>

Import 버튼을 클릭해서 train.stl 파일을 선택한다.

Add 버튼을 클릭해서 전체 영역과 격자 조밀화를 위한 박스를 만들어준다. 

* far(전체영역) : 입구, 출구, 바닥 등의 경계를 구분하기 위해 Hex6로 생성

  + Type : None
  
  + Min./Max. : (-75 -40 0) / (260 0 40) 
  
  + 좌우 대칭이기 때문에 y 축으로 절반만 생성한다. 

  + 각 면의 이름을 inlet(xMin), outlet(xMax), side(yMin), symmetry(yMax), ground(zMin), top(zMax)으로 바꿔준다.

  <p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/train/far.png"><br> far 설정
</p>

* refine box : Hex로 생성

  + Type : None
  
  + Min./Max. : (-18 -5 0) / (100 5 7)
  
  + 생성하면 Hex_1_surface라는 면이 생성된다. 이것을 마우스 오른쪽 버튼으로 선택하고 Edit를 눌러 Type을 None으로 설정한다.

  <p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/train/hex.png"><br> Refinement Box 설정
</p>
   
Next 버튼을 눌러 다음 단계로 넘어간다.

## 3) 영역 (Region)

상단 (+) 버튼을 눌러 영역을 생성하고 그래픽 창에 연두색으로 나타나는 선의 교차점을 마우스로 이동하여 유체 영역에 위치시킨 후 Add 버튼을 클릭하면 설정이 완료된다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/train/region.png"><br> Region 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.

## 4) 배경 격자 (Base Grid)

Use Hex6를 선택하고 격자수를 100, 20, 20으로 설정한다. Generate 버튼을 누르면 배경 격자가 생성된다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/train/baseGrid.png"><br> Base Grid 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.

## 5) Castellation

Configuration과 Advanced는 디폴트 설정을 사용한다.

Surface/Feature Refinement에서 차량의 격자 레벨을 설정한다.

* 차량

  + Surface Refinement Level : 5
  
  + Feature Edge refinement Level : 5
  
  + Surfaces : train_surface_0

<p style="text-align: center">
     <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/train/refineTrain.png"><br> 차량 surface/feature level 설정
</p>

Volume Refinement에서 refine box에 대한 격자 레벨을 각각 설정한다.

* Volume

  + Volume Refinement Level : 4 
 
  + Volume : Hex_1

<p style="text-align: center">
     <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/train/refineVolume.png"><br> Volume level 설정
</p>

설정을 끝내면 화면은 다음과 같이 된다.

<p style="text-align: center">
     <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/train/castell.png"><br> 격자 레벨 설정
</p>

Refine 버튼을 누르면 castellation이 진행된다. 메뉴의 Parallel 설정을 사용해서 병렬로 진행할 수 있다.

작업이 끝나면 Next 버튼을 눌러 다음 단계로 넘어간다.

## 6) Snap

디폴트 설정을 그대로 사용하고 Snap 버튼을 누른다.

작업이 끝나면 Next 버튼을 눌러 다음 단계로 넘어간다.

## 7) Boundary Layer

Configuration에서 (+)를 눌러 다음과 같이 설정한다.

<p style="text-align: center">
     <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/train/blayer.png"><br> Boundary Layer Configuration
</p>

* Number of Layers : 5

* Thickness Model Specification : First and Expansion

* Size Specification : Relative

* First Layer Thickness : 0.3

* Expansion Ratio : 1.2

* Min. thickness : 0.1

* Boundary : train_surface_0

Starting Analysis에서 Feature Angle Threshold를 60으로 설정한다. 

<p style="text-align: center">
     <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/train/boundary.png"><br> Boundary Layer 설정
</p>

나머지는 디폴트 설정을 그대로 사용하고 Apply 버튼을 누른다.

작업이 끝나면 Next 버튼을 눌러 다음 단계로 넘어간다.

## 8) Export

마지막으로 train이라는 이름으로 Export 하면 baramFlow v23에서 열 수 있는 Project 폴더가 생성된다.

<p style="text-align: center">
     <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/train/finalMesh.png"><br> 최종 격자
</p>

