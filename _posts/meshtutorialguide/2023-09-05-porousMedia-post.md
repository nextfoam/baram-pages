---
layout: post
title: 07. Porous Media
category: mesh
---

# 1) Porous Media 개요

### * [형상 파일 링크](https://drive.google.com/file/d/1Jlqrgd5BrKkAfhzNkybtb0cF3zSEAFfA/view?usp=sharing) 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/intro.png"><br> 형상 및 유동장
</p>

본 에제는 porous media 조건을 사용한 유동해석 예제이다. 상부 왼쪽에서 유동이 유입되고 porous 영역을 지나 아래로 유동이 흐르는 문제이다.(위 그림 왼쪽에서 파란색 부분이 porous 영역)

OpenFOAM의 porous media 모델은 porous 영역에서 불연속적인 속도 분포가 나타나고 압력손실도 입력 조건과 조금 다른 결과를 보이는 문제가 있다. 아래 그림의 왼쪽이 Baram-v23의 결과이며, 오른쪽이 OpenFOAM 2306의 standard 솔버를 사용한 결과이다. 

Baram이 사용하는 NextFOAM에서는 porous 영역에서 압력의 interpolation 방법을 개선하여 이 문제를 해결하였다(이에 대한 자세한 내용은 아래 링크의 문서를 참고). 결과의 정확성과 함께 수렴성도 많이 좋아진 것을 확인할 수 있다.

### *[Porous Media 참고 문헌](https://nextfoam.co.kr/proc/DownloadProc.php?fName=231101140051_yvpJhMF0nY.pdf&realfName=10thOKUCC_OpenFOAM%EC%82%AC%EC%86%8C%ED%95%9C%EB%AC%B8%EC%A0%9C%EB%93%A4.pdf)

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/res.png"><br> 결과 (좌)Baram v23, (우) openfoam 2306 standard solver
</p>

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/residual-1.png"><br> Residual (좌)Baram v23, (우) openfoam 2306 standard solver
</p>
<br/>


# 2) 형상(Geometry)

덕트의 형상은 stl 파일을 사용한다.

Import 버튼을 눌러 porousMedia.stl 파일을 선택하고 'Split Surface' 옵션을 선택하여 경계면을 구분한다. 하나의 면으로 되어있는 형상 파일이 feature angle에 따라 7개의 면으로 나누어진다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/import.png"><br> 
</p>

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/split.png"><br> 
</p>

7개의 면들 중에 입구와 출구를 구분하기 쉽게 이름을 바꿔준다. 그래픽창에서 마우스로 입구를 클릭하면 Geometry 리스트에서 해당 면이 활성화된다. 마우스 오른쪽 버튼으로 Edit를 누르고 이름을 inlet, outlet으로 바꾸어 준다.

Porous 영역은 Add 버튼을 눌러 Hex를 이용해서 만든다. Hex의 설정은 다음과 같다.

* Name : porousZone

* Type : CellZone

* Min. : (-0.3 -0.2 0.8)

* Max. : (0.3 0.2 0.9)

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/hex.png"><br>
</p> 

Porous 영역을 생성하면 그 하위에 porousZone_surface라는 것이 생성되는데 이것의 Type을 None으로 설정한다.

최종적인 Geometry 리스트는 다음 그림과 같이 된다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/geom.png"><br> 
</p> 

Next 버튼을 눌러 다음 단계로 넘어간다.
<br/>

# 3) Region

상단 (+) 버튼을 눌러 영역을 생성하고 그래픽 창에 연두색으로 나타나는 선의 교차점을 마우스로 이동하여 유체 영역에 위치시킨 후 Add 버튼을 클릭하면 설정이 완료된다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/region.png"><br> 
</p> 

Next 버튼을 눌러 다음 단계로 넘어간다.
<br/>

# 4) Base Grid

격자수를 60, 40, 120으로 설정한다. Generate 버튼을 누르면 배경 격자가 생성된다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/baseGrid.png"><br> 
</p> 

Next 버튼을 눌러 다음 단계로 넘어간다.
<br/>

# 5) Castellation

전체 영역의 격자를 균일하게 만들 것이기 때문에 별도의 refinement 설정 없이 Refine 버튼을 누르면 castellation이 진행된다.

작업이 끝나면 Next 버튼을 눌러 다음 단계로 넘어간다.
<br/>

# 6) Snap

모든 설정은 디폴트 값을 사용한다.


# 7) Boundary Layer

덕트 벽면에 경계층 격자를 생성한다.

Configuration에서 (+)를 눌러 다음과 같이 설정한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/blayer.png"><br> 
</p> 

* Number of Layers : 5

* Thickness Model Specification : First and Expansion

* Size Specification : Relative

* First Layer Thickness : 0.15

* Expansion Ratio : 1.2

* Min. Total Thickness : 0.3

* Boundary : 모든 덕트 벽면 선택

나머지는 Dafault 설정 그대로 적용하고 apply 버튼을 누른다.

|[![intro](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/layer.png)](https://github.com/nextfoam/baram-pages/raw/main/screenshots/mesh/porousMedia/layer.png){:target="_blank"}|

작업이 끝나면 Next 버튼을 눌러 다음 단계로 넘어간다.

  
# 8) Export

마지막으로 porous라는 이름으로 Export 하면 baramFlow v23에서 열 수 있는 Project 폴더가 생성된다.

