---
layout: post
title: 10. Propeller
category: mesh
---


# Propeller

## * [형상 파일](https://drive.google.com/file/d/1Y0-PdoUDE6MFPLRlPVwE1Q54BMvOkn2N/view?usp=sharing) 

## 개요 

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/propeller/intro.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/propeller/intro.png){:target="_blank"}|

* 본 예제는 OpenFOAM의 pimpleFoam tutorial에 있는 propeller의 격자를 BaramMesh로 생성하는 예제이다.

* Sliding mesh로 계산하기 위해 프로펠러를 둘러싼 실린더가 있고 그 내부를 cell zone으로 설정한다. Cell zone을 둘러싼 면은 sliding mesh를 위해 같은 위치에 2개가 interface면으로 있어야 한다.

* baramMesh를 실행하고 propeller라는 이름으로 project를 생성한다.

## 1. 형상정의 (Geometry)

형상은 주어진 propeller.stl, propelerStem.stl, far.stl 3개의 파일을 사용한다. far.stl은 원방경계를 위한 실린더인데 유동의 입출구가 구문되어 있지 않기 때문에 읽을 때 경계면을 분리해 주어야 한다. 

하단 탭에서 Import - Select를 선택하고 propeller.stl, propellerStem.stl 파일을 선택한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/importSTL.png"  >
    <br> import stl files
</p>

하단 탭에서 Import - Select를 선택하고 far.stl,파일을 선택한다. Split Surface 옵션을 활성화한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/importSTL1.png"  >
    <br> import stl files
</p>

Feature Angle이 디폴트인 60인 상태에서 입구, 출구, 원방경계의 3개로 나누어지는 것을 확인할 수 있다. OK 버튼을 누른다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/importSTL2.png"  >
    <br> split surface
</p>

Geometry에서 far_surface 면을 마우스 오른쪽 버튼으로 선택하고 Edit/View를 눌러 이름을 far로 바꾸어 준다.

Geometry에서 far_surface1 면을 마우스 오른쪽 버튼으로 선택하고 Edit/View를 눌러 이름을 inlet으로 바꾸어 준다.

Geometry에서 far_surface2 면을 마우스 오른쪽 버튼으로 선택하고 Edit/View를 눌러 이름을 outlet으로 바꾸어 준다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/geom.png"  >
    <br> 프로펠러와 원방경계 형상
</p>

Sliding mesh를 위한 cell zone을 만들기 위해 Add 버튼을 눌러 실린더를 만든다. Cylinder를 선택하고 다음과 같이 설정한다.

+ Name : cellZone
+ Type : CellZone
+ Cylinder Geometry
  + Axis Point1 : (-0.06 0 0)
  + Axis Point2 : (0.08 0 0) 
+ Radius : 0.12

Geometry에서 cellZone_surface 면을 마우스 오른쪽 버튼으로 선택하고 Edit/View를 눌러 Type을 Interface - Non-Conformal로 바꾸어 준다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/cellZone.png"  >
    <br> Add cell zone geometry
</p>

Local refinement를 위한 영역을 만들기 위해 Add 버튼을 눌러 실린더를 만든다. Cylinder를 선택하고 다음과 같이 설정한다.

+ Name : refine
+ Type : None
+ Cylinder Geometry
  + Axis Point1 : (-0.1 0 0)
  + Axis Point2 : (0.6 0 0) 
+ Radius : 0.16


Geometry에서 cellZone_surface 면을 마우스 오른쪽 버튼으로 선택하고 Edit/View를 눌러 Type을 None으로 바꾸어 준다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/refine.png"  >
    <br> Add refine region geometry
</p>

Geometry의 최종 결과는 다음 그밀과 같다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/geom1.png"  >
    <br> 최종 형상
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.


## 2. 영역정의(Region)

Region에서는 Fluid의 영역을 지정한다.

상단 (+)버튼을 클릭하면 아래 그림과 같이 변경된다. 디스플레이 창에서 마우스를 움직여 중앙점을 계산영역 내부에 위치시킨다. Add Region에서 Type을 Fluid로 그대로 두고 Add 버튼을 누르면 설정이 완료된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/region.png"  >
    <br> Region 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.


## 3. 배경격자(Base Grid)

Number of Cells per Direction에 20, 12, 12를 입력하고 Generate 버튼을 누른다. Display Control에 boundary들이 생성되고 격자 모양을 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/baseGrid.png"  >
    <br> base grid 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.



## 4. 격자세분화(Castellation)

propeller에는 레벨 4~6을, stem에는 레벨 4를, cellZone에는 레벨 4를, refine 영역에는 레벨 3을 사용한다.

### surface/Feature Refinement

(+)를 눌러 항목을 추가한다. propeller, stem, cellZone_surface, refine_surface에 대해 다음과 같이 설정한다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/surfaceRefine.png "Surface/Feature Refinement 설정")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/surfaceRefine.png){:target="_blank"}|


### Volume Refinement

(+)를 눌러 항목을 추가한다. cellZone과 refine의 레벨을 4와 3으로 설정한다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/volumeRefine.png "Volume Refinement 설정")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/volumeRefine.png){:target="_blank"}|



나머지 설정은 디폴트를 사용하고 Refine 버튼을 누른다. 완료되면 아래 그림과 같이 Display Control을 통해 격자를 확인할 수 있다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/refineResult.png "Refinement 결과")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/refineResult.png){:target="_blank"}|



작업이 완료되면 Next 버튼을 눌러 다음 단계로 넘어간다.



## 5. 형상구현(Snap)

Feature Snapping의 Feature Snap Type을 implicit으로 설정한다. 나머지 설정은 디폴트를 사용하고 Snap 버튼을 누른다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/snap.png "Snap 결과")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/snap.png){:target="_blank"}|



## 6. 경계층격자(Boundary Layer)

propeller와 stem에 경계층 격자를 만든다. Configuration은 다음과 같이 설정한다.

+ Number of Layers : 3
+ Thickness Model Specification : First and Expansion
+ Size Specification : Relative
+ First Layer Thickness : 0.1
+ Expansion Ratio : 1.2
+ Min. Total Thickness : 0.2
+ Boundary : propeller, propellerStem

Advanced Configuration의 Static Analysis of Starting Mesh의 Feature Angle Threshold를 60으로 설정한다. 나머지는 디폴트 값을 사용한다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/layer.png "Boundary Layer 설정")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/propeller/layer.png){:target="_blank"}|


Apply - Next 버튼을 눌러 다음 단계로 넘어간다.


## 7. 내보내기(Export)

마지막으로 propeller_flow라는 이름으로 Export 하면 baramFlow v23에서 열 수 있는 Project 폴더가 생성된다.
