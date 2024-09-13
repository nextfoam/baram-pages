---
layout: post
title: 09. Materials
category: userguidelist
---

# Setup - Materials

BARAM은 몇가지 물질들의 물성값을 데이터베이스로 제공한다. 해석에 사용할 물질들을 추가하고, 필요하다면 물성값을 수정해서 사용할 수 있다. 그리고 이 물질들이 조합하여 혼합물(mixture)을 구성할 수 있으며, 화학종 혼합을 계산할 때 이것을 사용한다.

BARAM이 제공하는 물질 데이터베이스는 다음과 같다.

* Gas : Air, Oxygen, Nitrogen, Carbon-dioxide, Hydrogen, Argon, Carbon-monoxide, Methane, Water-vapor

* Liquid : Water-liquid

* Solid : Steel, Concrete, Aluminum, Copper

아래 왼쪽 그림 오른쪽상단의 (+)버튼을 누르면 가운데 그림과 같은 창이 나타나고 물질을 추가 할 수 있다. 오른쪽 그림은 oxygen이 추가된 결과이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/material.png"><br> Material 설정
</p>

혼합물(mixture)을 추가할 때는 여러개의 물질을 한꺼번에 선택하고 아래 가운데 그림처럼 'Create Mixture' 버튼을 이용한다. 이 버튼은 Model에서 화학종 계산이 활성화 되었을 때만 나타난다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/material-maxture.png"><br> Mixture material 설정
</p>

물성값 수정 버튼을 누르면 아래 그림의 창이 나타난다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/materialProperties.png"><br> 물성값 설정
</p>

수정할 수 있는 항목은 Name, Density, Specific Heat, Viscosity, Thermal Conductivity, Molecular Weight, Absorption Coefficient, Saturation Pressure, Emissivity 등이며 기체/액체/고체에 따라서 그리고 에너지방정식을 계산하는지에 따라서 항목들이 조금씩 달라진다.

### Density

Constant, Perfect Gas, Polynomial, Incompressible perfect gas 등을 선택할 수 있다. 에너지방정식을 풀지 않을 때와 액체나 고체일 때는 Constant만 사용할 수 있다. 

Incompressible perfect gas는 밀도를 온도만의 함수로 결정한다.(현재 화학종 혼합을 계산할 때만 쓸 수 있는데 다음 버전부터는 에너지방정식을 계산하는 모든 경우에 사용할 수 있게 될 예정이다.)

<h2 style="text-align: center">
    $\rho = \frac {p_{ref}} {RT}$
</h2>

$p_{ref}$ : Reference Values에서 설정한 압력이 사용된다.

### Specific Heat Capacity

Constant와 Polymomial을 선택할 수 있다.

### Viscosity

Constant, Sutherland, Polynomial을 선택할 수 있으며, 액체의 경우 Cross, Hershel-Bulkley, Carreau, Non-Newtonian-power-law 등의 비뉴턴유체 모델을 선택할 수 있다.

Sutherland 관계식은 이상기체의 점도를 온도의 함수로 표현한 것으로 에너지방정식을 계산할 때만 사용할 수 있다. Sutherland Coefficient와 Sutherland Temperature로 표현한다.

<h2 style="text-align: center">
    $\mu = \mu_{ref} {\frac {T} {T_{ref}}}^{2/3} \frac{T_{ref} + T_s}{T + T_s} = \frac{A_s T^{2/3}}{T+T_s}$
</h2>

공기의 경우 $T_{ref}$=273.15K 일 때 $\mu_{ref}$=1.716e-5, $T_s$=110.4K, $A_s$=1.458e-6 이다.

Sutherland를 사용하면 Thermal Conductivity는 Chapman-Enskog approach로 계산하기 때문에 비활성화 된다.

<h2 style="text-align: center">
    $\kappa = \mu C_v \left(1.32+1.77 \frac {R}{C_v} \right)$
</h2>

#### Non-Newtonian Viscosity

Cross, Hershel-Bulkley, Carreau, Non-Newtonian-power-law 등은 비뉴턴유체(non-Newtonial fluid) 모델로, 물질이 액체이고 난류 모델이 laminar일 때만 사용할 수 있다. 각 모델은 다음의 식을 사용한다.

