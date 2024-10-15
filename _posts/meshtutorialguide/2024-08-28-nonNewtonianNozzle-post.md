---
layout: post
title: 16. Axi-symmetric Nozzle
category: mesh
---


# Axi-symmetric Nozzle

## * [형상 파일](https://drive.google.com/file/d/1mWnujK9XPQyt5gnSD0Z4cF3hP67tHVA1/view?usp=sharing) 

## 개요 

[![](https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/intro.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/blood/intro.png){:target="_blank"}

* 본 예제는 축대칭 노즐 해석을 위한 격자 생성 예제이다.
* 미국 식품의약청이 주관한 비뉴턴유체 시뮬레이션 검증을 위한 벤치마크 테스트 프로그램인 FDA's Nozzle Challenge에서 사용된 다음 논문에 있는 형상이다.

_Trias, Miquel, Antonio Arbona, Joan Massó, Borja Miñano, and Carles Bona. “FDA’s nozzle numerical simulation challenge: non-Newtonian fluid effects and blood damage.” PloS one 9, no. 3 (2014): e92638._  

* baramMesh를 실행하고 nonNewtonian_nozzle이라는 이름으로 project를 생성한다.

## 1. 형상정의 (Geometry)

형상은 주어진 fda-nozzle-scaled.stl 파일을 사용한다. 이 파일은 x-y 평면 상의 축대칭 면을 z 방향으로 extrude한 3차원 형상이다. baramMesh에서는 축대칭 형상의 격자를 직접 만드는 것이 아니라 3차원 격자를 만들고 그 중 하나의 면을 회전시켜(extrude) 축대칭 격자로 내보내는 방식을 사용한다.

하단 탭에서 Import - Select를 선택하고 stl 파일을 선택한다. 'Split Surface' 옵션을 선택하고 OK 버튼을 누르면 아래 그림의 오른쪽과 같은 창이 나타난다. 8개의 경계면이 만들어지는 것을 확인할 수 있다. OK 버튼을 클릭하면 형상을 불러온다.
[![](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/importSTL.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/importSTL.png){:target="_blank"}

stl 파일을 읽으면 zone0_suface, zone0_surface1, ...과 같이 번호가 매겨진 8개의 면을 확인할 수 있다. 각 면을 구분하기 위해 이름을 바꾸어 준다. 마우스 오른쪽 버튼으로 면을 선택하고 Edit/View를 클릭하여 Name을 원하는 이름으로 변경한다. Type은 디폴트인 Boundary를 그대로 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/changeName.png"  >
    <br> 
</p>

## 2. 영역정의(Region)

Region에서는 Fluid의 영역을 지정한다.

상단 (+)버튼을 클릭하면 아래 그림과 같이 변경된다. 디스플레이 창에서 마우스를 움직여 중앙점을 계산영역 내부에 위치시킨다. Add Region에서 Type을 Fluid로 그대로 두고 Add 버튼을 누르면 설정이 완료된다.

[![](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/region.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/region.png){:target="_blank"}



Next 버튼을 눌러 다음 단계로 넘어간다.


## 3. 배경격자(Base Grid)

Number of Cells per Direction에 (600 50 2)를 입력한다. snappyHexMesh는 최 외각 경계면으로 형상 파일을 사용하는 경우 한쪽 방향으로 1개의 격자를 사용할 수 없기 때문에 2개를 사용한다.

Generate 버튼을 누르면 Display Control에 boundary들이 생성되고 격자 모양을 확인할 수 있다.

[![](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/baseGrid.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/baseGrid.png){:target="_blank"}

Next 버튼을 눌러 다음 단계로 넘어간다.


## 4. 격자세분화(Castellation)

아무런 설정 변경 없이 Refine 버튼을 누른다. 완료되면 아래 그림과 같이 Display Control을 통해 격자를 확인할 수 있다.

[![](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/castel.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/castel.png){:target="_blank"}

작업이 완료되면 Next 버튼을 눌러 다음 단계로 넘어간다.


## 5. 형상구현(Snap)

아무런 설정 변경 없이 Snap 버튼을 누른다.

작업이 완료되면 Next 버튼을 눌러 다음 단계로 넘어간다.


## 6. 경계층격자(Boundary Layer)

Configurations의 (+) 버튼을 눌러 다음과 같이 설정한다.

+ Number of Layers : 5
+ Thickness Model Specification : First and Expansion
+ Size Specification : relative
+ First Layer Thickness : 0.15
+ Expansion Rate : 1.2
+ Min.Total Thickness : 0.3
+ Boundary : wall, wall1

[![](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/layer-setup.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/layer-setup.png){:target="_blank"}


나머지 설정은 디폴트를 사용하고 Start 버튼을 누른다. 완료되면 아래 그림과 같이 Display Control을 통해 격자를 확인할 수 있다.

[![](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/layer.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/layer.png){:target="_blank"}

Next 버튼을 눌러 다음 단계로 넘어간다.


## 7. 내보내기(Export)

축대칭 격자로 내보내기 위해 '2D Exports'에 있는 'Axi-Symmetry' 버튼을 클릭하면 다음과 같은 창이 열린다.

[![](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/export-setup.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/nonNewtonianNozzle/export-setup.png){:target="_blank"}

+ 경로와 이름을 설정한다.
+ Source Boundary에 back을 선택하고, Exposed Boundary는 front를 선택한다.
+ Axis Origin은 (0 0 0), Direction은 (-1 0 0)을 설정한다.

OK 버튼을 누르면 baramFlow에서 읽을 수 있는 폴더가 생성된다. 


마지막으로 cavityFlow이라는 이름으로 Export 하면 baramFlow v23에서 열 수 있는 Project 폴더, polyMesh 폴더 등이 생성된다.
