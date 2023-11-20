---
layout: post
title: Initialization
category: userguidelist
---

# Initialization

Initialization은 계산에 사용하는 초기값을 설정하는 것과 계산을 통해 저장된 데이터를 모두 지우고 초기화하는 역할을 한다.

x, y, z 방향의 속도 성분과 압력, 온도, volume fraction 등의 초기값을 설정한다.

난류는 Spalart-Allmaras 모델을 사용할 때는 nuTilda를 사용하고, k-epsilon, k-omega 계열의 난류모델을 사용할 때는 velocity scale, turbulence intensity, viscosity ratio를 사용한다. 이 3가지 값을 이용해서 nut, k, epsilon, omega 등의 값을 계산해서 초기조건으로 사용하는데, 계산 방법은 다음과 같다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/eqn_nut.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/eqn_k.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/eqn_epsilon.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/eqn_omega.png"><br>
</p>

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/initial.png"><br> Initialization 설정
</p>

Advanced 탭에서 원하는 영역의 초기값을 따로 설정할 수 있다. OpenFOAM의 setFields 유틸리티를 사용한다.

영역은 hex, cylinder, sphere, cell zone을 사용할 수 있다. hex는 2개 점의 좌표로 정의된다. cylinder는 2개점의 좌표와 반지름으로 정의되며, sphere는 중심점과 반지름으로 정의된다.

초기화할 필드는 속도, 압력, 온도, volume fraction 등이다.

Override Boundary Value를 체크하면 영역에 포함되어 있는 경계면의 값도 해당 초기값으로 설정된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/setfield.png"><br> Advanced 설정
</p>


