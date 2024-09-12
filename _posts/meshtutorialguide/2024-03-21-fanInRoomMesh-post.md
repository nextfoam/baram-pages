---
layout: post
title: 09. Rotating Fan in Room
category: mesh
---


# Rotating Fan In Room

## * [형상 파일](https://drive.google.com/file/d/1R3UNNL2LdiWBOziU7s-_M1gecTOwwGz7/view?usp=sharing) 

## 개요 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/room/room-intro.png" ><br>
</p>

* 본 예제는 OpenFOAM의 pimpleFoam tutorial에 있는 rotatingFanInRoom의 격자를 BaramMesh로 생성하는 예제이다.

* 실내에 회전하는 팬이 있고 이것을 sliding mesh로 계산하기 위해 팬을 둘러싼 실린더가 있고 그 내부를 cell zone으로 설정한다. Cell zone을 둘러싼 면은 sliding mesh를 위해 같은 위치에 2개가 interface면으로 있어야 한다.

* baramMesh를 실행하고 fanInRoom이라는 이름으로 project를 생성한다.

## 1. 형상정의 (Geometry)

형상은 주어진 6개의 stl 파일을 사용한다. 하단 탭에서 Import - Select를 선택하고 6개의 stl 파일을 선택한다.


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/room/fanInRoom-importSTL.png"  >
    <br> import stl files
</p>

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/room/fanInRoom-geom.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/room/fanInRoom-geom.png){:target="_blank"}|

체적이 있는 AMI, desk, fan은 AMI_surface_0, desk_surface_0, fan_surface_0라는 면이 추가로 생성되었다.

### Geometry 속성 설정

필요한 항목을 마우스 오른쪽 버튼으로 선택하고 Edit를 누르면 설정창이 나타나다.

+ AMI : 내부를 Cell zone으로 만들기 위해 CellZone을 선택한다.
  + AMI_surface_0 : cell zone 외곽에 2개의 면을 만들기 위해 interface - Non-Conformal을 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/room/fanInRoom-cellZone.png"  >, <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/room/fanInRoom-interface.png"  >
    <br> AMI Geometry 속성 설정
</p>

+ 나머지는 디폴트로 설정한다.

Next 버튼을 눌러 다음 단계로 넘어간다.



## 2. 영역정의(Region)

Region에서는 Fluid의 영역을 지정한다.

상단 (+)버튼을 클릭하면 아래 그림과 같이 변경된다. 디스플레이 창에서 마우스를 움직여 중앙점을 계산영역 내부에 위치시킨다. Add Region에서 Type을 Fluid로 그대로 두고 Add 버튼을 누르면 설정이 완료된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/room/fanInRoom-region.png"  >
    <br> Region 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.


## 3. 배경격자(Base Grid)

Number of Cells per Direction에 65, 55, 30을 입력하고 Generate 버튼을 누른다. Display Control에 boundary들이 생성되고 격자 모양을 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/room/fanInRoom-baseGrid.png"  >
    <br> Region 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.



## 4. 격자세분화(Castellation)

fan과 AMI에 격자를 밀집시키기 위해 레벨 3을 사용하고 desk는 레벨 1을 사용한다. 나머지는 따로 설정하지 않고 디폴트인 0을 사용한다.

### surface/Feature Refinement

(+)를 눌러 항목을 추가한다. AMI, desk, fan, desk에 대해 다음과 같이 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/room/fanInRoom-ami.png"  >, <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/room/fanInRoom-desk.png"  >, <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/room/fanInRoom-fan.png"  >
    <br> Surface/Feature Refinement 설정
</p>

### Volume Refinement

(+)를 눌러 항목을 추가한다. AMI의 레벨을 3으로 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/room/fanInRoom-amiVol.png"  >
    <br> Volume Refinement 설정
</p>


나머지 설정은 디폴트를 사용하고 Refine 버튼을 누른다. 완료되면 아래 그림과 같이 Display Control을 통해 격자를 확인할 수 있다.


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/room/fanInRoom-refine.png"  >
    <br> Refinement 설정
</p>


작업이 완료되면 Next 버튼을 눌러 다음 단계로 넘어간다.



## 5. 형상구현(Snap)

Feature Snapping의 Feature Snap Type을 implicit으로 설정한다. 나머지 설정은 디폴트를 사용하고 Snap 버튼을 누른다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cavity/cavity-snap.png"><br>
</p>

## 6. 경계층격자(Boundary Layer)

경계층격자는 생성하지 않는다. 

Apply - Next 버튼을 눌러 다음 단계로 넘어간다.


## 7. 내보내기(Export)

마지막으로 fanInRoon이라는 이름으로 Export 하면 baramFlow v23에서 열 수 있는 Project 폴더, polyMesh 폴더 등이 생성된다.
