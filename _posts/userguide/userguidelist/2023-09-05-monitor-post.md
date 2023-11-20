---
layout: post
title: Monitor
category: userguidelist
---

# Monitors

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/monitor.png"><br> Monitors 설정
</p>

계산 중 결과의 모니터링을 위한 설정을 하는 곳이다. Force, Point, Surface, Volume 등 4 가지를 설정할 수 있다. Add 버튼을 눌러 해당 항목을 추가할 수 있다. 계산이 시작되면 추가된 항목은 Monitor 창에 그래프가 그려진다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/monitor1.png"><br> 모니터링 그래프 예
</p>

## Force

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/force.png"><br> Force 설정
</p>

설정 항목은 Write Interval, Lift Direction, Drag Direction, Center of Rotation, Boundaries이다. Write Interval은 몇 번 iteration 마다 데이터를 저장할 것인가이다. Pitch axis는 drag, lift 방향과 수직하게 결정된다. Force와 force coefficient 데이터가 저장되며 그래프는 C<sub>d</sub>, C<sub>l</sub>, C<sub>m</sub>이 그려진다. <span style="color:blue">C<sub>d</sub>, C<sub>l</sub>, C<sub>m</sub>을 계산할 때 필요한 reference 값은 [Setup-Reference Values]의 값을 사용한다</span>.

## Point

Point에 대한 설정창은 아래 그림과 같다. 모니터링할 필드(Field)와 좌표(Coordinate)와 모니터링 간격(Write Interval)을 입력한다. 경계면에서의 값을 모니터링하고 싶다면 Snap onto Boundary에서 해당 경계면을 선택한다. 이 경우 좌표가 정확히 경계면상에 있지 않아도 좌표와 가장 인접한 지점의 값을 모니터링한다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/point.png"><br> Point 설정
</p>


## Surface

Surface에 대한 설정창은 아래 그림과 같다. 모니터링 할 경계면(Surface), 필드(Field Variable), Report Type, Write Interval을 입력한다. 

Report Type은 area-weighted average, mass-weighted average, integral, mass flowrate, volume flowrate, average, minimum, maximum, Coefficient of variation(CoV)을 선택할 수 있다. mass flowrate와 volume flowrate일 때는 경계면만 선택하면 되고, 다른 것들은 경계면과 필드를 선택한다. 

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/surface.png"><br> surface 설정
</p>


## Volume

Volume에 대한 설정창은 아래 그림과 같다. 모니터링 할 영역(Volumes), 필드(Field Variable), Report Type, Write Interval을 입력한다.

Report Type은 volume average, volume integral, minimum, maximum, Coefficient of variation(CoV)을 선택할 수 있다.

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/volume.png"><br> volume 설정
</p>

