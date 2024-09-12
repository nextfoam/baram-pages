---
layout: post
title: 15. Sirocco Fan
category: _mesh
---


# Sirocco Fan

## * [형상 파일](https://drive.google.com/file/d/1SsLoBumVaTYTpb_X_yyStnzYwQs_x-8-/view?usp=sharing) 

## 개요 

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/intro.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/slidingMesh/intro.png){:target="_blank"}|

* 본 예제는 간단한 형상의 시로코팬의 격자를 BaramMesh로 생성하는 예제이다. 

* Sliding mesh로 계산하기 위해 회전체를 둘러싼 실린더가 있고 그 내부를 cell zone으로 설정한다. 

* baramMesh를 실행하고 siroccoFan이라는 이름으로 project를 생성한다.

## 1. 형상정의 (Geometry)

형상은 주어진 axis.stl, axis-r.stl, inlet.stl, outlet.stl, blades.stl, externalwalls.stl, interface.stl, walls.stl 8개의 파일을 사용한다.  

하단 탭에서 Import - Select를 선택하고 stl 파일들을 선택한다. 


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/importSTL.png"  >
    <br> import stl files
</p>


Cell zone을 만들기 위해 Add 버튼을 눌러 Cylinder를 선택한다. Type은 CellZone으로 선택하고 형상은 다음과 같이 설정한다.

+ Axis Point 1 : (0 0 -0.0169)
+ Axis Point 2 : (0 0 0.084)
+ Radius : 0.075

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/createCylinder.png"  >
    <br> Add cell zone geometry
</p>


Geometry에서 Cylinder_1_surface1 면을 마우스 오른쪽 버튼으로 선택하고 Edit/View를 눌러 Type을 None으로 바꾸어 준다.

Geometry에서 interface-stat 면을 마우스 오른쪽 버튼으로 선택하고 Edit/View를 눌러 Type을 interface - Non-Conformal로 바꾸어 준다. Slding mesh를 사용할 때 한쪽 interface 면이 움직이기 때문에 Non-Conformal로 지정해야 한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/interface.png"  >
    <br> Add cell zone geometry
</p>

Geometry의 최종 결과는 다음 그림과 같다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/geom1.png "Geometry 설정")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/geom1.png){:target="_blank"}|

Next 버튼을 눌러 다음 단계로 넘어간다.


## 2. 영역정의(Region)

Region에서는 Fluid의 영역을 지정한다.

상단 (+)버튼을 클릭하면 아래 그림과 같이 변경된다. 디스플레이 창에서 마우스를 움직여 중앙점을 계산영역 내부에 위치시킨다. Add Region에서 Type을 Fluid로 그대로 두고 Add 버튼을 누르면 설정이 완료된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/region.png"  >
    <br> Region 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.


## 3. 배경격자(Base Grid)

Number of Cells per Direction에 100, 50, 50를 입력하고 Generate 버튼을 누른다. Display Control에 boundary들이 생성되고 격자 모양을 확인할 수 있다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/baseGrid.png "base grid 설정")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/baseGrid.png){:target="_blank"}|


Next 버튼을 눌러 다음 단계로 넘어간다.



## 4. 격자세분화(Castellation)

### surface/Feature Refinement

(+)를 눌러 항목을 추가한다. interface-stat와 blades에 대해 다음과 같이 설정한다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/surfaceRefine.png "Surface/Feature Refinement 설정")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/surfaceRefine.png){:target="_blank"}|


### Volume Refinement

Volume Refinement는 따로 설정하지 않는다.



나머지 설정은 디폴트를 사용하고 Refine 버튼을 누른다. 완료되면 아래 그림과 같이 Display Control을 통해 격자를 확인할 수 있다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/refineResult.png "Refinement 결과")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/refineResult.png){:target="_blank"}|



작업이 완료되면 Next 버튼을 눌러 다음 단계로 넘어간다.



## 5. 형상구현(Snap)

Feature Snapping에서 Multi-Surface Feature Snap을 확성화한다. 나머지 설정은 디폴트를 사용하고 Snap 버튼을 누른다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/snap.png "Snap 결과")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/siroccoFan/snap.png){:target="_blank"}|



## 6. 경계층격자(Boundary Layer)

이 예제에서는 경계층격자를 만들지 않는다


Apply - Next 버튼을 눌러 다음 단계로 넘어간다.


## 7. 내보내기(Export)

마지막으로 siroccoFan_flow라는 이름으로 Export 하면 baramFlow에서 열 수 있는 Project 폴더가 생성된다.
