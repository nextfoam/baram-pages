---
layout: post
title: 2. Under-Relaxation Factors & Improve Stability
category: NumericalCondition
---

# 2. Under-Relaxation Factors & Improve Stability

* Under-Relxation Factors, Improve Stability와 Max Iterations pre Time Step에 대한 설명은 다음과 같다. <br>

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/13.2.png"><br>
    그림 13.2
</p>

&ensp; - Under-Relaxation Factors : Relaxation Factor에 해당하는 값을 입력한다.<br>

&ensp; - Imporve Stability : High Order Term Relaxation이다.<br>

&ensp; - Max Iterations per Time Step : Transient 계산에서 활성화되고, 1 time step안에 최대 Iteration을 설정할 수 있다.<br>

&ensp; - Number of Correctors : Transient 계산에서 활성화되고, Pressure Equation을 몇 번 계산할 것인지 정한다. 즉, Solution의 수정 횟수를 결정한다.<br>