---
layout: post
title: 08. Models
category: userguidelist
---

# Models

난류모델과 온도 해석 여부를 설정한다. 격자를 읽었을 때 multi-region 격자이면 온도는 자동으로 해석하는 것으로 설정되고 바꿀 수 없다. Solver Type이 Density-based일 때도 온도는 자동으로 해석하는 것으로 설정되고 바꿀 수 없다.

Solver Type(Pressure-based/Density-based), Multiphase(Off/VOF/Cavitation),  Species 등은 프로그램 시작할 때 launcher에서 설정되며 바꿀 수 없다.(Cavitation, Species는 아직 지원되지 않는다)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/models.png"><br> Models 설정
</p>

## Turbulence

Turbulence를 더블 클릭하면 아래 그림의 설정창이 나타난다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/turbulence.png"><br> Turbulence Models 설정
</p>

Model을 선택하면 그에 따라 필요한 추가 설정 부분이 표시된다.

* Inviscid : 압축성 유동에서 Euler라고 많이 표현되는, 점성을 고려하지 않는 모델로 별도의 설정은 없다. 이 옵션을 선택하면 내부적으로 laminar가 선택되고 점성계수는 0이 된다. 물성값에서 점성계수를 직접 0으로 설정할 필요는 없다.

* Laminar : 층류유동이며 별도의 설정은 없다.

* Spalart-Allmaras : 1 equation 난류모델이며 turbulent Prandtl Number를 설정할 수 있다.

* k-epsilon : standard, RNG, Realizable 3가지 k-epsilon 모델을 선택할 수 있으며 turbulent Prandtl Number를 설정할 수 있다. Realizable 모델을 선택하면 Near-Wall Treatment 옵션으로 Standard Wall Function과 Enhanced Wall Treatment(two layer)를 선택할 수 있다.

* k-omega : k-omega 모델은 현재 Menter의 SST(Shear Stress Transport) 모델만 지원한다. turbulent Prandtl Number를 설정할 수 있다.


### Enhanced Wall Treatment(two layer)

Enhanced Wall Treatment(two layer)는 넥스트폼이 개발한 것으로 blending 함수를 사용한다. Standard wall function은 y+가 buffer layer에 있는 경우 결과의 정확도가 문제될 수 있는데, 이 모델은 y+에 상관없이 사용할 수 있는 벽함수이다. blending 함수는 다음의 식이 사용된다.

<h2 style="text-align: center">
    $\lambda = {\frac 1 2} \left[1 + tanh \left( \frac{Re_y - {Re_y}^* } {A} \right) \right ]$
</h2>

<h2 style="text-align: center">
    $A = \frac {\Delta Re_y } {tanh(0.98)}$
</h2>

*Ref) Shih, T. H., Liou, W. W., Shabbir, A., Yang, Z., & Zhu, J. (1995). A New k-epsilon eddy Viscosity Model for High Reynolds Number Turbulent Flows. Computers and Fluids, 24(3), 227-238.*


### turbulent Prandtl Number

turbulent Prandtl Number는 Internal Field와 Wall Function 두 가지를 설정할 수 있다. Internal Field의 값은 난류모델에 사용되고, Wall Function의 값은 alphat(turbulent thermal diffusivity)의 벽함수에 사용된다. 


## Energy

Energy를 더블 클릭하면 아래 그림의 설정창이 나타난다. 포함할 것인지 아닌지를 선택한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/energy.png"> <br> Energy 설정 
</p>


