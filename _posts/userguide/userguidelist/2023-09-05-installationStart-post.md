---
layout: post
title: 02. Installation & Start
category: userguidelist
---

# 설치 및 실행

BARAM-v24의 설치 방법은 [https://baramcfd.org/docs/installation/](https://baramcfd.org/docs/installation/) 참고.

*윈도우즈에서는 프로그램 설치가 완료되면 바탕화면에 BaramFlow, BaramMesh 아이콘이 만들어진다. 아이콘을 더블 클릭해서 실행하면 된다.

*리눅스는 터미널을 이용해서 파일을 실행한다. 터미널에서 BARAM이 설치된 폴더로 이동을 하고 실행 파일을 실행하여 프로그램을 시작한다. 실행파일은 bash 스크립트이며 실행 명령어는 다음과 같다. 

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




