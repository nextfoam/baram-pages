---
layout: post
title: Reference Values
category: userguidelist
---

# Reference Values

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/reference.png"><br> Reference Values 설정
</p>

Area, Density, Length, Velocity 값은 force coefficient를 계산할 때 사용된다.

Pressure는 유동의 유출입이 없는 폐공간과 같이 압력이 어디에도 정의되지 않았을 때, 기준 압력이 된다. fvSolution의 SIMPLE 혹은 PIMPLE 딕셔너리의  pRefValue 값이다.
