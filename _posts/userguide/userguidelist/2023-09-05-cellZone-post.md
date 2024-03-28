---
layout: post
title: 10. Cell Zone Condition
category: userguidelist
---

# Cell Zone Conditions

Cell zone Condition에는 격자의 region과 cell zone이 아래 그림과 같이 표시된다. Single-region 문제인 경우 하나의 region만 표시되고 multi-region인 경우 region의 개수 만큼 나타난다. 각 region에 속한 cell zone들이 그 아래에 나타난다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/cellZoneUI.png"><br> CellZone 설정
</p>

Region을 더블 클릭하면 아래 그림의 창이 나타난다. [Setup-Materials]에 있는 물질들 중 하나를 해당 region의 물질로 선택한다. 전체 region에 소스항이나 일정한 값을 주고 싶다면 해당 항목을 설정한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/region.png"><br> Region 설정
</p>

다상유동의 경우에는 2개의 물질을 primary와 secondary로 설정해 주고 두 물질간의 표면장력(surface tension)을 입력해 준다. 아래 그림에서 Select 버튼을 누르면 오른쪽 그림과 같은 창이 열리고 물질을 선택할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/regionVOF.png"><br> 다상유동에서 유체 선택
</p>

cellZone을 더블 클릭하면 아래 그림의 창이 나타난다. Zone Type, Source Terms, Fixed Values를 설정할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/cellZone.png"><br> cell zone 설정
</p>
<br>

## Zone Type

Zone type은 Multiple Reference Frame(MRF), Porous, Sliding Mesh, Actuator Disk 등이 있다. 이 조건들과 함께 Source Terms, Fixed Values 조건을 사용할 수 있다.
<br>

### Multiple Reference Frame, MRF

MRF는 회전하는 물체를 시뮬레이션 할 때 물체를 회전시키지 않고 회전체 주변의 유동을 회전상대좌표계에서 계산하는 방법이다. MRF를 선택하면 아래 그림과 같은 설정 부분이 나타난다. 세부 설정 항목은 다음과 같다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mrf.png"><br> MRF 설정
</p>

* Rotating Speed, RPM : 회전속도(Revolution Per Minute)

* Rotating Axis Origin : 회전 중심의 좌표

* Rotating Axis Direction: 회전축(회전 방향이 반시계 방향이 되도록 방향 설정)

* Static Boundary : MRF cell zone 영역 안에 있지만 회전하지 않는 경계면들을 선택한다. <span style="color:blue"> 인터페이스 면도 선택해야 한다.</span>
<br>

### Sliding Mesh

+ Sliding Mesh는 운동하는(baram 현재 버전에서는 회전 운동만 지원, 병진 운동은 추후 지원 예정) 물체 주위를 cell zone으로 구성하고 격자를 움직이는 방법이다.
+ 운동하는 cell zone과 정지한 cell zone의 각 경계면은 interface로 구성해야 한다.
+ <span style="color:blue">Cell zone 내부에 있는 움직이는 경계면은 moving wall 경계조건을 사용해햐 한다.</span>

설정 항목은 Rotating Speed(RPM), Rotation Axis Origin, Rotation Axis Direction이며 회전 방향은 MRF에서와 같다.
<br>

### Poirous Zone

Porous Zone은 다공성 매질이나 작은 영역에 매우 복잡한 형상이 있을 때 형상을 직접 구현하지 않고 유속에 따른 압력 손실로 모델링하는 방법이다. 압력 손실의 모델링 방법은 Darcy-Forchheimer 모델과 Power law 모델을 사용할 수 있다.

