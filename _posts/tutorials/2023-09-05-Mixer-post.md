---
layout: post
title: 03. Mixer
category: tutorials
---

# 03. Mixer 

* [격자 파일](https://drive.google.com/file/d/1Bop5tSUOdzj3twkmJtvLKBqwX8sAW2Dk/view?usp=sharing)

## 1) 개요 
* 본 예제는 정상상태 비압축성 유동해석 예제이다.<br>

* 용기 내부의 폐쇄 영역에서 임펠러가 회전할 때 내부의 유동을 예측하는 문제이다. <br>

* 임펠러는 두께가 없는 면인 baffle로 처리한다.<br>

* 임펠러 개수는 4개인데 회전주기조건을 사용해서 4분의 1만 모델링하였다.<br>

* 그림 3.1에서 형상과 격자를 나타내었다.<br>

<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.1.png"><br>
    그림 3.1
</p>

계산 조건은 다음과 같다. <br>

●  solver : SimpleNFoam (넥스트폼이 개발한 정상상태 비압축성 해석 솔버) <br>

●  난류 모델 : Realizable 𝑘 − ε<br>

●  밀도 : 1,000𝑘𝑔/㎥ <br>

●  점성 계수 : 0.001𝑘𝑔/𝑚s <br>

●  임펠러 회전 수 : 100RPM  <br>

BARAM을 실행하면 아래 과정을 따라서 case 파일을 만든다.<br>

●  New Case버튼 클릭<br>

●  Project Name : Mixer<br>

●  Flow Type : incompressible<br>

●  Multiphase Model : Off<br>

● Species Model : Not Include<br>

## 2) 격자
격자는 주어진 polyMesh 폴더를 활용한다. <br>
상단 탭에서 File - Load Mesh - OpenFOAM 순서대로 클릭하고 polyMesh 폴더를 선택한다. <br>

<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.2.png"><br>
    그림 3.2
</p>

## 3) 계산 조건
### (1) General
본 예제에서는 Default로 설정한다.<br>

### (2) Models
난류 모델은 Realizable 𝑘 − ε 모델을 사용하고 나머지는 Default를 사용한다. <br>

<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.3.png"><br>
    그림 3.3
</p>

### (3) Materials
본 예제에서 작동 유체는 물이다.<br>
유체의 이름과 물성치를 아래와 같이 변경한다.<br>

***●  water***<br>
```Density : 1000𝑘𝑔/㎥ (m/s)```  <br>
```Viscosity : 0.001𝑘𝑔/𝑚s```  <br>

<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.4.png"><br>
    그림 3.4
</p>

### (4) Cell Zone Conditions
Cell Zone Conditions에서는 MRF, Sliding Mesh, Source 등을 설정할 수 있다.<br>
본 예제에서는 'rot' Cell Zone에 MRF 조건을 설정한다.<br>

rot 선택 - Multiple Reference Fram, MRF를 선택하고 아래 값들을 입력한다.<br>

***●  Multiple Reference Frame***<br>
```Rotating Speed : 100(RPM)```<br>
```Rotation-Axis Origin : (0, 0, 0)```<br>
```Rotation-Axis Direction : (0, 0, 1)```  <br>
```Static Boundary : per1, per2, hub```  <br>


<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.5.png"><br>
    그림 3.5
</p>

### (5) Boundary Conditions
아래와 같이 경계면 타입과 경계값을 설정한다.<br>

**※per1, per2는 각각 회전 주기의 경계면이다.<br>**

***●  per1, per2 : Interface - Rotational Periodic***<br>
```per1 : Rotational Periodic으로 변경 후, Coupled Boundary는 per2 선택```<br>

***●  top : Symmetry***<br>

***●  imp_master, imp_slave : Thermo-Coupled Wall***<br>
```imp_master : Thermo-Coulped Wall로 변경 후, Coupled Boundary는 per2 선택```<br>

***●  나머지 : Wall***<br>
```Velocity Condition : No Slip```<br>

<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.6.png"><br>
    그림 3.6
</p>

### (6) Numerical Conditions
본 예제에서는 아래와 같이 설정을 변경한다. <br>

●  Pressure-Velocity Coupling Scheme : SIMPLEC <br>

●  Discretization Scheme  <br>
```Momentum : Second Order Upwind``` <br>
```Turbulence : First Order Upwind``` <br>

●  Under-Relaxation Factors  <br>
```Pressure : 0.3```<br>
```Momentum : 0.7```<br>
```Turbulence : 0.7```<br>
```Density : 0.9``` <br>

●  Convergence Criteria  <br>
```Pressure : 0.001``` <br>
```Momentum : 0.001``` <br>
```Turbulence : 0.001``` <br>

<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.7.1.png"><br>
    그림 3.7.1
</p>

<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.7.2.png"><br>
    그림 3.7.2
</p>

### (7) Initialization
본 예제에서는 Default값으로 초기화를 한다.<br>
하단에 Initializer 버튼을 클릭한다. 그 후, File - Save 버튼을 클릭하여 case 파일을 저장한다. <br>

### (8) Run
Run Conditions에서 다음과 같이 설정 후 계산을 진행한다.<br>

●  Number of Iterations : 2,000  <br>

●  Save Interval : 500  <br>

●  Data Write Format : Binary  <br>

●  Number of Cores : 4  <br>

<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.8.png"><br>
    그림 3.8
</p>

아래 그림은 Residuals 그래프이다.
<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.9.png"><br>
    그림 3.9
</p>

## 4) 후처리

### (1) 축 단면 벡터 분포
용기 내부의 속도 벡터를 보는 과정을 진행한다.<br>
paraview 아이콘을 클릭하여 paraview를 실행한다.<br>

Case Type을 Decomposed Case로 변경한다.

<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.10.png"><br>
    그림 3.10
</p>

Slice 기능을 활용하여 용기 내부의 단면을 자른다.<br>

Z-normal 버튼을 클릭 후, Origin을 다음과 같이 변경한다.<br>
●  Origin : 0.5 0.5 0.9  <br>

<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.11.png"><br>
    그림 3.11
</p>

<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.12.png"><br>
    그림 3.12
</p>

이후, Glyph 버튼을 선택하고 아래와 같이 설정을 변경한다.<br>

<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.13.png"><br>
    그림 3.13
</p>

아래 그림과 같이 용기 내부 벡터가 나오게 된다.

<p align='center'>
    <img src="https:nextfoam.co.kr/baramManual/mixer/3.14.png"><br>
    그림 3.14
</p>