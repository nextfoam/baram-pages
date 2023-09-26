---
layout: post
title: 16. Run Conditions
category: userguidelist
---

# 16. Run Conditions

<p align='Center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/userguide/16.1.png"><br>
    그림 16.1
</p>

* 계산의 Iterations, Save Interval등을 설정한다.<br>

## Steady 계산
* Number of Iterations : Iteration 수를 설정한다. 단, Convergence Criteria를 충족하면 해당 Iterations만큼 계산이 진행되지 않는다.<br>

* Save Interval : 매 N번 계산마다 데이터를 저장한다.<br>

* Retain Only the Most Recent Files : 가장 최근의 케이스 파일만 저장한다. 이전의 데이터 파일은 삭제한다.<br>

* Data Write Format : 저장되는 data의 형식을 설정한다. Binary는 용량은 작지만 User가 해당 데이터를 확인하지 못한다.<br>

* Data Write Precision : 저장되는 data의 유효숫자를 설정한다.<br>

* Time Precision : Time의 유효숫자를 의미한다.<br>