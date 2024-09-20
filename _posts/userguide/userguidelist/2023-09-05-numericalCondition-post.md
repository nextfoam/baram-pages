---
layout: post
title: 09. Numerical Conditions
category: userguidelist
---

# Numerical Conditions

해석에 사용되는 수치해석 조건들을 설정한다.

## Pressure-Velocity Coupling Scheme

SIMPLE과 SIMPLEC를 선택할 수 있으며, fvSolution 파일의 SIMPLE 딕셔너리의 consistent에 적용된다. SIMPLEC를 사용할 때 relaxation factor를 0.9 이상의 값으로 설정해서 수렴 속도를 높일 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/scheme00.png"><br> Pressure-velocity coupling scheme 설정
</p>

## Momentum Predictor

비정상상태(transient)일 때만 나타난다.

레이놀즈 수가 낮은 유동이나 다상유동 문제에서 momentum predcitor를 끄면 안정성이 향상되는 경우가 있다.

## Formulation

밀도 기반 압축성 솔버(Solver Type을 Density-based로 선택)에서만 나타난다. 현재 Implicit만 선택할 수 있다.

## Flux Type

밀도 기반 압축성 솔버(Solver Type을 Density-based로 선택)에서만 나타난다. 

Roe-FDS, AUSM, AUSM-up 3가지를 선택할 수 있다.

Roe-FDS를 선택하면 Entropy Fix Coefficient, $\epsilon$을 입력할 수 있다. 0~1 사이의 값을 입력한다.

AUSM-up를 선택하면 Cut-off Mach Number, $M_\inf$를 설정할 수 있다. 0~10 사이의 값을 입력한다.

AUSM을 선택하면 별도의 설정이 없다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/scheme0.png"><br> Flux Type 설정
</p>

## Discretization Schemes

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/scheme1.png"><br> Discretization Schemes 설정
</p>

### Pressure

Cell 중심의 압력으로부터 face의 압력을 계산하는 interpolation 기법을 선택하는 것으로 Linear, Momentum Weighted Reconstruct, Momentum Weighted를 선택할 수 있다. 

Linear : face 양쪽의 cell 중심값을 사용하여 linear interpolation하는 방법으로 안정성이 뛰어나다. MRF나 porous 모델과 같은 운동량 소스가 있는 경우 linear 기법의 사용을 권장한다.

Momentum Weighted : 운동량방정식의 계수($a_p$)를 weighting factor로 사용하는 방법으로 수렴성이 뛰어니다. 운동량 소스가 있는 경우 안정성에 문제가 있을 수 있다.

Momentum Weighted Reconstruct : second order 기법이라고 할 수 있는데 cell 중심의 압력구배를 이용한 extrapolation으로 face 좌우의 값을 계산하고 이를 평균해서 face 값으로 사용하는 방법이다. 평균은 운동량방정식의 계수($a_p$)를 weighting factor로 사용한다. 보다 정확한 결과를 얻을 수 있는 대신 안정성이 낮아질 수 있다.

### Time, Momentum, Energy, Turbulence, Volume Fraction

First order와 second order를 선택할 수 있다. fvSchemes 파일의 ddtSchemes와 divSchemes 딕셔너리에 사용된다.

Time은 first order일 때 Euler를 사용하고 second order일 때 backward를 사용한다.(넥스트폼이 수정)

Momentum, Turbulence, Energy는 first order upwind일 때 Gauss upwind를 사용하고, second order일 때는 Gauss linearUpwind와 <span style="color:blue">Venkatakrishnan’s limiter(넥스트폼이 개발)</span>을 사용한다.

## Under-Relaxation Factors

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/relaxation.png"><br> Under-Relaxation Factors 설정
</p>

정상상태에서는 default 값만, 비정상상태에서는 default 값과 final 값을 입력한다. fvSolution 파일의 relaxationFactors에 해당한다. 값이 클수록 수렴 속도가 빨라질 수 있으나 불안정해질 수 있다. SIMPLEC를 사용하는 경우 0.9 이상의 값을 추천한다.

