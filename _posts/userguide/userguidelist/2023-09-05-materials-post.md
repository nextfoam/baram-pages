---
layout: post
title: 09. Materials
category: userguidelist
---

# Setup - Materials

## Model에서 Species가 Not Include인 경우

BARAM은 몇가지 물질들의 물성값을 데이터베이스로 제공한다. 해석에 사용할 물질들을 추가하고, 필요하다면 물성값을 수정해서 사용할 수 있다. 

BARAM이 제공하는 물질 데이터베이스는 다음과 같다.

* Gas : Air, Oxygen, Nitrogen, Carbon-dioxide, Hydrogen, Argon, Carbon-monoxide, Methane, Water-vapor

* Liquid : Water-liquid

* Solid : Steel, Concrete, Aluminum, Copper

아래 왼쪽 그림 오른쪽상단의 (+)버튼을 누르면 가운데 그림과 같은 창이 나타나고 물질을 추가 할 수 있다. 오른쪽 그림은 oxygen이 추가된 결과이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/material.png"><br> Material 설정
</p>

물성값 수정 버튼을 누르면 아래 그림의 창이 나타난다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/materialProperties.png"><br> 물성값 설정
</p>

수정할 수 있는 항목은 Name, Density, Specific Heat, Viscosity, Thermal Conductivity, Molecular Weight, Absorption Coefficient, Saturation Pressure, Emissivity 등이며 기체/액체/고체에 따라서 그리고 에너지방정식을 계산하는지에 따라서 항목들이 조금씩 달라진다.

* Density : Constant, Perfect Gas, Polynomial을 선택할 수 있다. 에너지방정식을 풀지 않을 때와 액체나 고체일 때는 Constant만 사용할 수 있다.

* Specific Heat : Constant와 Polymomial을 선택할 수 있다.

* Viscosity
    * Constant, Sutherland, Polynomial을 선택할 수 있다.
    * 고체는 Viscosity가 없으며 Sutherland는 기체만 선택할 수 있다.
    * Sutherland는 에너지방정식을 풀 때만 사용할 수 있으며 Sutherland Coefficient와 Sutherland Temperature를 입력한다.
    * Sutherland를 사용하면 Thermal Conductivity는 Chapman-Enskog approach로 계산하기 때문에 비활성화 된다.
    * <span style="color:gray">비뉴턴유체(non-Newtonial fluid) 모델은 아직 지원하지 않으며 곧 지원할 계획이다.</span>

* Thermal Conductivity : Constant와 Polymomial을 선택할 수 있다.

* Molecular Weight : 액체와 기체일 때만 나타난다.

* Absorption Coefficient : 기체에서만 나타난다. 복사열전달 계산에만 사용된다.(현재는 불필요)

* Saturation Pressure : 기체에서만 나타난다. 캐비테이션 계산에만 사용된다.(현재는 불필요)

* Emissivity : 고체에서만 나타난다. 복사열전달 계산에만 사용된다.(현재는 불필요)


## Model에서 Species가 Include인 경우 

아래 왼쪽 그림 오른쪽상단의 (+) 버튼을 누르면 아래 가운데 그림처럼 'Create Mixture'라는 버튼이 나타난다. 여러 개의 화학종을 선택하고 이 버튼을 누르면, 오른쪽 그림과 같이 mixture가 추가된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/material-mixture.png"><br> Mixture material 설정
</p>

Mixture의 물성값 수정 버튼을 누르면 아래 그림의 창이 나타난다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mixture-properties.png"><br> 물성값 설정
</p>

수정할 수 있는 항목은 Name, Density Spec., Specific Heat Spec., Transport Spec., Mass Diffusivity, Primary Specie 등이다.

* Density Spec. : Constant, Perfect Gas, Incompressible perfect gas, Polynomial을 선택할 수 있다. 에너지방정식을 풀지 않을 때와 액체나 고체일 때는 Constant만 사용할 수 있다.

* Specific Heat Spec. : Constant와 Polymomial을 선택할 수 있다.

* Transport Spec. : Constant와 Polynomial, Sutherland를 선택할 수 있다.

* Mass Diffusivity : 현재는 상수로만 입력할 수 있다.

* Primary Specie : 이 화학종에 대한 전달방정식은 계산하지 않고 1에서 나머지 화학종들의 질량분율 합을 뺀 값으로 결정된다.