**Cross**

Cross power law 모델을 사용한다.

<h2 style="text-align: center">
    $\nu = \nu_\inf + \frac {\nu_0 - \nu_\infin}{1+(m \gamma)^n}$
</h2>

$\nu_0$ : zero shear viscosity

$\nu_\infin$ : infinite shear viscosity

$m$ : natural time

$n$ : power law index

$\gamma$ : shear strain rate

**Hershel-Bulkley**

<h2 style="text-align: center">
    $\nu = min (\nu_0 , \tau_0 / \gamma + k \gamma^^{n-1})$
</h2>

$\nu_0$ : zero shear viscosity

$\tau_0$ : yield stress threshold

$k$ : consistency index

$n$ : power law index

$\gamma$ : shear strain rate


**Carreau**

Bird-Carreau 모델을 사용한다.

<h2 style="text-align: center">
    $\nu = \nu_\infin + (\nu_0 - \nu_\infin )[1+(k \gamma)^a]^{\frac {n-1}{a}}$
</h2>

$\nu_0$ : zero shear viscosity

$\nu_\infin$ : infinite shear viscosity

$k$ : relaxation time

$n$ : power law index

$a$ : linearity deviation

$\gamma$ : shear strain rate


**Non-Newtonian-power-law**

<h2 style="text-align: center">
    $\nu = k \gamma ^{n-1}$
</h2>

$k$ : consistency index

$n$ : power law index

$\gamma$ : shear strain rate

이 모델은 최대, 최소 값인 $\nu_0$, $\nu_\infin$을 사용하여 값을 제한할 수 있다.


### Thermal Conductivity

Constant와 Polymomial을 선택할 수 있다.


### Molecular Weight

액체와 기체일 때만 나타난다.

### Absorption Coefficient

기체에서만 나타난다. 복사열전달 계산에만 사용된다.(현재는 불필요)

### Saturation Pressure

액체에서만 나타난다. 상변화 계산에 사용된다.(현재는 불필요)

### Emissivity

고체에서만 나타난다. 복사열전달 계산에만 사용된다.(현재는 불필요)


## Mixture의 물성값 설정 

Mixture의 물성값 수정 버튼을 누르면 아래 그림의 창이 나타난다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mixture-properties.png"><br> 물성값 설정
</p>

수정할 수 있는 항목은 Name, Density Spec., Specific Heat Spec., Transport Spec., Mass Diffusivity, Primary Specie 등이다.

### Density Spec.

Constant, Perfect Gas, Incompressible perfect gas, Polynomial을 선택할 수 있다. 에너지방정식을 풀지 않을 때와 액체나 고체일 때는 Constant만 사용할 수 있다.

Perfect Gas, Incompressible perfect gas를 선택한 경우 혼합물을 구성하는 각 물질의 밀도도 같은 값으로 설정된다.

Constant, Polynomial을 선택한 경우 혼합물을 구성하는 각 물질의 값을 설정해 준다. 혼합물의 밀도는 각 물질의 질량분율에 의해 결정된다.

### Specific Heat Spec.

Constant와 Polymomial을 선택할 수 있다. 혼합물을 구성하는 각 물질의 값을 설정해 준다. 혼합물의 값은 각 물질의 질량분율에 의해 결정된다.

### Transport Spec.

점성계수와 열전도도를 결정는 방법으로 Constant와 Polynomial, Sutherland를 선택할 수 있다.

Constant와 Polymomial을 선택한 경우 혼합물을 구성하는 각 물질의 viscosity와 thermal conductivity 값을 설정해 준다. Sutherland인 경우 각 물질의 Sutherland Coefficient(As)와 Sutherland Temperature(Ts)를 설정해 준다. 혼합물의 값은 각 물질의 질량분율에 의해 결정된다.

### Mass Diffusivity

현재는 상수로만 입력할 수 있다.

### Primary Specie

이 화학종에 대한 전달방정식은 계산하지 않고 1에서 나머지 화학종들의 질량분율 합을 뺀 값으로 결정된다.