밀도 기반 압축성 솔버를 사용할 때는 Turbulence 부분만 활성화 된다.

## Improve Stability

안정성 향상을 위해 laplacian scheme에 사용된다. 옵션을 끄면 fvSchemes.laplacianScheme은 "Gauss linear corrected"를 사용하고, 옵션이 켜지면 "Gauss linear limited corrected [limiting factor]를 사용한다. Limiting factor 값이 크면 좀 더 안정적이지만 정확도가 떨어질 수 있다.

## Max Iterations per Time Step, Number of Correctors

’Max Iterations per Time Step’은 비정상상태 계산에서 각 time step에서 수행할 최대 반복계산(iteration) 회수를 의미하며, ’Number of Correctors’는 각 반복계산마다 압력방정식을 몇번 계산할 것인지이다. fvSolution.PIMPLE 딕셔너리의 nOuterCorrectors와 nCorrectors에 적용된다.

## Multiphase

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/multiphase.png"><br> Multiphase 설정
</p>

’Max Iterations per Time Step’은 비정상상태 계산에서 각 time step에서 수행할 alpha(volume fraction) 방정식의 최대 반복계산(iteration) 회수를 의미하며, ’Number of Correctors’는 각 반복계산마다 alpha(volume fraction) 방정식을 몇번 계산할 것인지이다. fvSolution 파일의 solvers-alpha(volume fraction)의 nAlphaSubCycles과 nAlphaCorr 값이다.

MULES Variant는 MUlti-dimensionsal Limiter for Explicit Solution의 방법을 선택하는 것으로 fvSolution 파일의 solvers-alpha(volume fraction)의 MULESCorr 값이다. explicit이면 no, semi-implicit이면 yes이다.

Phase Interface Compression Factor는 상의 경계면 압축을 제어하는 요소이다. 0은 압축이 없음을 1은 보존적 압축에 해당된다. 값이 클수록 경계면이 얇게 포착되지만 불안정해 질 수 있다. fvSolution 파일의 solvers-alpha(volume fraction)의 cAlpha 값이다.

Number of MULES iterations over the limiter는 limiter에 대한 MULES 반복 횟수로, fvSolution 파일의 solvers-alpha(volume fraction)의 nLimiterIter 값이다.

## Convergence Criteria

Convergence Criteria는 각 필드의 수렴 조건을 나타낸다. fvSolution 파일의 SIMPLE 혹은 PIMPLE 딕셔너리의 residualControl에 해당한다. absolute 값들은 tolerance에 적용되고 비정상상태에서 활성화되는 relative는 relTol에 적용된다.

## Advanced

Limits와 Equations 두 가지로 구성된다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/limit.png"><br> Advanced 설정
</p>

### Limits

Limits의 값은 계산의 안정성을 위해 최소와 최대값을 제한한다. 온도와 Viscosity Ratio를 제한할 수 있다. 

온도의 제한은 fvOptions의 limitTemperature를 사용한다.

Maximum Viscosity Ratio는 turbulenceProperties 파일의 난류모델 딕셔너리에 설정된다. 디폴트는 1e5이며 값이 작을 때 안정성이 좋아지는 경우가 있으나 결과의 정확도에 문제가 될 수도 있다.

### Equations

유동, 에너지, 사용자 정의 함수, 화학종 등의 방정식을 on/off 할 수 있다. 

에너지방정식은 Viscous dissipation, Kinetic energy, Pressure Work 항을 각각 on/off할 수 있다. 이들의 영향이 매우 작은 경우 생략하게 되면 안정성 향상 효과를 볼 수 있다. 고속, 고온, 고점도 유동의 경우 생력하면 정확도에 문제가 있을 수 있다.

Sliding mesh를 사용하는 경우 모든 것을 off 하고 계산하면 격자의 운동이 제대로 구현되는지 확인할 수 있다.














