---
layout: post
title: 01. Velocity Condition
category: WallBoundaryCondition
---

# 01. Velocity Condition

* No-Slip : 점착조건을 가지는 벽을 의미한다. 벽면에서 유체의 속도는 0이다.<br>

* Slip : 점착조건을 가지지 않고 미끄러지는 벽을 의미한다. 벽면에서 유체의 속도는 0이다.<br>

* 각 필드는 다음의 경계조건을 사용한다.<br>
&ensp; - 압력 : fixedFluxPressure<br>
&ensp; - 온도 : zeroGradient<br>
&ensp; - k : kqRWallFunction<br>
&ensp; - ε, ω : NEXT::epsilonWallFunction, NEXT::omegaBlendedWallFunction<br>
&ensp; - 𝜈<sub>𝜏</sub> : k-ε 계열은 NEXT::nutkWallFunction, SST k-ω는 NEXT::nutSpaldingWallFunction<br>
&ensp; - α<sub>t</sub> : compressible::alphatWallFunction<br>

* Moving Wall : Sliding 경계 조건을 사용할 때, 움직이는 경계면에 적용된다.<br>

* Translational Moving Wall : 벽이 Translation 움직임을 가질 경우 적용한다.<br>
&ensp; - X, Y, Z-Velocity : 벽의 X, Y, Z 축 속도를 입력할 수 있다.<br>

* Rotating Moving Wall : 벽이 Rotating 움직임을 가질 경우 적용한다.<br>
&ensp; - Speed : 벽의 회전 속도를 의미한다.<br>
&ensp; - Rotation-Axis Origin : 벽의 회전 원점을 의미한다.<br>
&ensp; - Rotation-Axis Direction : 벽의 회전 축을 의미한다.<br>

* 각 필드는 다음의 경계조건을 사용한다.<br>
&ensp; - 압력, 온도 : zeroGradient<br>
&ensp; - k : kqRWallFunction<br>
&ensp; - ε, ω : NEXT::epsilonWallFunction, NEXT::omegaBlendedWallFunction<br>
&ensp; - 𝜈<sub>𝜏</sub> : k-ε 계열은 NEXT::nutkWallFunction, SST k-ω는 NEXT::nutSpaldingWallFunction<br>
&ensp; - α<sub>t</sub> : compressible::alphatWallFunction<br>