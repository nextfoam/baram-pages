---
layout: post
title: 01. Introduction
category: meshuserguidelist
---

# 개요

BARAM v23.3의 격자 생성 모듈 BaramMesh는 OpenFOAM의 유틸리티인 blockMesh와 snappyHexMesh를 사용하여 격자를 생성하는 모듈이다. 

형상은 STL 파일을 가져올 수 있고 육면체, 구, 실린더 형상을 생성할 수 있다. 

경계층 격자를 포함한 octree 방식의 3차원 격자를 생성할 수 있으며 region, cell zone, interface, baffle을 만들 수 있다.  
<br/>

OpenFOAM의 snappyHexMesh 유틸리티는 다음과 같은 단계를 통해 격자를 생성한다.

1) 전체 영역을 포함하는 정렬격자 형식의 배경 격자(background mesh)를 blockMesh 유틸리티를 사용하여 만든다. 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_blockMesh.png"><br> 배경 격자
</p>

2) 필요한 부분에 격자를 조밀하게 만들고, 격자를 만들지 않을 부분의 격자를 삭제한다. 이 과정을 castellation이라고 한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_castellate.png"><br> castellate
</p>

3) Surface 부근의 격자점을 surface 표면으로 이동하여 정확한 형상을 구현한다. 이 과정을 snap이라고 한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_snap.png"><br> snap
</p>

4) 경계층 격자를 만든다. 이 과정을 add layer라고 한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_layer.png"><br> 경계층 격자
</p>

첫번째 단계를 지나면 constant/polyMesh 폴더에 격자가 만들어지고, 2, 3, 4 단게를 지날 때 마다 1, 2, 3 폴더가 만들어 진다. 

BaramMesh에서는 위의 과정을 좀 더 세분화 해서 다음의 일곱개의 단계로 나누어 진행한다.

1) Geometry : 형상 파일을 읽어오거나 기본 형상을 만든다.

2) Region : 격자를 만들 영역 내부를 지정한다.

3) Base Grid : 배경 격자를 만든다.

4) Castellation : 필요한 부분에 격자를 조밀하게 만들고, 격자를 만들지 않을 부분의 격자를 삭제한다.

5) Snap : Surface 부근의 격자점을 surface 표면으로 이동하여 정확한 형상을 구현한다.

6) Boundary Layer : 경계층 격자를 만든다.

7) Export : BaramFlow에서 읽을 수 있는 폴더 형식으로 격자를 내보낸다.  
<br/>

위의 일곱 단계는 순차적으로 진행된다. 

__하나의 단계가 완료되면 그 단계는 잠금 상태가 되고 다음 단계로 넘어간다. 이전 단계로 돌아가서 다른 설정으로 작업하려면 해당 단계로 가서 잠금을 해제해야 한다. 잠금을 해제하면 해당 단계 이후에 만들어지 모든 결과물은 지워진다.__  
<br/>

# 설치 및 실행

BARAM v23의 설치 방법은 [Installation page](https://baramcfd.org/docs/installation/) 참고.

윈도우즈에서는 프로그램 설치가 완료되면 바탕화면에 BaramFlow, BaramMesh 아이콘이 만들어진다.

리눅스 터미널에서 실행할 때의 명령어는 다음과 같다.

    BaramFlow : baramFlow.sh 혹은 python -m baramFlow.main
    BaramMesh : baramMesh.sh 혹은 python -m baramMesh.main

baramMesh를 실행하면 새로운 격자를 만들 것인지 기존의 격자 작업을 열 것인지를 선택하는 창이 나타난다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_start.png"><br> 시작 화면
</p>

창에는 최근에 작업한 폴더들이 표시되는데 선택하면 baramMesh가 시작되고 해당 격자 작업이 열린다. 기존의 격자 작업을 열고 싶은데 창에 표시되지 않는 경우는 Open 버튼을 눌러 해당 폴더를 선택하면 된다. 

새로운 격자를 만들 New Case 버튼을 누르고 원하는 위치에 이름을 입력하면 baramMesh가 실행된다.