OpenFOAM의 porous media 모델은 porous 영역에서 불연속적인 속도 분포가 나타나고 압력손실도 입력 조건과 조금 다른 결과를 보이는 문제가 있다. Baram이 사용하는 NextFOAM에서는 porous 영역에서 압력의 interpolation 방법을 개선하여 이 문제를 해결하였다.([이에 대한 자세한 내용은 아래 링크의 문서를 참고](https://nextfoam.co.kr/proc/DownloadProc.php?fName=231101140051_yvpJhMF0nY.pdf&realfName=10thOKUCC_OpenFOAM%EC%82%AC%EC%86%8C%ED%95%9C%EB%AC%B8%EC%A0%9C%EB%93%A4.pdf))

__Darcy-Forchheimer 모델__

다음의 식을 사용한다. <br>

<h2 style="text-align: center">
$S_i = \left( \mu d + \rho |U| \frac{f}{2} \right)$
</h2>
<br/>

압력손실 방향은 두 개의 벡터에 의해 결정된다. 두 벡터는 Direction-1, Direction-2에 의해 결정되고 세번째 방향은 두 벡터에 수직한 방향벡터이다.

Inertial Resistance Coefficient(f, Forchheimer coefficient)와 Viscous Resistance Coefficient(d, Darcy coefficient)를 벡터로 입력한다.

__Power law 모델__

다음의 식을 사용한다.


<h2 style="text-align: center">
$S_i = - \rho C_0 |U|^{C_1 -1} U$
</h2>
<br/>

C<sub>0</sub>와 C<sub>1</sub>은 상수로 입력한다.
<br>

### Actuator Disk

Actuator disk 모델은 프로펠러와 같은 회전체를 디스크로 모델링하여 속도의 소스항으로 처리한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/actuatorDisk.png"><br> Actuator Disk 설정
</p>

설정 항목은 다음과 같다.

* Disk Direction

* Power Coefficient

* Thrust Coefficient

* Disk Area : 디스크 단면적

* Upstream Point : 디스크 상류 임의 지점의 좌표

* Force Computation method : Froude's method / Variable-Scaling method


추력을 계산하는 방법 중 Froud's method는 다음 식을 사용한다.

<h2 style="text-align: center">
$T = 2 \rho A |u_m \cdot n|^2 a(1-a)$
</h2>

<h2 style="text-align: center">
$a = 1 - \frac{C_p}{C_t}$
</h2>
<br/>


추력을 계산하는 방법 중 Variable-Scaling method는 다음 식을 사용한다.

<h2 style="text-align: center">
$T = 0.5 \rho A |u_0 \cdot n|^2 C_T ^*$
</h2>

<h2 style="text-align: center">
${C_T}^* = C_T \left( \frac{|u_m|}{|u_0|}\right)^2$
</h2>
<br>

* 변수 정의

  + _T_ : Thrust magnitude

  + _ρ_ : Monitored incoming fluid density

  + _A_ : Actuator disk planar surface area

  + _u<sub>m</sub>_ : Incoming velocity spatial-averaged on monitored region

  + _u<sub>0</sub>_ : Incoming velocity spatial-averaged on actuator disk

  + _n_ : Surface-normal vector of the actuator disk pointing upstream

  + _a_ : Axial induction factor

  + _C<sub>p</sub>_ : Power coefficient

  + _C<sub>T</sub>_ : Thrust coefficient

  + _C<sub>T</sub> <sup>*</sup>_ : Calibrated thrust coefficient
<br>

## Source Terms

에너지, 질량, 난류 관련 필드 등에 소스 항을 설정할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/source.png"><br> Source Term 설정
</p>

소스의 크기를 주는 방법은 전체 cell zone에 가해질 소스의 크기를 주는 방법과 단위 체척당 가해질 소스의 크기를 주는 두 가지가 있다. 비정상상태 문제일 때 질량과 에너지 소스의 크기를 시간에 따라 변하는 값을 줄 수 있는데, piecewise linear와 polynomial 방법이 제공된다.
<br>

## Fixed Values

Cell zone의 속도 벡터, 온도, 난류 필드의 평균값을 고정할 수 있다. 속도의 경우 계산의 불안정성이 발생할 수 있어 relaxation factor를 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/fixedValue.png"><br> Fixed Value 설정
</p>


