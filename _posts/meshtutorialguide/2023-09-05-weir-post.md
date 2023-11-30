---
layout: post
title: 05. Weir
category: mesh
---

# 1) Weir 개요

## * [형상 파일](https://drive.google.com/file/d/1GAW7sYRYS07-To1PhH5QCLTAK29bbbuu/view?usp=sharing) 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/weir/main.png"><br> wave height
</p>

위어(Weir)는 수공학에서 수로에 설지하는 구조물로 물이 넘치게 만들어 특정 수위를 유지하거나 유량을 측정하는데 사용한다. CFD에서는 이론식으로 구할 수 있는 유량과 해석 결과를 비교하여 코드 검증용으로 사용하기도 한다.

본 예제는 사각 위어에서 수위가 일정한 경우에 대한 해석을 위한 격자 생성 및 계산 예제이다.

사각위어의 단순한 형상을 stl 파일로 읽어 격자를 생성한다.

물의 입구에 수두에 해당하는 압력조건을 사용하기 위해 입구 경계면을 물과 공기의 영역을 나누어 만든다. 입구의 수위는 1.6m이다.

# 2) 형상(Geometry)

위어의 형상은 stl 파일을 사용한다. 

입구의 물과 공기의 경계면을 구분하기 위해 두 개의 Hex6를 사용하여 그림과 같이 구성한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/weir/geom.png"><br> Geomerty 설정
</p>

Import 버튼을 클릭해서 weir.stl 파일을 선택한다.

Add 버튼을 클릭해서 2개의 Hex6를 만들어준다. 

* down : Hex6

  + Type : None
  
  + Min./Max. : (-2 -1 0) / (2 1 1.6) : 수위가 1.6인 조건이기 때문에 z 좌표를 1.6까지 생성 
  
  + down_xMin, down_xMax, down_yMin, down_yMax, down_zMin, down_zMax의 6개 면이 만들어 지는데 마우스 오른쪽 버튼으로 Edit를 선택해서 이름을 바꾸어 준다(xMin은 water-in, xMax는 out, yMin은 front, yMax는 back, zMin은 bottom). zMax는 경계면이 아니기 때문에 Type을 None으로 설정한다.
  
* up : Hex6

  + Type : None
  
  + Min./Max. : (-2 -1 1.6) / (2 1 2)
  
  + up_xMin, up_xMax, up_yMin, up_yMax, up_zMin, up_zMax의 6개 면이 만들어 지는데 마우스 오른쪽 버튼으로 Edit를 선택해서 이름을 바꾸어 준다(xMin은 air-in, xMax는 out-1, yMin은 front-1, yMax는 back-1, zMax는 top). zMin은 경계면이 아니기 때문에 Type을 None으로 설정한다. 
 
Next 버튼을 눌러 다음 단계로 넘어간다.

# 3) Region

상단 (+) 버튼을 눌러 영역을 생성하고 그래픽 창에 연두색으로 나타나는 선의 교차점을 마우스로 이동하여 유체 영역에 위치시킨 후 Add 버튼을 클릭하면 설정이 완료된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/weir/region.png"><br> Region 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.

# 4) Base Grid

격자수를 100, 50, 50으로 설정한다. Generate 버튼을 누르면 배경 격자가 생성된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/weir/baseGrid.png"><br> Base Grid 설정
</p>

Next 버튼을 눌러 다음 단계로 넘어간다.

# 5) Castellation

전체 영역의 격자를 균일하게 만들 것이기 때문에 별도의 refinement 설정 없이 Refine 버튼을 누르면 castellation이 진행된다.

작업이 끝나면 Next 버튼을 눌러 다음 단계로 넘어간다.

# 6) Snap

디폴트 설정을 그대로 사용하고 Snap 버튼을 누른다.

작업이 끝나면 Next 버튼을 눌러 다음 단계로 넘어간다.

# 7) Boundary Layer

따로 경계층 격자를 만들지 않을 것이기 때문에 Apply 버튼을 누르고 작업이 끝나면 Next 버튼을 눌러 다음 단계로 넘어간다.
  
# 8) Export

마지막으로 weir라는 이름으로 Export 하면 baramFlow v23에서 열 수 있는 Project 폴더가 생성된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/weir/finalMesh.png"><br> 최종 격자
</p>



