---
layout: post
title: 03. Cantilever Beam
category: mesh
---

# Cantilever Beam 

## * [형상 파일](https://drive.google.com/file/d/1WsbkUpeVhtj8RlEXlhHEVLmwsnjyem5v/view?usp=sharing) 

## 1) 개요 
* 본 예제는 Cantilever Beam (외팔보)의 stl파일을 이용해 외팔보 주변 격자를 생성하는 예제이다.<br>

* 외팔보 경계층 생성과 Refinement 조절을 하면서 격자를 생성한다. <br>

* baramMesh를 실행하면 cantileverBeam라는 이름으로 project를 생성한다.<br>

## 2) 형상 (Geometry)
형상은 주어진 cantileverBeam.stl 파일을 사용한다. <br>
하단 탭에서 Import - Select - cantileverBeam.stl을 선택한다. <br>
여기서 Split Surface는 형상 파일의 경계면을 분할해주는 기능이다.<br>
본 예제에서는 Split Surface를 비활성화한다.<br>


<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/1.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/2.png"><br>
</p>

이후 하단의 Add - Hex를 선택하고 이름은 Box로 한다.<br>
외팔보 근처에 조밀한 격자의 생성 영역을 Box로 지정한다.<br>

***●  Shape : Hex***<br>
●  Name : Hex_1<br>
●  Type : None<br>
```X : -0.05 ~ 0.2```<br>
```Y : 0 ~ 0.04```<br>
```Z : 0 ~ 0.2```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/3.png"><br>
</p>

이후 Hex_1_surface를 마우스 오른쪽 버튼으로 클릭하여 Edit을 선택하고 아래와 같이 Type을 None으로 변경한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/4.png"><br>
</p>

이후, 하단의 Add - Hex6 (6Sub-Srfaces)로 외팔보 외부 유동장을 생성한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/addHex6.png"><br>
</p>

●  Name : Hex6_1<br>
●  Type : CellZone<br>
```X : -0.4 ~ 1.2```<br>
```Y : 0 ~ 0.2```<br>
```Z : 0 ~ 0.5```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/Hex6.png"><br>
</p>

여기까지 진행하고 Next 버튼을 클릭한다.<br>

## 3) 영역 (Region)
Region에서는 Fluid의 영역을 지정한다. <br>

상단 +버튼을 클릭하고 다음과 같이 Fluid 영역을 지정한다.<br>

Point의 위치는 외팔보 외부 지점으로 다음과 같이 좌표를 입력하여 지정하면 된다.<br>

Point : (0.4, 0.0875, 0.25) <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/5.png"><br>
</p>

이후 Add 버튼을 누르면 아래 사진과 같이 Fluid 영역이 생성됨을 볼 수 있다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/6.png"><br>
</p>

## 4) 배경 격자 (Base Grid)
이후, 배경 격자를 생성한다.<br>

배경 격자 즉, Base Grid의 값은 다음과 같이 설정한다.<br>

이 때 되도록 x, y, z축 방향 격자들의 Aspect Ratio가 1이 되도록 만드는 것을 추천한다.<br>

**※ 아래 그림에서 Cell의 값이 1이 되도록 Number of Cells per Direction을 조정하면 Aspect Ratio가 1에 가까워진다.<br>**

또한, Use Hex6을 활성화하면 Hex6 기반으로 외부 유동장으로 형상을 생성한다.<br>

본 예제에서는 Use Hex6을 활성화한다.<br>

Number of Cells per Direction은 아래와 같이 입력한다.<br>

***●  Number of Cells per Direction***<br>
```X : 100```<br>
```Y : 12```<br>
```Z : 30```<br>

이후 Generate와 Next 버튼을 누른다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/7.png"><br>
</p>

## 5) Castellation
이후, Castellation 단계를 진행한다.<br>

여기서는 Surface Refinement와 Volume Refinement를 진행한다.<br>

Surface Refinement의 +버튼을 누르고 아래와 같이 외팔보 표면에 격자를 refinement한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/surfaceRefinement.png"><br>
</p>

Volume Refinement의 +버튼을 누르고 아래와 같이 외팔보 주변에 생성하였던 Hex_1에 대해 Volume Refinement를 정의한다.<br>

우선, Refine 버튼을 누르고 Volume은 Box를 선택한다.<br>

그리고 Volume Refinement Level은 2로 입력한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/8.png"><br>
</p>

이후, Refine 버튼을 누른다.<br>

## 6) Snap
Snap 단계에서는 형상의 Feature Line과 Surface를 따라 격자를 snap한다.<br>

Default 설정으로 snap 버튼을 누른다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/9.png"><br>
</p>

## 7) Boundary Layer
마지막으로 벽 주변에 Boundary Layer를 생성한다.<br>

Configuration의 + 버튼을 눌러 다음과 같이 경계층을 생성한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/10.png"><br>
</p>

이후 Apply 버튼을 눌러 외팔보 주변 경계층을 생성한다.<br>

그러면, 아래 그림과 같이 벽 주변에 경계층이 생성됨을 볼 수 있다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/13.png"><br>
</p>

최종적으로 생성된 격자 형태는 다음과 같다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/14.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/cantileverBeam/15.png"><br>
</p>

## 8) Export
마지막으로 cantileverBeam이라는 이름으로 Export 하면 baramFlow v23에서 열 수 있는 Project 폴더, polyMesh 폴더 등이 생성된다.<br>