---
layout: post
title: 02. Installation & Start
category: userguidelist
---

# 설치 및 실행

BARAM v23의 설치 방법은 https://baramcfd.org/docs/installation/ 참고.

윈도우즈에서는 프로그램 설치가 완료되면 바탕화면에 BaramFlow, BaramMesh 아이콘이 만들어진다.

리눅스 터미널에서 실행할 때의 명령어는 다음과 같다.


* BaramFlow : baramFlow.sh 혹은 python -m baramFlow.main
* BaramMesh : baramMesh.sh 혹은 python -m baramMesh.main


BARAM을 실행하면 새로운 계산을 할 것인지 기존의 문제를 열 것인지를 선택하는 창이 나타난다.

창에는 최근에 해석한 폴더들이 표시되는데 선택하면 BARAM이 시작되고 해당 문제가 열린다. 기존의 문제를 열고 싶은데 창에 표시되지 않는 경우는 Open 버튼을 눌러 해당 폴더를 선택하면 된다. 

새로운 계산을 할 때는 New Case 버튼을 누르고 원하는 위치에 이름을 입력하면 Flow Type, Multiphase Model, Species 선택창이 차례로 나타난 후 BARAM이 실행된다. 지금은 Flow Type은 incompressible만, Species는 Off만 선택할 수 있다. <br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/launcher1.png"><br> 시작화면
</p>

<br>
 
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/launcher2.png"><br> New Case
</p>

<br>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/launcher3.png"><br> Flow Type 설정
</p>

<br>
 
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/launcher4.png"><br> Multiphase Model 설정
</p>

<br>
 
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/launcher5.png"><br> Species 설정
</p>


