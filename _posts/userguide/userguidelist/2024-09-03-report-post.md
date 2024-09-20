---
layout: post
title: 14. Report
category: userguidelist
---

# Reports

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/report.png"><br> Report
</p>

계산 종료 후 결과 값을 추출하는 곳이다. Force, Point, Surface, Volume 등 4 가지에 대해 값을 추출할 수 있다.

## Force

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/forceReport.png"><br> 
</p>

Flow Direction은 'Direct'와 'Angle of Attack, Sideslip'을 선택할 수 있다. 'Direct'는 Drag와 Lift의 방향을 벡터로 입력하는 방식이다. 'Angle of Attack, Sideslip'은 받음각(AOS)과 옆미끄럼각(AOS)가 0일 때의 Drag, Lift 방향을 기준으로 각도를 입력한다. Pitch axis는 drag, lift 방향과 수직하게 결정된다.

'Center of Rotation'과 경계면을 선택하고 'Compute' 버튼을 누르면 결과를 확인할 수 있다. Drag/Lift/Moment coefficient와 함께 Force와 Moment를 압력항과 점성항으로 나누어 방향별 값을 확인할 수 있다. 

<span style="color:blue">C<sub>d</sub>, C<sub>l</sub>, C<sub>m</sub>을 계산할 때 필요한 reference 값은 [Setup-Reference Values]의 값을 사용한다</span>.

Monitoring에서와 달리 Report에서는 저장된 데이터를 이용해서 계산하기 때문에 데이터의 write precision에 따라 monitoring의 값과 미소한 차이가 있을 수 있다.

## Point

모니터링할 필드(Field)와 좌표(Coordinate)를 입력한다. 경계면에서의 값을 모니터링하고 싶다면 Snap onto Boundary에서 해당 경계면을 선택한다. 이 경우 좌표가 정확히 경계면상에 있지 않아도 좌표와 가장 인접한 지점의 값을 보여준다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/pointReport.png"><br>
</p>


## Surface

모니터링 할 경계면(Surface), 필드(Field Variable), Report Type을 설정한다. 

Report Type은 area-weighted average, mass-weighted average, integral, mass flowrate, volume flowrate, average, minimum, maximum, Coefficient of variation(CoV)을 선택할 수 있다. mass flowrate와 volume flowrate일 때는 경계면만 선택하면 되고, 다른 것들은 경계면과 필드를 선택한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/surfaceReport.png"><br> 
</p>


## Volume

모니터링 할 영역(Volumes), 필드(Field Variable), Report Type을 입력한다.

Report Type은 volume average, volume integral, minimum, maximum, Coefficient of variation(CoV)을 선택할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/volumeReport.png"><br> 
</p>

