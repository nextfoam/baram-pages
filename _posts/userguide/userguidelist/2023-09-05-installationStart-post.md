---
layout: post
title: 02. Installation & Start
category: userguidelist
---

# 설치

BARAM-v24의 설치 방법은 [https://baramcfd.org/docs/installation/](https://baramcfd.org/docs/installation/) 사이트에 정리되어 있다.

<!------------------------------------------------------------------>
# 실행

윈도우즈에서는 프로그램 설치가 완료되면 바탕화면에 BaramFlow, BaramMesh 아이콘이 만들어진다. 아이콘을 더블 클릭해서 실행한다.

리눅스는 터미널을 이용해서 파일을 실행한다. 터미널에서 BARAM이 설치된 폴더로 이동을 하고 실행 파일을 실행하여 프로그램을 시작한다. 실행파일은 bash 스크립트이며 실행 명령어는 다음과 같다. 

* BaramFlow : bash baramFlow.sh
* BaramMesh : bash baramMesh.sh

BARAM을 실행하면 새로운 계산을 할 것인지 기존의 문제를 열 것인지를 선택하는 창이 나타난다.

창에는 최근에 해석한 폴더들이 표시되는데 선택하면 BARAM이 시작되고 해당 문제가 열린다. 기존의 문제를 열고 싶은데 창에 표시되지 않는 경우는 Open 버튼을 눌러 해당 폴더를 선택하면 된다. 

새로운 계산을 할 때는 New Case 버튼을 누르고 원하는 위치에 이름을 입력하면 Solver Type, Multiphase Mode 선택창이 차례로 나타난 후 BARAM이 실행된다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/launcher1.png"><br> 시작화면
</p>
 
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/launcher2.png"><br> New Case
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/launcher3.png"><br> Solver Type 설정
</p>
 
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/launcher4.png"><br> Multiphase Model 설정
</p>

<!------------------------------------------------------------------>
# 주화면

프로그램을 실행하면 아래 그림과 같은 창이 나타난다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/maingui.png"><br> 주화면
</p>

주화면은 다음 5개의 영역으로 나눌 수 있다.

* Menu
  + File, Mesh, View, Parallel, Settings, Help 등의 메뉴가 있다 
* Graphics Toolbar
* Navigation
  + 물리 모델, 물성치, 경계 조건, 수치해석 조건, 초기 조건 등의 탭을 선택할 수 있다
* Configration
  + 물리 모델, 물성치, 경계 조건, 수치해석 조건, 초기 조건 등의 모델과 값을 설정할 수 있다
* Graphics \& Console(각 탭을 클릭하면 전환 된다)
  + Console : 계산 진행 중에 나오는 Residuals, 각종 Log, Error 문구 등이 나타난다  
  + Mesh : 해석에 사용되는 격자를 보여준다  
  + Residuals : 해석의 Residuals 값을 보여준다  
  + Monitor : User가 원하는 Monitoring 물리량의 그래프를 나타낸다  

<!------------------------------------------------------------------>
# 메뉴

메뉴는 File, Mesh, View, Parallel, Settings, External Tools, Help 등으로 구성된다.

## File

### Save

모든 설정을 저장한다.

### Save As

모든 설정을 다른 이름으로 저장하는데 계산결과는 저장하지 않는다

### Load Mesh

격자를 불러온다. 지원하는 격자 파일 포맷은 다음과 같다.
* __openfoam__ : constant 혹은 polyMesh 폴더를 선택한다. multi-region인 경우는 여러 개의 polyMesh 폴더가 있기 때문에 constant 폴더를 선택히야 한다. multi-region 격자에서 특정한 polyMesh 폴더를 선택하면 해당 부분만 읽어 온다.
* __Fluent__ : msh/cas 파일을 변환한다. 아스키 파일만 가능하다. 넥스트폼이 개발한 fluenToFoam 유틸리티를 사용하며 multi-region 격자로 변환이 가능하다.
* __StarCCM+__ : ccm 파일을 변환한다. libccmio 라이브러리가 있어야 한다. 리눅스에서만 지원된다. 
* __Gmsh__ : 오픈소스 격자 생성 프로그램인 Gmsh의 msh 파일을 변환한다. 아스키 파일만 가능하다.
* __I-deas Universal__ : unv 파일을 변환한다. 아스키 파일만 가능하다.
* <span style="color:gray">PLOT3D GRID : PLOT3D 격자를 변환한다.(곧 지원 예정)</span>

### Close Case

현재의 작업을 종료하고 BaramFlow의 초기 화면(New Case 혹은 Open 선택)으로 돌아간다.

### Exit

프로그램을 종료한다.

<!------------------------------------------------------------------>
## Mesh

격자 정보 출력, 축소/확대(Scale), 이동(Translate), 회전(Rotate) 등의 동작을 수행한다.

__Mesh Info.__ : cell 정보와 도메인 크기를 보여준다.
__Scale__ : x, y, z 각 방향의 비율을 입력 한다.
__Translate__ : x, y, z 각 방향으로 이동할 거리를 입력한다.
__Rotate__ : 회전 중심의 좌표, 회전축, 각도를 입력한다.

## View

주화면의 Graphics에 있는 Console, Mesh, Residuals, Monitor 등을 on/off 할 수 있다

## Parallel

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/parallel.png"><br> 병렬 연산 설정 창
</p>

병렬 연산에 대한 설정을 한다. CPU core 개수와 병렬 연산 방식을 선택한다. 병렬 연산 방식은 Local Machine과 Cluster가 있으며, Cluster인 경우 node list가 적힌 텍스트 파일을 만들어 주어야 한다. 파일 내용은 다음과 같다.

[node name1]   cpu=[number of cores]

[node name2]   cpu=[number of cores]

[node name3]   cpu=[number of cores]

...


## Settings

Scale, Language, ParaView 3가지가 있다.

__Scale__ : 프로그램의 해상도를 조절하는 것으로 기본값인 1.0 보다 커지면 창이 커지고 글자도 커진다. 새로운 설정을 적용하려면 프로그램을 닫고 다시 시작해야 한다.

__Language__ : 현재 English, Suomi(핀란드어), 한국어만 지원 된다. 언어 번역은 Qt Linguist를 사용하며 사용자가 직접 참여할 수 있다. 참여 방법은 아래의 링크를 참조.
[언어 번역 / Language Translate](https://baramcfd.org/docs/internationalization/)

__ParaView__ : ParaView 실행파일의 위치를 지정한다.

## External Tools

External Tools에는 ParaView 항목이 있는데, 후처리를 위해 ParaView를 구동한다.

## Help

About에서 프로그램정보와 third party 프로그램 정보를 확인할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/about.png"><br> About 창
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/thirdParty.png"><br> third party software 정보
</p>

<!------------------------------------------------------------------>
# Graphics Tool bar

3차원 그래픽에 대한 tool bar에는 다음과 같은 아이콘들이 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/graphicsToolbar.png"><br> graphics tool bar
</p>

<p align='left'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/axis.png">    Axis : 원점(0, 0, 0)을 기준으로 해석 영역의 축 방향을 나타내준다.
</p>

<p align='left'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/ruler.png">    Axis Grid : Graphics 창에 해석 영역의 x, y, z 축 좌표를 표시해준다.
</p>

<p align='left'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/ruler-1.png">    Ruler : 면 위의 두 점 사이의 거리를 확인할 수 있다.
</p>

<p align='left'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/perspective.png">    Perspective : Perspective/Orthogonal view를 선택한다.
</p>

<p align='left'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/fit.png">    Fit : 해석 모델을 Graphics창에 전체 모습이 나오게 보여준다.

</p>

<p align='left'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/viewNormal.png">    Axis View : 현재 상태에 가장 근접한 축 단면에서 모델을 보여준다.

</p>

<p align='left'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/rotation.png">   Rotation View : 해석 모델을 90도 회전한다.
</p>

<p align='left'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/bg.png">   Backgroud Color : 바탕화면의 색상을 설정한다.
</p>

View option은 Feature Edges, Points, Surfaces, Surface With Edges, Wireframe의 5가지를 선택할 수 있다.

<!------------------------------------------------------------------>
# 그래픽창의 마우스 컨트롤

* 회전 : 마우스 왼쪽 버튼을 누르고 이동
* 이동 : 마우스 휠을 누르고 이동
* 축소/확대 : 마우스 휠을 돌리거나 마우스 오른쪽 버튼을 누르고 이동 
* 경계면 선택 : 마우스 왼쪽 버튼 - 선택한 면이 흰색으로 표시

