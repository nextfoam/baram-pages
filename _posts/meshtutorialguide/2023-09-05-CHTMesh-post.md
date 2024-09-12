---
layout: post
title: 04. CHT
category: _mesh
---

# 개요

고체의 열전도를 포함한 열전달 해석을 위한 multi-region 격자 생성 예제이다.

2차원 모델이며 원형의 유체 영역을 사각형의 고체 영역이 둘러싸고 있다. 유체 영역에 회전하는 막대가 있으며 MRF를 사용하기 위해 cell zone이 있다. 

모델의 구조는 다음과 같다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cht/hotBar.png"><br> 형상
</p>

baramMesh를 실행하고 'CHD-2d-Mesh'라는 이름으로 프로젝트를 생성한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cht/createProject.png"><br> 프로젝트 생성
</p>

# Geometry

형상은 전체 영역인 육면체, 유체 영역인 실린더, cell zone인 실린더, 막대인 육면체의 4개로 구성되는데, Add 버튼을 눌러 하나씩 만든다. 회전하는 막대 중심의 좌표가 (0 0 0)이 되로록 만든다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cht/first.png"><br> Geometry
</p>

## 전체 영역

전체 영역인 육면체는 Hex6(6 Sub-Surfaces)를 이용해서 만든다.

Type은 None이다. Min. 포인트의 좌표는 (-7 -5 0)이고 Max. 포인트의 좌표는 (7 9 0.1)이다.

생성하면 geometry 네비게이션에 Hex6_1와 6개의 면(xMin , xMax, yMin, yMax, zMin, zMax)이 만들어 진다. 이 6개의 면이 경계면이 된다. 각 면을 선택하고 마우스 오른쪽 버튼을 클릭해서 Edit를 눌러 이름을 다음과 같이 바꿔준다. 2차원 격자이기 때문에 zMin, zMax면은 2차원 경계조건인 empty를 사용할 것이다.

* Hex6_1_xMin : left

* Hex6_1_xMax : right

* Hex6_1_yMin : bottom

* Hex6_1_yMax : top

* Hex6_1_zMin : empty_down

* Hex6_1_zMax : empty_up

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cht/allDomain.png"><br> 전체 영역 형상 생성
</p>

## 막대

회전하는 막대는 육면체(Hex)를 이용해서 만든다.

Type은 None이다. Min. 포인트의 좌표는 (-0.1 -1.2 0)이고 Max. 포인트의 좌표는 (0.1 1.2 0.1)이다.

생성하면 geometry 네비게이션에 Hex_1 과 1개의 면(Hex_1_surface)가 만들어 진다. 이 면을 선택하고 마우스 오른쪽 버튼을 클릭해서 Edit를 눌러 이름을 inner_wall로 바꿔준다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cht/bar.png"><br> 막대 형상 생성
</p>

## 회전하는 cell zone

회전하는 cell zone은 Cylinder를 이용해서 만든다.

Type은 CellZone이다. 이름을 rotor_zone으로 바꿔준다. Axis Point 1 좌표는 (0 0 0)이고 Axis Point 2 좌표는 (0 0 0.1)이며 Radius는 2이다.

생성하면 geometry 네비게이션에 rotor_zone 과 1개의 면(rotor_zone_surface)가 만들어 진다. 이 면을 선택하고 마우스 오른쪽 버튼을 클릭해서 Edit를 눌러 이름을 rotor로 바꿔주고 Type을 Interface로 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cht/rotor_zone.png"><br> 회전하는 cell zone 형상 생성
</p>

## 유체 영역

유체 영역은 Cylinder를 이용해서 만든다.

Type은 None다. 이름을 fluid로 바꿔준다. Axis Point 1 좌표는 (0 2 0)이고 Axis Point 2 좌표는 (0 2 0.1)이며 Radius는 5이다.

