---
layout: post
title: 03. BARAM의 동작원리
category: userguidelist
---

# 03. BARAM의 동작원리 

(주)넥스트폼이 개발한 OpenFOAM 패키지인 nextFoam, TSLAeroFoam을 기반으로 다음의 순서로 동작한다.<br>

1) 프로그램을 실행하고 격자를 읽으면 temp 폴더 안에 0, constant, system 폴더가 만들어진다.<br>

2) constant 폴더 아래에 polyMesh 폴더가 sysyem 폴더 아래에 controlDict가 생성된다.<br>

3) 물성치, 물리 모델, 경계조건, 수치조건 등을 성정한다.<br>

4) 초기화를 진행하면 각 폴더 별로 다음과 같이 파일들이 생성된다.<br>
&nbsp; 4-1) 0폴더 아래에 경계값, 초기값들이 저장된다.<br>
&nbsp; 4-2) constant 폴더 아래에 g, operatingConditions, 물성치들이 저장된다.<br>
&nbsp; 4-3) system 폴더 아래에 decomposeParDict, fvSchemes, fvSolution들이 저장된다.<br>

5) File-save를 누르면 최상위 temp폴더가 case로 폴더명이 변경된다.<br>

6) 계산을 시작하면 stdout에 계산 로그가 남게 되고, 에러나 문제가 발생할 경우 stdout, stderr, baram 파일에 로그가 남게 된다.<br>