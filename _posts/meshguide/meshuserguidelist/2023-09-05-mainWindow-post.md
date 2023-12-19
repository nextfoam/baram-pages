---
layout: post
title: 02. Main Window
category: meshuserguidelist
---

# 주화면

프로그램을 실행하면 아래 그림과 같은 창이 나타난다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_mainWindow.png"><br> 시작 화면
</p>

주화면은 다음 6개의 영역으로 나눌 수 있다.

* 메뉴

* 진행단계 패널(Progress panel) : 화면 상단의 현재 작업의 상태를 나타내는 부분
  
* 설정 창(Configration window) : 화면의 왼쪽에 위치. 각 단계에서 필요한 모델과 값을 설정하는 부분

* 디스플레이 컨트롤(Display Control) : 화면의 왼쪽 두번째에 위치. 형상과 격자의 디스플레이에 관한 설정 부분

* 그래픽 창 : 형상과 격자를 보여주는 부분
  
* 메시지 창(Console Log) : 어플리케이션 실행시 로그를 보여주는 부분

## 메뉴

File, Mesh Quality, View, Parallel, Settings, Help 등의 메뉴가 있다.

File에는 New, Open, Open Recent, Save, Exit의 하위 메뉴가 있다. 

Mesh Quality의 Parameters를 클릭하면 아래 그림과 같은 창이 나타난다. 여기에 설정된 값을 기준으로 격자가 만들어 진다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_parameters.png"><br> Mesh Quality Parameters
</p>

병렬연산을 사용할 때는 Parallel메뉴를 사용한다. Environment를 클릭하면 아래 그림의 창이 나타난다. 코어수를 입력하고 로컬 머신인지 클러스터인지를 선택한다. 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_parallel.png"><br> 병렬연산 설정
</p>

클러스터일 때는 호스트 파일을 만들어 주어야 하는데 View/Edit 버튼을 눌러 만들 수 있다. 파일 내용은 다음과 같다.

[node name1]   cpu=[number of cores]

[node name2]   cpu=[number of cores]

[node name3]   cpu=[number of cores]

...

Settings에는 Scale, Language 2가지가 있다.

Scale은 프로그램의 해상도를 조절하는 것으로 기본값인 1.0 보다 커지면 창이 커지고 글자도 커진다. 새로운 설정을 적용하려면 프로그램을 닫고 다시 시작해야 한다.

Language는 현재 English, Suomi(핀란드어), 한국어만 지원 된다. 언어 번역은 Qt Linguist를 사용하며 사용자가 직접 참여할 수 있다. 참여 방법은 아래의 링크를 참조.

[언어 번역 / Laanguage Translate](https://baramcfd.org/docs/internationalization/)  
<br/>

## 진행단계 패널(Progress panel)

7가지 단계가 표시되어 있다. 현재 이후의 단계는 비활성화되어 있다. 현재 단계가 끝나고 Next 버튼을 누르면 현 단계는 잠금 상태가 되고 다음 단계가 활성화 된다. 

이전 단계로 돌아가면 상태를 확인할 수는 있지만 수정할 수는 없다. 이전 단계를 수정하고 싶으면 Unlock 버튼을 눌러 잠금을 해제해야 한다. 잠금을 해제하면 그 이후는 모든 단계의 잠금이 해제되고 만들어진 격자 데이터도 지워진다.  
<br/>

## 설정 창(Configration window)

각 단계에서 필요한 모델과 값을 설정한다.  
<br/>

## 디스플레이 컨트롤(Display Control)

형상과 격자의 리스트가 표시된다. Type은 Geomerty, Boundary, Mesh 3가지가 있다. [1.Geometry], [2.Region] 단계에서는 Geometry만 표시되고 [3.Base Grid]에서 배경 격자를 만들면 그 때부터 Boundary와 Mesh가 나타난다. Name과 Type을 클릭하여 리스트를 정렬할 수 있다.

리스트를 마우스 오른쪽 버튼으로 클릭하면 Hide, Opacity, Color, Display Mode, No Cut 등이 나타난다. 이것으로 디스플레이 형태를 설정할 수 있다. 각각의 항목별로 설정할 수도 있고 마우스의 드래그앤 드랍으로 여러개를 한꺼번에 설정할 수 있다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_display.png"><br> Display Control
</p>

상단의 Cut을 펼치면 축에 수직한 단면으로 잘라서 볼 수 있다. 디스플레이 옵션에서 No Cut을 선택한 개체는 잘리지 않는다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_cut.png"><br> Display Control 예
</p>  
<br/>

## 그래픽 창

상단에 디스플레이 환경을 설정하는 tool bar가 있다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/graphicsToolbar.png"><br> graphics tool bar
</p>
  
<p style="text-align: left">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/axis.png">    Axis : 원점(0, 0, 0)을 기준으로 해석 영역의 축 방향을 나타내준다.

</p>

<p style="text-align: left">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/ruler.png">    Ruler : Graphics 창에 해석 영역의 x, y, z 축 좌표를 표시해준다.

</p>

<p style="text-align: left">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/perspective.png">    Perspective : Perspective/Orthogonal view를 선택한다.

</p>

<p style="text-align: left">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/fit.png">    Fit : 해석 모델을 Graphics창에 전체 모습이 나오게 보여준다.

</p>

<p style="text-align: left">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/viewNormal.png">    Axis View : 현재 상태에 가장 근접한 축 단면에서 모델을 보여준다.

</p>

<p style="text-align: left">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/rotation.png">   Rotation View : 해석 모델을 90도 회전한다.

</p>

