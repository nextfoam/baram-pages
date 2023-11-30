---
layout: post
title: 06. DrivAer
category: mesh
---

# DrivAer

## 1) 개요 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/drivAer/main.png"><br>
</p>

DrivAer는 자동차 공학 분야에서 사용되는 차량 외부 디자인 및 공기역학 테스트를 위한 실제 차량 모델로 차량의 외부 형태와 공기역학적 특성을 시뮬레이션하고 평가하기 위해 사용된다. 단순화된 모델과 매우 복잡한 양산차 사이의 격차를 줄이기 위해 도입된 모델이다. 

공개되어 있는 CAD 파일을 이용하여 BARAM에서 격자를 만들고 계산하여 풍동시험 결과와 비교하는 예제이다.

형상 파일은 아래의 링크된 페이지에서 Fastback, Smooth Underbody, with Mirrors, with Wheels에 해당하는 모델을 다운 받을 수 있다.(body_no_wheel.stl, Wheels_Front_Smooth.stl, Wheels_Rear_Smooth.stl)

https://www.epc.ed.tum.de/en/aer/research-groups/automotive/drivaer/geometry/


## 2) 형상 (Geometry)

형상은 차량, 앞바퀴, 뒤바퀴의 3개 stl 파일을 사용한다. 전체 영역 설정을 위한 Hex6와 차량 주위에 격자를 조밀하게 만들기 위해 3개의 Hex를 사용하여 다음 그림과 같이 구성한다. 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/drivAer/geom.png"><br> Geomerty 설정
</p>

Import 버튼을 클릭해서 body_no_wheel.stl, Wheels_Front_Smooth.stl, Wheels_Rear_Smooth.stl 파일을 선택한다.

Add 버튼을 클릭해서 전체 영역과 격자 조밀화를 위한 3개의 박스를 만들어준다. 

* far(전체영역) : 입구, 출구, 바닥 등의 경계를 구분하기 위해 Hex6로 생성

  + Type : None
  
  + Min./Max. : (-14 0 -0.3) / (30 4 6) 
  
  + 좌우 대칭이기 때문에 y 축으로 절반만 생성한다. z축의 최소값은 stl 파일의 최소값을 사용하면 바퀴의 원형과 바닥의 평면이 접하는 부분의 격자가 너무 나빠지기 때문에 조금 높게 잡아준다.

* refineBox1 : Hex로 생성

  + Type : None
  
  + Min./Max. : (-2 0 -0.3) / (15 2 2.5)
  
  + 생성하면 refineBox1_surface라는 면이 생성된다. 이것을 마우스 오른쪽 버튼으로 선택하고 Edit를 눌러 Type을 None으로 설정한다.
  
* refineBox2 : Hex로 생성

  + Type : None
  
  + Min./Max. : (-1 0 -0.3) / (7 1.2 1.5)

  + 생성하면 refineBox2_surface라는 면이 생성된다. 이것을 마우스 오른쪽 버튼으로 선택하고 Edit를 눌러 Type을 None으로 설정한다.
    
* refineBox3 : Hex로 생성

  + Type : None
  
  + Min./Max. : (3 0 -0.3) / (5 1 1)
  
  + 생성하면 refineBox3_surface라는 면이 생성된다. 이것을 마우스 오른쪽 버튼으로 선택하고 Edit를 눌러 Type을 None으로 설정한다.
  
Next 버튼을 눌러 다음 단계로 넘어간다.

## 3) 영역 (Region)

상단 (+) 버튼을 눌러 영역을 생성하고 그래픽 창에 연두색으로 나타나는 선의 교차점을 마우스로 이동하여 유체 영역에 위치시킨 후 Add 버튼을 클릭하면 설정이 완료된다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/drivAer/region.png"><br> Region 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.

## 4) 배경 격자 (Base Grid)

Use Hex6를 선택하고 격자수를 220, 20, 32로 설정한다. Generate 버튼을 누르면 배경 격자가 생성된다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/drivAer/baseGrid.png"><br> Base Grid 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.

## 5) Castellation

Configuration과 Advanced는 디폴트 설정을 사용한다.

Surface/Feature Refinement에서 바퀴와 차체에 격자 레벨을 각각 설정한다.

* wheel

  + Surface Refinement Level : 5
  
  + Feature Edge refinement Level : 1
  
  + Surfaces : Wheels_Front_Smooth_surface_0, Wheels_Rear_Smooth_surface_0

<p style="text-align: center">
     <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/drivAer/refineWheel.png"><br> wheel surface/feature level 설정
</p>
  
* body

  + Surface Refinement Level : 4
  
  + Feature Edge refinement Level : 5
  
  + Surfaces : body_no_wheel_surface_0

<p style="text-align: center">
     <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/drivAer/refineBody.png"><br> body surface/feature level 설정
</p>

Volume Refinement에서 refine box에 대한 격자 레벨을 각각 설정한다.

* refine1

  + Volume Refinement Level : 1
  
  + Volume : refineBox1
  
* refine2

  + Volume Refinement Level : 2
  
  + Volume : refineBox2
  
* refine3

  + Volume Refinement Level : 3
  
  + Volume : refineBox3

설정을 끝내면 화면은 다음과 같이 된다.

<p style="text-align: center">
     <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/drivAer/castell.png"><br> 격자 레벨 설정
</p>

Refine 버튼을 누르면 castellation이 진행된다. 메뉴의 Parallel 설정을 사용해서 병렬로 진행할 수 있다.

작업이 끝나면 Next 버튼을 눌러 다음 단계로 넘어간다.

## 6) Snap

디폴트 설정을 그대로 사용하고 Snap 버튼을 누른다.

작업이 끝나면 Next 버튼을 눌러 다음 단계로 넘어간다.

## 7) Boundary Layer

차량과 바퀴에 첫번째 경계층 높이는 0.001, expansion ratio는 1.2로 5개의 경계층 격자를 생성한다.

Configuration에서 (+)를 눌러 다음과 같이 설정한다.

<p style="text-align: center">
     <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/drivAer/blayer.png"><br> Boundary Layer Configuration
</p>

* Number of Layers : 4

* Thickness Model Specification : First and Expansion

* Size Specification : Absolute

* First Layer Thickness : 0.001

* Expansion Ratio : 1.2

* Min. thickness : 0.0001

* Boundary : body_no_wheel_surface_0, Wheels_Front_Smooth_surface_0, Wheels_Rear_Smooth_surface_0

Starting Analysis에서 Feature Angle Threshold를 60으로 설정한다. 

<p style="text-align: center">
     <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/drivAer/boundary.png"><br> Boundary Layer 설정
</p>

나머지는 디폴트 설정을 그대로 사용하고 Apply 버튼을 누른다.

작업이 끝나면 Next 버튼을 눌러 다음 단계로 넘어간다.

## 8) Export

마지막으로 drivAer라는 이름으로 Export 하면 baramFlow v23에서 열 수 있는 Project 폴더가 생성된다.

<p style="text-align: center">
     <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/drivAer/finalMesh.png"><br> 최종 격자
</p>

