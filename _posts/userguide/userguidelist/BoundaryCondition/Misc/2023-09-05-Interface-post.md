---
layout: post
title: 02. Interface
category: Misc
---

# 02. Interface

<p align='Center'>
    <img src="https:nextfoam.co.kr/baramManual/userguide/11.16.png"><br>
    그림 11.16
</p>

* Internal Interface, Rotational Periodic, Translational Periodic을 설정할 수 있다.<br>
&ensp; - Internal Interface : 두 면을 선택하면 모두 Internal Interface로 설정된다.<br>

&ensp; - Rotational Interface : 두 면을 선택하면 회전 주기 조건으로 변경된다.<br>
&ensp; - 회전축과 회전축의 원점도 같이 설정해야한다.<br>

&ensp; - Translational Interface : 두 면을 선택하면 병진 운동의 주기 조건으로 변경된다.<br>
&ensp; - 병진 방향도(Translation Vector) 설정해야한다.<br>

&ensp;&ensp; **※Cyclic 경계 조건은 회전 주기로 설정되는 두 경계면의 격자 topology가 일치해야한다.**<br>
&ensp;&ensp; **※반면, Rotational Interface로 설정되는 두 경계면의 격자 topology가 일치할 필요는 없다.**<br>