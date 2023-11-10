# AhmedBody

## * [형상 파일](https://drive.google.com/file/d/1gxuKBcN6puyEF6Yv6VEYSNUz-tlHyAuD/view) 

## 1) 개요 
* 본 예제는 Ahmed Body의 stl파일을 이용해 자동차의 외부 유동장 격자를 생성하는 예제이다.<br>

* 자동차 주위에 경계층 생성과 Refinement 조절을 하면서 격자를 생성한다. <br>

* baramMesh를 실행하면 ahmedBody라는 이름으로 project를 생성한다.<br>

## 2) 형상 (Geometry)
형상은 주어진 ahmed.stl 파일을 사용한다. <br>
하단 탭에서 Import - Select - ahmed.stl을 선택한다. <br>
Feature Angle을 비활성화하고 ahmed.stl을 연다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/1.png"><br>
</p>

Geometry tab에서 surface들의 이름을 다음과 같이 변경한다.<br>

●  ahmed → bottom <br>
●  ahmed1 → leg<br>
●  ahmed2 → nose1<br>
●  ahmed3 → nose2<br>
●  ahmed4 → nose3<br>
●  ahmed5 → nose4<br>
●  ahmed6 → nose5<br>
●  ahmed7 → rear<br>
●  ahmed8 → side<br>
●  ahmed9 → slant<br>
●  ahmed10 → top<br>

이후, 자동차의 외부유동 해석을 위해 원방 경계를 생성한다.<br>
하단의 Add - Hex6를 선택하고 이름은 Farfield로 한다.<br>
여기서 Hex6는 외부 유동 해석에서 원방 경계를 생성할 경우 사용하는 형상이다.<br>

***●  Shape : Hex6***<br>
●  Name : Farfield<br>
●  Type : CellZone<br>
```X : -4.5 ~ 10```<br>
```Y : -0.05 ~ 5```<br>
```Z : 0 ~ 3```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/3.png"><br>
</p>

이후 생성된 Surface들의 이름을 다음과 같이 변경한다.<br>

●  Hex6_1_xMin → inlet <br>
●  Hex6_1_xMax → outlet <br>
●  Hex6_1_yMin → wall <br>
●  Hex6_1_yMax → sky <br>
●  Hex6_1_zMin → left_side <br>
●  Hex6_1_zMax → right_side <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/4.png"><br>
</p>

좌우 대칭 형상이기 때문에 +z 방향으로 격자 절반만 생성한다.<br>

이후, 격자 크기를 조밀하게 적용할 영역을 지정한다.<br>
Add - Hex를 눌러 영역 하나를 생성하고 이름은 Refinement1로 지정한다.<br>

***●  Shape : Hex***<br>
●  Name : Refinement1<br>
●  Type : None<br>
```X : -0.6 ~ 1```<br>
```Y : -0.05 ~ 0.4```<br>
```Z : 0 ~ 0.27```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/5.png"><br>
</p>

Refinement1_surface의 타입은 None으로 변경한다.<br>

이후, 다시 한 번 Add - Hex를 눌러 영역 하나를 생성하고 이름은 Refinement2로 지정한다.<br>

***●  Shape : Hex***<br>
●  Name : Refinement2<br>
●  Type : None<br>
```X : -0.9 ~ 1.7```<br>
```Y : -0.05 ~ 0.6```<br>
```Z : 0 ~ 0.5```<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/6.png"><br>
</p>

Refinement2_surface의 타입은 None으로 변경한다.<br>

이후 상단의 Parallel - Environment를 클릭하고, Number of Cores는 4를 입력한다.<br>
이렇게 하면 4개 코어를 이용하여 격자를 생성하게 된다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/parallel.png"><br>
</p>

여기까지 진행하고 Next 버튼을 클릭한다.<br>

## 3) 영역 (Region)
Region에서는 Fluid의 영역을 지정한다. <br>

상단 +버튼을 클릭하고 다음과 같이 Fluid 영역을 지정한다.<br>

Point의 위치는 차량 외부 지점으로 다음과 같이 좌표를 입력하여 지정하면 된다.<br>

Point : (2.75, 2.475, 1.40275) <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/7.png"><br>
</p>

이후 Add 버튼을 누르면 아래 사진과 같이 Fluid 영역이 생성됨을 볼 수 있다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/8.png"><br>
</p>

## 4) 배경 격자 (Base Grid)
이후, 배경 격자를 생성한다.<br>
여기서는 Use Hex6를 활성화 한 후, Number of Cells per Direction은 아래와 같이 입력한다.<br>

***●  Number of Cells per Direction***<br>
```X : 100```<br>
```Y : 35```<br>
```Z : 20```<br>

이후 Generate와 Next 버튼을 누른다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/9.png"><br>
</p>

## 5) Castellation
이후, Castellation 단계를 진행한다.<br>

Volume Refinement의 +버튼을 누르고 아래와 같이 차량 주변에 생성하였던 Refinement1에 대해 Volume Refinement를 정의한다.<br>

Group Name은 Refinement1로 변경한다.<br>

그리고 Volume Refinement Level은 5로 입력한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/10.png"><br>
</p>

이후 다시 한번 +버튼을 누르고 Refinement2에 대해 Volume Refinement를 정의한다.<br>

Group Name은 Refinement2로 변경하고 Volume Refinement Level은 3으로 입력한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/11.png"><br>
</p>

Refine 버튼을 눌러 Refine을 진행한다.<br>

## 6) Snap
Snap 단계에서는 기본 설정으로 snap을 진행한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/12.png"><br>
</p>

## 7) Boundary Layer
마지막으로 벽 주변에 Boundary Layer를 생성한다.<br>

Configuration의 + 버튼을 눌러 다음과 같이 경계층을 생성한다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/13.png"><br>
</p>

최종적으로 생성된 격자 형태는 다음과 같다.<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/14.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/ahmedBody/15.png"><br>
</p>

## 8) Export
마지막으로 ahmedBody이라는 이름으로 Export 하면 baramFlow v23에서 열 수 있는 Project 폴더, polyMesh 폴더 등이 생성된다.<br>