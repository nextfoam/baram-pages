---
layout: post
title: 16. Run Conditions
category: userguidelist
---

# Run Conditions

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/runcondition.png"><br> Run Conditions 설정 - steady(좌),transient(우)
</p>

얼마나 계산할 것인지는 정상상태일때는 number of iteration을 사용하고, 비정상상태일 때는 End Time을 사용한다.

### Time Stepping Method

비정상상태일 때 time stepping method는 fixed와 adaptive를 선택할 수 있다. Fixed일 때는 time step size가 필요하다. Adaptive일 때는 유동영역은 Courant Number, 솔리드 영역에는 Maximum Diffusion Number에 의해 time step size가 결정된다.

Courant Number(CFL)와 Diffusion Number($D_i$)는 다음과 같이 정의된다.

<h2 style="text-align: center">
    $CFL = U \frac{\Delta t}{\Delta x}$
</h2>

<h2 style="text-align: center">
    $D_i = \alpha \frac{\Delta t}{\Delta x^2}$
</h2>

$\alpha$ : thermal diffusivity

$\Delta t$ : time step size

$\Delta x$ : grid size


### Max Courant Number for Vof

다상유동 계산시에는 추가로 Max Courant Number for VoF가 필요하다.


### Save Interval

어떤 간격으로 데이터를 자동으로 저장할 것인가를 지정한다. __0이면 자동 저장을 하지 않고 마지막 결과만 저장한다__. 계산이 종료되면 여기서 주어진 값과 상관없이 종료된 시점의 데이터는 저장된다.


### Retain Only the Most Recent Files

Maximum Number of Data Files에 설정된 개수 만큼의 가장 최근 결과만 저장하고 이전 결과는 삭제한다. 

