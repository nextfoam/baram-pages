---
layout: post
title: 01. Introduction
category: meshuserguidelist
---

# 개요

BARAM v23.3의 격자 생성 모듈 BaramMesh는 OpenFOAM의 유틸리티인 blockMesh와 snappyHexMesh를 사용하여 격자를 생성하는 모듈이다. 형상은 STL 파일을 가져올 수 있고 육면체, 구, 실린더 형상을 생성할 수 있다. 경계층 격자를 포함한 octree 방식의 3차원 격자를 생성할 수 있으며 region, cell zone, interface, baffle을 만들 수 있다.

snappyHexMesh는 다음과 같은 단계를 통해 격자를 생성한다.

1) 전체 영역을 포함하는 정렬격자 형식의 배경 격자(background mesh)를 blockMesh 유틸리티를 사용하여 만든다. 

<p style="text-align: center">
    <!--<img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh-castellate.png"><br> 배경 격자 -->
    <img src="pic/mesh_castellate.png"><br> 배경 격자
</p>

2) 필요한 부분에 격자를 조밀하게 만들고, 격자를 만들지 않을 부분의 격자를 삭제한다. 이 과정을 castellation이라고 한다.

3) Surface 부근의 격자점을 surface 표면으로 이동하여 정확한 형상을 구현한다. 이 과정을 snap이라고 한다.

4) 경계층 격자를 만든다. 이 과정을 add layer라고 한다.

1 번 단계를 지나면 constant.polyMesh 폴더에 격자가 만들어지고, 2, 3, 4 단게를 지날 때 마다 1, 2, 3 폴더가 만들어 진다. 

BaramMesh에서는 위의 과정을 좀 더 세분화 해서 7개의 단계로 나누어 진행한다.

