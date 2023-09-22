---
layout: post
title: 02. Thermo-Coupled Wall
category: Wall
---

# 02. Thermo-Coupled Wall

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/11.15.png"><br>
    그림 11.15
</p>

* Thermo-Coulped Wall은 계산 영역 내부에 있는 두께가 없는 벽면에 대한 조건이다.<br>

* 일반적으로 이름에 master와 slaver가 있는 경계면을 Thermo-Coupled Wall로 설정한다.<br>

* Coupled Boundary로 두 개의 경계면을 연결하면 된다.<br>

* 각 필드는 다음의 경계조건을 사용한다.<br>
&ensp; - 압력 : fixedFluxPressure<br>
&ensp; - 온도 : zeroGradient<br>
&ensp; - k : kqRWallFunction<br>
&ensp; - ε, ω : NEXT::epsilonWallFunction, NEXT::omegaBlendedWallFunction<br>
&ensp; - 𝜈<sub>𝜏</sub> : k-ε 계열은 NEXT::nutkWallFunction, SST k-ω는 NEXT::nutSpaldingWallFunction<br>
&ensp; - α<sub>t</sub> : compressible::alphatWallFunction<br>