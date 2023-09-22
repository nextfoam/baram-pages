---
layout: post
title: 3. Multiphase & Convergence Criteria
category: NumericalCondition
---

# 3. Multiphase & Convergence Criteria

* Multiphase의 수치 정보와 Convergence Criteria에 대한 정보는 다음과 같다. <br>

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/13.3.png"><br>
    그림 13.3
</p>

&ensp; - Max Iterations per Time Step : Transient 계산에서 활성화되고, 1 time step안에 최대 Iteration을 설정할 수 있다.<br>

&ensp; - Number of Correctors : Transient 계산에서 활성화되고, Pressure Equation을 몇 번 계산할 것인지 정한다. 즉, Solution을 수정 횟수를 결정한다.<br>

&ensp; - MULES Variant : Multiphase 경계면의 변형 포착 방식을 결정한다.<br>

&ensp; - Phase Interface Compression Factor : 인터페이스의 압축을 제어하는 요소이다. 0은 압축이 없음을 1은 보존적 압축에 해당된다.<br>
&ensp; 일반적으로 1.0값을 사용하는 것이 좋다.<br>

&ensp; 아래 링크는 Phase Interface Compression Factor에 따른 결과를 잘 보여주는 영상이다.<br>
https://www.youtube.com/watch?v=-fU7kTIoIb4<br>

&ensp; - Number of MULES iterations over the limiter : limiter에 대한 MULES 반복 횟수<br>

&ensp; - Convergence Criteria : 각 필드의 수렴 조건을 나타낸다.<br>

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/13.4.png"><br>
    그림 13.4
</p>

&ensp; - Limits : 최소, 최대 온도 범위를 결정한다.<br>