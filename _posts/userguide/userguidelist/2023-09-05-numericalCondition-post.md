---
layout: post
title: Numerical Conditions
category: userguidelist
---

# Numerical Conditions

해석에 사용되는 수치해석 조건들을 설정한다.

## Pressure-Velocity Coupling Scheme

SIMPLE과 SIMPLEC를 선택할 수 있으며, fvSolution 파일의 SIMPLE 딕셔너리의 consistent에 적용된다. SIMPLEC를 사용할 때 relaxation factor를 0.9 이상의 값으로 설정해서 수렴 속도를 높일 수 있다.

## Momentum Predictor

레이놀즈 수가 낮은 유동이나 다상유동 문제에서 momentum predcitor를 끄면 안정성이 향상되는 경우가 있다.

## Discretization Schemes

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/scheme1.png"><br> Discretization Schemes 설정
</p>

Time, momentum, energy, turbulence, volume fraction의 이산화 기법을 선택한다. First order와 second order를 선택할 수 있다. fvSchemes 파일의 ddtSchemes와 divSchemes 딕셔너리에 사용된다.

Time은 first order일 때 Euler를 사용하고 second order일 때 backward를 사용한다.(넥스트폼이 수정)

Momentum은 first order upwind일 때 Gauss upwind를 사용하고, second order일 때는 Gauss linearUpwind와 <span style="color:blue">Venkatakrishnan’s limiter(넥스트폼이 개발)를 사용한다.</span>

Turbulence와 Energy는 first order upwind일 때 Gauss upwind를 사용하고, second order일 때는 Gauss linearUpwind와 <span style="color:blue">Barth-Jespersen’s limiter(넥스트폼이 개발)를 사용한다.</span>

## Under-Relaxation Factors

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/relaxation.png"><br> Under-Relaxation Factors 설정
</p>

정상상태에서는 default 값만, 비정상상태에서는 default 값과 final 값을 입력한다. fvSolution 파일의 relaxationFactors에 해당한다. 값이 클수록 수렴 속도가 빨라질 수 있으나 불안정해질 수 있다. SIMPLEC를 사용하는 경우 0.9 이상의 값을 추천한다.

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

## Advanced - Limits

Limits의 값은 계산의 안정성을 위해 온도의 최소, 최대값을 제한한다. fvOptions의 limitTemperature를 사용한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/limit.png"><br> Limits 설정
</p>

