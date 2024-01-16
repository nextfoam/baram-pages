---
layout: post
title: 07. General
category: userguidelist
---

# General

Time, Gravity, Operating Conditions를 설정한다.

* Time : steady / transient 선택

* Gravity : 중력의 방향과 크기 설정. 온도를 계산하지 않거나 압축성 유동일 때는 사용되지 않음

* Operating Conditions
  + Operating Pressure : 기준 압력 설정. 프로그램에서 입력하는 압력은 이 값을 기준으로하는 상대압력을 사용한다. 이 값으로 0을 사용하면 모든 압력은 절대압력이 된다.

  ~~+ Reference Pressure Location : 유동의 유출입이 없는 폐공간과 같이 압력이 어디에도 정의되지 않았을 때, 기준 압력이 정의될 위치가 된다.~~(v24에서 없어짐. cell number 0을 기준 위치로 사용)

<p align='center'>
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/general.png"><br> General 설정
</p>


