---
layout: post
title: 11. Gap Refinement
category: mesh
---


# Gap Refinement

## * [형상 파일 다운로드](https://drive.google.com/file/d/1aNHAqI2Ab7C0sDQgrjo5Nc2gRofLCCyZ/view?usp=sharing) 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/intro.png"  >
    <br> import한 형상
</p>

## 개요 

본 예제는 BARAM-v24.2에 추가된 Gap Refinement의 기능에 대한 이해를 돕기 위한 것이다.

Gap Refinement에는 'Min. Cell Layers in a gap', 'Gap Detection Start Level', 'Max. Refinement Level', 'Direction', 'Include surface's own gap' 등의 입력 및 옵션이 있다. 이것들의 설정에 따라 격자가 어떻게 생성되는지 알아본다.

* baramMesh를 실행하고 gapRefinement라는 이름으로 project를 생성한다.

## 1. 형상정의 (Geometry)

형상은 주어진 hex_with_self_gap.stl 파일과 baramMesh에서 구와 육면체를 만들어서 사용한다.

하단 탭에서 Import - Select를 선택하고 hex_with_self_gap.stl 파일을 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/geom.png"  >
    <br> import한 형상
</p>

### Geometry 생성

+ 구 생성 : Add 버튼을 눌러 창이 나타나면 Sphere를 선택한다. 중심점은 (0 6.5 0)을 입력하고 반경은 2를 입력한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/sphere.png"  >
    <br> 구 생성
</p>

+ 육면체 생성 : Add 버튼을 눌러 창이 나타나면 Hex를 선택한다. 최소, 최대 좌표는 (-9 9 -2), (10 9.5 2)를 입력한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/hex.png"  >
    <br> 육면체 생성
</p>

+ 원방 경계면 생성 : Add 버튼을 눌러 창이 나타나면 Hex6를 선택한다. 최소, 최대 좌표는 (-20 -10 -5), (20 16 5)를 입력한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/hex6.png"  >
    <br> 원방경계면 생성
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/fullGeom.png"  >
    <br> 완성된 형상
</p>


## 2. 영역정의(Region)

Region에서는 Fluid의 영역을 지정한다.

상단 (+)버튼을 클릭하면 아래 그림과 같이 변경된다. 디스플레이 창에서 마우스를 움직여 중앙점을 계산영역 내부에 위치시킨다. Add Region에서 Type을 Fluid로 그대로 두고 Add 버튼을 누르면 설정이 완료된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/region.png"  >
    <br> Region 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.


## 3. 배경격자(Base Grid)

Number of Cells per Direction에 20, 13, 5를 입력하고 Generate 버튼을 누른다. Display Control에 boundary들이 생성되고 격자 모양을 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/baseGrid.png"  >
    <br> Base Grid
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.



## 4. 격자세분화(Castellation)

Volume Refinement만 설정한다.

전체 영역의 레벨을 1로 주고 Gap Refinement를 활성화 한다. 다음과 같이 설정한다.

+ Volume Refinement Level : 1
+ Gap Refinement : on
  + Min. Cell Layers in gap : 4
  + Gap Detection Start Level : 1
  + Max. Refinement Level : 4
  + Direction : Mixed
  + Include surface's own gap : on
+ Volume : Hex6_1

사이즈 레벨이 1인 크기(여기서는 1)보다 작은 영역을 gap으로 판단하고 여기에 최소 4개의 격자가 들어가게 한다는 것이다. 최고 레벨은 4로 주었기 때문에 레벨이 4일 때도 4개 이상이 들어가지 않더라도 더이상 분할하지 않고, 방향은 inside와 outside 모두 적용하고, 자신의 면에 의한 gap도 포함한다는 설정이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/castel1.png"  >
    <br> Base Grid
</p>

나머지 설정은 디폴트를 사용하고 Refine 버튼을 누른다. 완료되면 아래 그림과 같이 Display Control을 통해 격자를 확인할 수 있다.


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/refine.png"  >
    <br> Refinement 설정
</p>


작업이 완료되면 Next 버튼을 눌러 다음 단계로 넘어간다.



## 5. 형상구현(Snap)

Feature Snapping의 Feature Snap Type을 implicit으로 설정한다. 나머지 설정은 디폴트를 사용하고 Snap 버튼을 누른다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/snap.png"><br>
</p>




## Gap Refinement 설정 변경의 영향

Gap Refinement의 입력변수와 옵션을 바꿔서 격자를 만들어 본다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/gaps.png"  >
    <br> Base Grid
</p>

### Gap Detection Start Level의 영향

Gap Refinement의 기본 조건에서 Gap Detection Start Level을 2로 바꾸면 결과는 다음과 같다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/gap-detect.png"><br>
</p>

Gap의 크기가 사이즈 레벨 2보다 크기 때문에 아무런 refine이 되지 않는다.

### Gap Direction의 영향

Gap Direction을 inside와 outside로 바꾸면 결과는 다음과 같다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/gap-direction.png"><br>
</p>

### Include surface's own gap의 영향

이 옵션에 따른 영향은 다음과 같다

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/gap/gap-self.png"><br>
</p>

