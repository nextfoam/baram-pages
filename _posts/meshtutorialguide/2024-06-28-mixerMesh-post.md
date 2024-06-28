---
layout: post
title: 13. Mixer
category: mesh
---


# Mexer - baffle, periodic, cell zone

## * [형상 파일](https://drive.google.com/file/d/1K_DUBphQi3Xqhy7E7dTtYR-s_D46DmZQ/view?usp=sharing) 

## 개요 

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixer/intro.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mixer/intro.png){:target="_blank"}|

* 본 예제는 단순한 형상의 믹서 격자 생성 예제이다. MRF를 이용하여 정상상태 계산을 할 것이다. 유동의 입출구는 없으며, 전체 형상의 1/4만 모델링하여 회전 주기조건을 사용할 것이다. 임펠러는 두께가 없는 평면(baffle)로 처리한다.

* 형상 파일을 다운로드 하고 압축을 풀면 믹서의 형상(mixer.stl)과 cell zone 형상(cellZone.stl) 파일이 있다. 

* baramMesh를 실행하고 mixerMesh라는 이름으로 project를 생성한다.

## 1. 형상정의 (Geometry)

형상은 주어진 mixer.stl, cellZone.stl 2개의 파일을 사용한다. 하단 탭에서 Import - Select를 선택하고 2개의 파일을 선택한다. 


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/importSTL.png"  >
    <br> import stl files
</p>

mixer.stl 파일은 wall, hub, hub_rot, impeller, periodic1, periodic2, top 등의 7개의 솔리드로 구성되어 있다. 

Geometry에서 cellZone을 마우스 오른쪽 버튼으로 선택하고 Edit/View를 눌러 Type을 CellZone으로 바꾸어 준다.

Geometry에서 cellZone_surface를 마우스 오른쪽 버튼으로 선택하고 Edit/View를 눌러 Type을 None으로 바꾸어 준다.

Geometry에서 impeller를 마우스 오른쪽 버튼으로 선택하고 Edit/View를 눌러 Type을 interface로 바꾸어 준다.(Non-Conformal, Inter-Region은 활성화하지 않는다)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/geom.png"  >
    <br> Geometry 설정
</p>


Next 버튼을 눌러 다음 단계로 넘어간다.


## 2. 영역정의(Region)

Region에서는 Fluid의 영역을 지정한다.

상단 (+)버튼을 클릭하면 아래 그림과 같이 변경된다. 디스플레이 창에서 마우스를 움직여 중앙점을 계산영역 내부에 위치시킨다. Add Region에서 Type을 Fluid로 그대로 두고 Add 버튼을 누르면 설정이 완료된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/region.png"  >
    <br> Region 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.


## 3. 배경격자(Base Grid)

Number of Cells per Direction에 60, 40, 80을 입력하고 Generate 버튼을 누른다. Display Control에 boundary들이 생성되고 격자 모양을 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/baseGrid.png"  >
    <br> base grid 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.



## 4. 격자세분화(Castellation)

cellZone에는 레벨 1을, hub, hub_rot, impeller에는 레벨 2를 사용한다.

### surface/Feature Refinement

(+)를 눌러 항목을 추가한다. hub, hub_rot, impeller에 대해 다음과 같이 설정한다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/surfaceRefine.png "Surface/Feature Refinement 설정")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/surfaceRefine.png){:target="_blank"}|


### Volume Refinement

(+)를 눌러 항목을 추가한다. cellZone의 레벨을 1로 설정한다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/volumeRefine.png "Volume Refinement 설정")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/volumeRefine.png){:target="_blank"}|


Configuration의 Keep Non-Manifold Edges를 활성화한다.

나머지 설정은 디폴트를 사용하고 Refine 버튼을 누른다. 완료되면 아래 그림과 같이 Display Control을 통해 격자를 확인할 수 있다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/refineResult.png "Refinement 결과")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/refineResult.png){:target="_blank"}|


작업이 완료되면 Next 버튼을 눌러 다음 단계로 넘어간다.


## 5. 형상구현(Snap)

Iteration Count의 Smoothing for Surface와 Smoothing for Internal을 모두 0으로 설정한다. 형상이 단순하고 성긴 격자를 사용할 때 smoothing은 형상의 왜곡을 가져올 수 있어 사용하지 않는 것이 좋을 때가 있다.


나머지 설정은 디폴트를 사용하고 Snap 버튼을 누른다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/snap.png "Snap 결과")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/snap.png){:target="_blank"}|



## 6. 경계층격자(Boundary Layer)

wall, hub, hub_rot, impeller, impeller_slave에 경계층 격자를 만든다. Configuration은 다음과 같이 설정한다.

+ Number of Layers : 3
+ Thickness Model Specification : First and Expansion
+ Size Specification : Relative
+ First Layer Thickness : 0.1
+ Expansion Ratio : 1.2
+ Min. Total Thickness : 0.2
+ Boundary : wall, hub, hub_rot, impeller, impeller_slave

Advanced Configuration은 다음과 같이 설정한다.

+ Static Analysis of Starting Mesh의 Feature Angle Threshold : 60
+ Patch Displacement Smoothing의 Number of Iteration과 Smooth Layer Thickness : 0 
+ 나머지는 디폴트 값을 사용한다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/layer.png "Boundary Layer 설정")](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixer/layer.png){:target="_blank"}|


Apply - Next 버튼을 눌러 다음 단계로 넘어간다.


## 7. 내보내기(Export)

마지막으로 mexer_flow라는 이름으로 Export 하면 baramFlow에서 열 수 있는 Project 폴더가 생성된다.
