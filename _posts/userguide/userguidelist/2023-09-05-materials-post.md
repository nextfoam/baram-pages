---
layout: post
title: 09. Materials
category: userguidelist
---

# Setup - Materials

BARAM은 몇가지 물질들의 물성값을 데이터베이스로 제공한다. 해석에 사용할 물질들을 추가하고, 필요하다면 물성값을 수정해서 사용할 수 있다. 아래 그림 오른쪽상단의 (+)버튼을 누르면 물질을 추가 할 수 있다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/material.png"><br> Material 설정
</p>

BARAM이 제공하는 물질 데이터베이스는 다음과 같다.

* Gas : Air, Oxygen, Nitrogen, Carbon-dioxide, Hydrogen, Argon, Carbon-monoxide, Methane, Water-vapor

* Liquid : Water-liquid

* Solid : Steel, Concrete, Aluminum, Copper


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


