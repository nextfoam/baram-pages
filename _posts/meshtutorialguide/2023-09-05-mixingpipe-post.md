---
layout: post
title: 01. Mixing Pipe
category: mesh
---

# Mixing Pipe 

## * [형상 파일](https://drive.google.com/file/d/1AmqT8iVNacvKUmp-CsSFFNSV6WoxQE7B/view?usp=sharing) 

## 1) 개요 
* 본 예제는 Mixing Pipe의 stl파일을 이용해 pipe 내부 격자를 생성하는 예제이다.<br>

* Pipe 내부의 경계층 생성과 Refinement 조절을 하면서 격자를 생성한다. <br>

* baramMesh를 실행하면 mixingpipe라는 이름으로 project를 생성한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.1.png"><br>
</p>

## 2) 형상 (Geometry)
형상은 주어진 mixingpipe.stl 파일을 사용한다. <br>
하단 탭에서 Import - Select - mixingpipe.stl을 선택한다. <br>
여기서 Split Surface는 형상 파일의 경계면을 분할해주는 기능이다.<br>
Split Surface를 활성화하면 Feature Angle을 기준으로 경계면이 분할된다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.2.png"><br>
</p>

window는 다음과 같다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.3.png"><br>
</p>

Geometry tab에서 surface들의 이름을 다음과 같이 변경한다.<br>

●  mixingpipe_surface_0 → wall <br>
●  mixingpipe_surface_1 → outlet<br>
●  mixingpipe_surface_2 → inlet1<br>
●  mixingpipe_surface_3 → inlet2<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.4.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.5.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.6.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.10.png"><br>
</p>

이후 하단의 Add - Hex를 선택하고 이름은 Box로 한다.<br>
inlet1 근처에 조밀한 격자의 생성 영역을 Box로 지정한다.<br>

***●  Shape : Hex***<br>
●  Name : Box<br>
●  Type : None<br>
```X : -0.5 ~ 0.5```<br>
```Y : -0.3 ~ 0.3```<br>
```Z : -1.8 ~ 0```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.7.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.8.png"><br>
</p>

이후 Box_surface를 마우스 오른쪽 버튼으로 클릭하여 Edit을 선택하고 아래와 같이 변경한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.9.png"><br>
</p>

여기까지 진행하고 Next 버튼을 클릭한다.<br>

이 때, Geometry Tab과 Display Control에 대한 설명은 아래와 같다.<br>

### 2-1) Geometry Tab
Geometry tab에서는 면 혹은 공간의 Type을 변경하거나 삭제할 수 있다.<br>
아래는 변경가능한 면과 공간의 Type이다.<br>
● Surface Type<br>
```Boundary : 면을 Inlet, Outlet, Wall의 경계면으로 설정한다.```<br>
```None : 면이 아무런 Type을 가지지 않는 즉, Internal로 설정한다.```<br>
```Interface : 면을 Non-Conformal 격자 혹은 Inter-Region간 Interface로 설정한다.```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.4.png"><br>
</p>

● Volume Type<br>
```None : 해당 공간을 아무런 Type을 가지지 않는 공간으로 설정한다.```<br>
```CellZone : 해당 공간을 유체 혹은 고체의 CellZone으로 설정한다.```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.8.png"><br>
</p>

### 2-2) Display Control
Display Control에서는 다음의 기능을 설정할 수 있다.<br>
```Cut : 격자를 사용자가 원하는 축 방향으로 잘라주는 기능이다.```<br>
```Hide & Show : 해당 면을 숨기거나 보여준다.```<br>
```Opacity : 해당 면을 숨기거나 보여준다.```<br>
```Color : 해당 면을 숨기거나 보여준다.```<br>
```Display Mode : 면을 보여주는 방식을 변경한다.```<br>
```Wireframe, Surface, Surface with WireFrame 총 세 가지 방식으로 변경가능하다.```<br>
```No Cut : 격자 중에서 사용자 선택에 따라 해당 면에 Cut 기능을 끌 수 있다.```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.21.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.22.png"><br>
</p>

## 3) 영역 (Region)
Region에서는 Fluid와 Solid 영역을 지정한다. <br>

상단 +버튼을 클릭하면 다음과 같이 화면이 변경된다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.11.png"><br>
</p>

이 때, Point과 위치하는 영역이 Fluid 혹은 Solid가 된다.<br>

본 예제에서는 Fluid 하나의 물질만 정의한다.<br>

Point의 위치는 Pipe 내부 임의의 영역으로 지정하면 된다.<br>

이후 Add 버튼을 누르면 아래 사진과 같이 Fluid 영역이 생성됨을 볼 수 있다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.12.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.13.png"><br>
</p>

## 4) 배경 격자 (Base Grid)
Snappy Hex Mesh는 배경 격자를 생성하고, 형상 Feature Line을 따라 Castellationg하는 방식으로 격자를 생성한다.<br>

BARAM-Snappy 역시 동일한 방식으로 격자를 생성하므로, 배경 격자를 생성해야한다.<br>

배경 격자 즉, Base Grid의 값은 다음과 같이 설정한다.<br>

이 때 되도록 x, y, z축 방향 격자들의 Aspect Ratio가 1이 되도록 만드는 것을 추천한다.<br>

**※ 아래 그림에서 Cell의 값이 1이 되도록 Number of Cells per Direction을 조정하면 Aspect Ratio가 1에 가까워진다.<br>**

Number of Cells per Direction은 아래와 같이 입력한다.<br>

***●  Number of Cells per Direction***<br>
```X : 20```<br>
```Y : 5```<br>
```Z : 40```<br>

이후 Generate와 Next 버튼을 누른다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.14.png"><br>
</p>

### 4-1) Use Hex6

* Use Hex6 기능을 활성화하면, 형상 크기에 맞게 배경 격자의 영역이 조정된다.<br>

## 5) Castellation
Castellation 단계에서는 형상의 Feature Line을 따라 Base Grid를 삭제하고 Volume Refinement를 진행한다.<br>

Volume Refinement의 +버튼을 누르고 아래와 같이 mixingpipe와 box에 대해 Volume Refinement를 정의한다.<br>

이후 Refine 버튼을 눌러 Refinement를 진행한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.15.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.16.png"><br>
</p>

## 6) Snap
Snap 단계에서는 형상의 Feature Line과 Surface를 따라 격자를 snap한다.<br>

Default 설정으로 snap 버튼을 누르면 아래와 같이 격자가 생성됨을 알 수 있다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.17.png"><br>
</p>

## 7) Boundary Layer
마지막으로 벽 주변에 Boundary Layer를 생성한다.<br>

Configuration의 + 버튼을 눌러 다음과 같이 경계층을 생성한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.18.png"><br>
</p>

아래 그림과 같이 벽 주변에 경계층이 생성됨을 볼 수 있다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.19.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/mixingpipe/1.20.png"><br>
</p>

## 8) Export
마지막으로 mixingpie라는 이름으로 Export 하면 BARAM v23에서 열 수 있는 Project 폴더, polyMesh 폴더 등이 생성된다.<br>