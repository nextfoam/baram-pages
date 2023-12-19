---
layout: post
title: 11. Boundary Condition
category: userguidelist
---

# Boundary Conditions

Navigation의 Boundary Conditions를 선택하면 Configuration에 아래 그림처럼 region 별로 경계면이 표시된다. 경계면을 선택하고 마우스 오른쪽 버튼을 누르면 경계조건을 설정할 수 있다. 경계면을 선택하면 그래픽창에 그 경계면이 붉은색으로 표시된다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/boundaryCondition.png"><br> Boundary Conditions
</p>

경계조건은 Inlet, Outlet, Wall, Misc의 4개 범주로 구분되어 있으며, 각 범주에는 다음과 같은 종류의 경계조건이 있다. 다상유동, 압축성유동 등의 조건에 따라 표시되는 것이 다르다. 경계면을 선택하고 더블 클릭을 하거나 Edit 버튼을 누르면 경계조건의 세부 설정창이 나타난다.

* Inlet

   + [Velocity Inlet](#velocity-inlet)
   
   + [Flow Rate Inlet](#flow-rate-inlet)
   
   + [Pressure Inlet](#pressure-inlet)
   
   + [ABL Inlet : 대기경계층 조건(Atmospheric Boundary Layer)](#abl-inlet)
   
   + [Free Stream](#free-stream)
   
   + [Open Channel Inlet : 다상유동 해석에만 사용](#open-channel-inlet)
   
   + [Far-field Riemann : 압축성유동 해석에만 사용](#far-field-riemann)
   
   + [Subsonic Inflow : 압축성유동 해석에만 사용](#subsonic-inflow)
   
   + [Supersonic Inflow : 압축성유동 해석에만 사용](#supersonic-inflow)
   
* Outlet

   + [Pressure Outlet](#pressure-outlet)
   
   + [Outflow](#outflow)
   
   + [Open Channel Outlet : 다상유동 해석에만 사용](#open-channel-outlet)
   
   + [Subsonic Outflow : 압축성유동 해석에만 사용](#subsonic-outflow)
   
   + [Supersonic Outflow : 압축성유동 해석에만 사용](#supersonic-outflow)
   
* Wall

   + [Wall](#wall)
   
   + [Thermo-Coupled Wall](#thermo-coupled-wall)
   
* Misc.

   + [Symmetry](#symmetry)
   
   + [Interface](#interface)
   
   + [Empty](#empty-wedge)
   
   + [Cyclic](#cyclic)
   
   + [Wedge](#empty-wedge)
   
   + [Porous Jump](#porous-jump)
   
   + [Fan ](#fan)
<br>

## Velocity Inlet

Velocity Inlet 조건은 유동의 입구에 속도, 난류, 온도 값을 주는 조건이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/velocityInlet.png"><br> Velocity Inlet 설정
</p>

속도는 x, y, z 속도 성분을 주는 방법과(Component) 경계면에 수직한 속도를 주는 방법이(Magnitude, Normal to Boundary) 있다.

난류는 난류 필드의 값을(k, epsilon, omega, nuTilda) 주는 방법과 intensity/viscosity ratio를 주는 방법이 있다. Spalart-Allmaras 모델에서는 난류 필드의 값인 Modified Turbulent Viscosity(nuTilda)를 주는 방법만 지원한다.

온도는 일정한 값을 준다.

각 필드가 사용하는 openfoam의 경계조건은 다음과 같다.

* 속도 : Componet일 때는 fixedValue, Magnitude일 때는 surfaceNoramlVelocity

* 압력 : zeroGradient

* 온도 : fixedValue

* k : turbulentIntensityInletOutletTKE (넥스트폼이 개발)

* epsilon, omega : viscosityRatioInletOutletTDR (넥스트폼이 개발)

* nuTilda : fixedValue
<br>

### boundary profile 조건 설정

Velocity Inlet 조건에서 속도와 온도를 시간에 따른 변화(temporal) 혹은 공간 상의 분포(spatial)로 지정할 수 있다.


#### Temporal Distribution

Velocity Inlet 조건에서 속도의 Profile Type을 Temporal Distribution으로 선택하면 아래 그림의 창에서 Piecewise linear를 사용하여 지정할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/profile.png"><br> Temporal Distribution 조건 설정
</p>

Velocity Inlet 조건에서 온도의 Profile Type을 Temporal Distribution으로 선택하면 Piecewise linear와 Polynomial로 지정할 수 있다. Polynomial은 아래 그림의 창에서 식의 계수 *a<sub>n</sub>*들을 지정한다.

<h2 style="text-align: center">
$S = a_0 \cdot t^0 + a_1 \cdot t^1 + a_2 \cdot t^2 + ... + a_n \cdot t^n$
</h2>
<br/>

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/polynomial.png">
    <br/>
    Temporal Distribution 조건 설정 - polynomial
</p>
<br/>

#### Spatial Distribution

Velocity Inlet 조건에서 속도나 온도의 Profile Type을 Spaticl Distribution으로 선택하면 csv 파일을 선택할 수 있다. Velocity Inlet 조건에서 Velocity Specification Method가 Magnitude, Normal to Boundary인 경우는 속도에 대해 적용할 수 없다.

csv 파일은 (x좌표, y좌표, z좌표, value)의 값이 ","로 구분되어 씌어져 있어야 한다. velocityInlet 조건에서 속도는 다음과 같은 형식이 된다.(x, y, z, Ux, Uy, Uz) 

0.0, 0.0, 0.0, 0.1, 0.2, 0.0

0.0, 0.7, 0.0, 0.1, 0.3, 0.0

0.0, 1.2, 0.0, 0.1, 0.4, 0.0

...
<br>

## Flow Rate Inlet

Flow Rate Inlet 조건은 유동의 입구에 유량, 난류, 온도 값을 주는 조건이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/flowrate.png"><br> Flow Rate Inlet 설정
</p>

유량은 질량유량(mass flow rate)과 체적유량(volume flow rate)을 줄 수 있으며 난류와 온도는 Velocity Inlet 조건과 동일하게 준다.

속도(U)가 사용하는 openfoam의 경계조건은 flowRateIneltVelocity이며 압력, 난류, 온도는 Velocity Inlet 조건과 동일하다. 
<br>

## Pressure Inlet

Pressure Inlet 조건은 유동의 입구에 전압력(total pressure)과 난류, 온도 값을 주는 조건이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/pressureInlet.png"><br> Pressure Inlet 설정
</p>

전압력은 상수로 줄 수 있으며 난류와 온도는 Velocity Inlet 조건과 동일하게 준다.

openfoam의 경계조건은 압력은 totalPressure, 속도는 pressureInletOutletVelocity를 사용한다.
<br>

## ABL Inlet

ABL(Atmospheric Boundary Layer) Inlet 조건은 유동의 입구에 대기경계층의 속도와 난류 분포를 주는 조건이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/ablInlet.png"><br> ABL Inlet 설정
</p>

입력 항목은 다음과 같다.

* Flow Direction : 바람의 방향 벡터

* Ground-Normal Direction : 지표면에 수직한 벡터

* Reference Height, z<sub>ref</sub>

* Reference Flow Speed, U<sub>ref</sub> : Reference Height에서의 속도

* Surface Roughness Length, z<sub>0</sub>

* Minimum z-coordinate, d : 지표면의 높이 방향 좌표(지표면에서 높이가 z-d 로 계산됨)


속도와 난류 분포는 다음의 식을 사용한다.

<h2 style="text-align: center">
$u = \frac{u^*}{\kappa} ln\left(\frac{z - d + z_0}{z_0}\right)$
</h2>

<h2 style="text-align: center">
$k = \frac{(u^* )^2}{\sqrt{C_\mu}} \sqrt{C_1 ln \left( \frac{z - d + z_0}{z_0} \right) + C_2}$
</h2>

<h2 style="text-align: center">
$\epsilon = \frac{(u^* )^3}{\kappa (z - d + z_0)} \sqrt{C_1 ln \left( \frac{z - d + z_0}{z_0} \right) + C_2}$
</h2>

<h2 style="text-align: center">
$\omega = \frac{u^*}{\kappa \sqrt{C_\mu}} \frac{1}{z - d + z_0}$
</h2>

<h2 style="text-align: center">
$u^* = \frac{u_{ref} \kappa} {ln \left( \frac{z_{ref} + z_0}{z_0} \right)}$
</h2>
<br/>


변수정의

* _z_ : 수직 방향 좌표

* _κ_ : Von Karman's constant, 0.41

* _C<sub>μ</sub>_ : constant, 0.09

* _C<sub>1</sub>_ : constant, 0

* _C<sub>2</sub>_ : constant, 1



각 필드가 사용하는 openfoam의 경계조건은 다음과 같다.

* 속도 : atmBoundaryLayerInletVelocity

* 압력 : zeroGradient

* k : atmBoundaryLayerInletK

* epsilon, omega : atmBoundaryLayerInletEpsilon, atmBoundaryLayerInletOmega
<br>

## Free Stream

Free Stream 조건은 유동이 도메인으로 들어오는 경우는 일정한 속도를, 나가는 경우는 속도 구배가 0이 되는 조건이다. 비압축성 외부 유동의 원방 경계조건으로 많이 사용된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/freestream.png"><br> Free Stream 설정
</p>

Free Stream Velocity는 속도 벡터를 입력하고 압력은 상수로 주며 난류와 온도는 Velocity Inlet 조건과 동일하게 준다.

각 필드가 사용하는 openfoam의 경계조건은 다음과 같다.

* 속도 : freestreamVelocity

* 압력 : freestreamPressure

* 온도 : freestream

* 난류 : freestream
<br>

## Open Channel Inlet

Open Channel Inlet 조건은 자유수면을 계산할 때 입구에 일정한 유량을 주고 그에 따라 수면의 높이가 변할 수 있는 조건이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/openChannelInlet.png"><br> Open Channel Inlet 설정
</p>

체적유량을 상수로 입력하고, 난류는 Velocity Inlet 조건과 동일하게 준다.

각 필드가 사용하는 openfoam의 경계조건은 다음과 같다.

* 속도 : variableHeightFlowRateInletVelocity

* 압력 : zeroGradient

* 체적분율 : variableHeightFlowRate

* k : turbulentIntensityInletOutletTKE (넥스트폼이 개발)

* epsilon, omega : viscosityRatioInletOutletTDR (넥스트폼이 개발)

* nuTilda : fixedValue
<br>

## Far-field Riemann

압축성 유동의 원방경계에 사용하는 Riemann 경계조건이다.(넥스트폼이 개발)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/riemann.png"><br> Far-field Riemann 설정
</p>

유동의 방향 벡터, 원방에서의 마하수, 압력(static pressure), 온도(static temperature)를 입력하고, 난류는 Velocity Inlet 조건과 동일하게 준다.

속도, 압력, 온도의 openfoam 경계조건은 farfieldRiemann이며 난류는 Velocity Inlet 조건과 동일하다.
<br>

## Subsonic Inflow

Subsonic Inflow 조건은 압축성 유동에서 유체기계와 같은 내부유동의 입구 아음속 경계조건이다.(넥스트폼이 개발)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/subsonicInflow.png"><br> Subsonic Inflow 설정
</p>

유동의 방향 벡터, 전압력(total pressure), 전온도(total temperature)를 입력하고, 난류는 Velocity Inlet 조건과 동일하게 준다.

속도, 압력, 온도의 openfoam 경계조건은 subsonicInflow이며 난류는 Velocity Inlet 조건과 동일하다.
<br>

## Supersonic Inflow

Supersonic Inflow 조건은 유동의 입구가 초음속인 경우 사용하는 경계조건이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/supersonicInflow.png"><br> Supersonic Inflow 설정
</p>

속도 벡터, 압력(static pressure), 온도(static temperature)를 입력하고, 난류는 Velocity Inlet 조건과 동일하게 준다.

속도, 압력, 온도의 openfoam 경계조건은 fixedValue이며 난류는 Velocity Inlet 조건과 동일하다.
<br>

## Pressure Outlet

Pressure Outlet 조건은 출구 경계면에 일정한 전압력을(Total Pressure) 주는 조건이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/pressureOutlet.png"><br> Pressure Outlet 설정
</p>

전압력(total pressure)를 입력하고 유동이 유입될 때의 조건을 옵션으로 선택한다. 'Calculate Backflow' 옵션을 선택하면 유입되는 유동의 전온도(total temperature)와 난류 조건을 줄 수 있다.

각 필드가 사용하는 openfoam의 경계조건은 다음과 같다.

* 속도 : pressureInletOutletVelocity

* 압력 : totalPressure

* 온도 : zeroGradient(Calculate Backflow 옵션을 사용하지 않을 때) 혹은 inletOutletTotalTemperature

* k : zeroGradient(Calculate Backflow 옵션을 사용하지 않을 때) 혹은 turbulentIntensityInletOutletTKE (넥스트폼이 개발)

* epsilon, omega : zeroGradient(Calculate Backflow 옵션을 사용하지 않을 때) 혹은 viscosityRatioInletOutletTDR (넥스트폼이 개발)

* nuTilda : zeroGradient(Calculate Backflow 옵션을 사용하지 않을 때) 혹은 inletOutlet
<br>

## Open Channel Outlet

Open Channel outlet 조건은 자유수면을 계산할 때 출구에 일정한 평균 속도를 주고 그에 따라 수면의 높이가 변할 수 있는 조건이다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/openChannelOutlet.png"><br> Open Channel Outlet 설정
</p>

평균 속도를 상수로 입력하고, 난류는 Velocity Inlet 조건과 동일하게 준다.

각 필드가 사용하는 openfoam의 경계조건은 다음과 같다.

* 속도 : outletPhaseMeanVelocity

* 압력 : zeroGradient

* 체적분율 : variableHeightFlowRate

* k : turbulentIntensityInletOutletTKE (넥스트폼이 개발)

* epsilon, omega : viscosityRatioInletOutletTDR (넥스트폼이 개발)

* nuTilda : zeroGradient
<br>

## Outflow

Outflow 조건은 출구의 모든 필드에 대해 zero gradient 조건을 사용한다.
<br>

## Subsonic Outflow

Subsonic Outflow 조건은 압축성 유동에서 유체기계와 같은 내부유동의 출구 아음속 경계조건이다.

압력(static pressure)을 입력한다. 

속도, 압력, 온도의 openfoam 경계조건은 subsonicOutflow이며 난류는 zeroGradient이다. 
<br>

## Supersonic Outflow

Supersonic Outflow 조건은 압축성 유동의 초음속 출구 경계조건이다.

입력할 것은 없으며, 모든필드의 openfoam 경계조건은 zero gradient이다.
<br>

## Wall

Wall은 유동이 통과하지 못하는 벽면을 의미하며 벽면의 운동에 의한 속도조건과 온도조건을 지정할 수 있다. 압력과 난류는 별도의 조건 설정이 필요없다.
<br>

### 속도 조건

속도 조건은 No Slip, Slip, Moving Wall, Atmospheric Wall, Translational Moving Wall, Rotational Moving Wall 조건을 선택할 수 있다. 

No Slip 조건은 벽변 점착 조건으로 속도가 (0, 0, 0)으로 설정된다. Slip은 마찰이 없는 벽면으로 벽면에 수식한 속도 성분이 없다는 조건이다. <span style="color:blue">Moving Wall은 움직이는 물체에 대한 조건으로 Sliding Mesh와 같은 이동격자계를 사용할 때 움직이는 물체에 적용된다</span>. Atmospheric Wall은 대기경계층 문제에서 지표면에 사용된다. nut의 벽함수로 nutkAtmRoughWallFunction이 사용된다. Translational Moving Wall과 Rotational Moving Wall은 격자가 움직이지는 않지만 벽면이 일정한 속도로 움직이고 있다는 것으로 벽에서의 속도는 벽면의 이동속도와 같게 된다.

### 온도 조건

온도 조건은 Adiabatic, Constant Temperature, Constant Heat Flux, Convection 조건을 선택할 수 있다.

* Adiabatic : 단열 조건으로 별도로 설정할 것은 없다. 복사열전달이 없는 경우는 온도 경계조건으로 zeroGradient를 사용한다. 복사열전달이 있는 경우는 복사를 포함한 열유속이 0이라는 조건을 사용한다(externalWallHeatFluxTemperature)

* Constant Temperature : 온도가 일정한 조건이다. fixedValue 조건을 사용한다.

* Constant Heat Flux : 열유속이 일정한 조건이다. externalHextFluxTemperature 조건을 사용한다.(넥스트폼이 수정)

* Convection : 일정한 외부 온도와 열전달계수를 사용하는 조건이다. externalHextFluxTemperature 조건을 사용한다.(넥스트폼이 수정)

### 난류 경계조건

벽에서의 난류 조건은 벽함수(wall function)을 사용한다.

* k : kqRWallFunction

* epsilon : epsilonWallFunction

* omega : omegaWallFunction

* nuTilda : zeroGradient

* nut : nutkWallFunction(k-epsilon 모델일 때), nutUSpaldingWallFunction(SST k-omega, Spalart-Allmaras 모델일 때)

* alphat : compressible::alphatWallFunction
<br>

## Thermo-Coupled Wall

Thermo-Coupled Wall 조건은 계산 영역 내부에 있는 두께가 없는 벽면(baffle)에 대한 조건이다. baffle은 master와 slave 2개의 경계면이 쌍을 이루고 있으며 모두 thermo-coupled wall 조건을 사용한다.

각 필드가 사용하는 openfoam의 경계조건은 다음과 같다.

* 속도 : noSlip

* 압력 : fixedFluxPressure

* 온도 : turbulentTemperatureCoupledBaffleMixed (넥스트폼이 수정)

* 난류 : Wall과 같은 조건 사용
<br>

## 기타 경계조건 - Misc

### Empty, Wedge

OpenFOAM은 별도의 2차원 격자가 없으며 3차원 격자의 높이 방향으로 하나의 격자가 있을 때 그 위, 아래면에 empty 조건을 주면 2차원 문제가 된다. 마찬가지로 축대칭 격자도 없으며 wedge 모향의 3차원 격자에 회전방향으로 하나의 격자가 있을 때 그 양쪽면에 wedge 조건을 주면 축대칭 문제가 된다.

### Symmetry

대칭 조건의 경계면에 사용한다. 

### Interface

2개 경계면의 관계를 나타내는 조건이다. 계산 영역 내부의 두께가 없고 유동이 통과하는 경계면이나 cell zone 경계면에서 같은 위치에 2개의 경계면이 있을 때 사용한다. 쌍을 이루는 2개 경계면의 격자는 일치할 필요는 없다.

Internal Interface, Rotational Periodic, Translational Periodic의 3가지가 있다.

openfoam의 cyclicAMI 조건을 사용한다.

### Cyclic

interface와 같은 기능을 하지만 2개의 쌍을 이루는 격자가 완전히 일치해야 한다.

### Porous Jump

Porous Jump 조건은 계산영역 내부에 있는 cyclic 면에서 압력 변화를 주는 조건이다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/porousJump.png"><br> Porous Jump 설정
</p>

입력항목은 다음과 같다.

* Darcy Coefficient, D

* Inertial Coefficient, I

* Porous media thickness, L

* Coupled boundary

압력 변화는 다음 식으로 계산된다. _μ_는 점성계수, _ρ_는 밀도, _U_는 속도이다.

<!--
<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/eqn_porousJump.png"><br>
</p>
-->
<h2 style="text-align: center">
$\Delta p = -\left(D \mu U + \frac{1}{2} I \rho U^2 \right)L$
</h2>
<br/>

openfoam에서 사용하는 경계조건은 압력은 porousBafflePressure이고, 나머지는 모두 cyclic이다.

### Fan

fan 조건은 계산영역 내부에 있는 cyclic 면에 팬의 압력-유량 곡선(P-Q curve)을 파일로 주는 조건이다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/fan.png"><br> Fan 설정
</p>

압력-유량 곡선(P-Q curve)을 파일은 csv 형식으로 첫번째 열에 압력, 두번째 열에 유량이 적힌 텍스트 파일이면 된다.

openfoam에서 사용하는 경계조건은 압력은 fanPressureJump이고, 나머지는 모두 cyclic이다.