생성하면 geometry 네비게이션에 fluid와 1개의 면(fluid_surface)가 만들어 진다. 이 면이 유체영역과 고체영역의 경계면이 된다. 이 면을 선택하고 마우스 오른쪽 버튼을 클릭해서 Edit를 눌러 이름을 fluid-solid로 바꿔주고 Type을 Interface-Inter-Region으로 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cht/fluid.png"><br> 유체 영역 형상 생성
</p>
<br>
최종적으로 Geometry 내비게이션은 아래 그림과 같이 된다.
<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cht/geomNavigation.png"><br> Geometry 네비게이션
</p>

형상을 만들면 'Display control'에 형상이 Geometry Type으로 표시된다. 항목을 클릭하고 마우스 오른쪽 버튼을 누르면 디스플레이 설정을 할 수 있다. Hide, Opacity, Color, Display Mode, No Cut 등이 있다.

'Next' 버튼을 눌러 '2.Region' 단계로 넘어간다.

# Region

여기서는 Region을 지정한다. 각 Region 내부의 임의의 점의 좌표를 설정하는 방법을 사용한다. 좌표를 직접 입력할 수도 있고 그래픽창에 초록색선이 만나는 점을 마우스로 이동해서 지정할 수 있다. 이 문제에서는 유체와 고체 두개의 영억을 설정한다.

Region 네비게이션의 오른쪽 상단에 있는(+)를 누르면 Region을 만들 수 있다.

그래픽창의 초록색선을 이동해서 유체 영역에 위치시킨 다음 Name을 fluid로 바꾸고 Type을 Fluid로 선택한다. 'Add' 버튼을 누르면 유체 영역이 만들어 진다.

같은 방법으로 고체 영역을 만들어 준다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cht/regionSelect.png"><br> Region 설정
</p>
<br>

'Next' 버튼을 눌러 '3.Base Grid' 단계로 넘어간다.

# Base Grid

배경 격자를 만들어 준다. 전체 도메인을 포함하는 육면체를 만들고 OpenFOAM의 blockMesh 유틸리티를 이용해 정렬격자로 만든다.

전체 도메인을 포함하는 육면체는 Geometry에서 만든 Hex6를 사용하도록 설정한다. x, y, z 방향의 격자개수는 140,140,1을 입력한다. 2차원 격자이기 때문에 z방향의 개수를 1로 준다.

'Generate' 버튼을 누르면 격자가 만들어 진다. 격자가 만들어지면 Display Control에 Boundary type과 Mesh type이 추가된다. 이것들은 상부의 'Cut'을 펼쳐서 x, y, z 축의 단면으로 잘라내고 볼 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cht/baseGrid.png"><br> Base Grid 설정
</p>
<br>

'Next' 버튼을 눌러 '4.Castellation' 단계로 넘어간다.

# Castellation

면과 제적의 격자를 조밀하게 나눌 수 있는 부분인데, 이 문제에서는 아무것도 수행하지 않는다.

'Refine' 버튼을 누르고 작업이 종료되면 'Next' 버튼을 눌러 '5.Snap' 단계로 넘어간다.

# Snap

형상에 맞게 격자점을 이동하는 부분이다. 디폴트 설정을 사용한다. 'Snap' 버튼을 누르고 작업이 종료되면 'Next' 버튼을 눌러 '6.Boundary Layer' 단계로 넘어간다.

# Boundary Layer

Boundary Layer 네비게이션 위쪽 Configurations 오른쪽의 (+)를 눌러 경계층 격자 생성 조건을 준다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cht/boundaryLayer.png"><br> Boundary Layer 설정
</p>
<br>

* Number of Layers : 3

* Thickness Model Specification : First and Expansion

* Size specification : Relative

* First Layer Thickness : 0.3

* Expansion Ratio : 1.2

* Min. Total Thickness: 0.1 

* Boundary : inner_wall, fluid_solid

'Advanced Configuration'은 디폴트 값을 사용한다.

'Apply' 버튼을 누르고 작업이 종료되면 'Next' 버튼을 눌러 '7.Export' 단계로 넘어간다.

# Export

'Export'버튼을 눌러 원하는 이름을 입력하면 baramFlow에서 열 수 있는 폴더가 만들어진다.

저장하고(File 메뉴의 Save) 프로그램을 종료한다.

