---
layout: post
title: 02. 설치 및 실행방법
category: userguidelist
---

# 02. 설치 및 실행방법 

* 설치는 [Installation](/baram-pages/docs/installation) 페이지를 참고하면 된다.<br>

* 설치 시, require software 목록을 참고하여 Python, MS-MPI, OpenMPI 등을 먼저 설치 후 BARAM 설치를 추천한다.<br>

* BARAM v23이 설치되면 OpenFOAM v2212이 설치된다.<br>

* 설치가 완료되면 바탕화면에 BARAM 아이콘이 생성된다. 실행 시, 아이콘을 더블 클릭하면 BARAM이 실행된다.<br>

* Github에서 Source Code를 받아 실행할 경우, 프롬포트에 <br>
```commandline
    python main.py
```
위 명령어를 입력하여 실행하면 된다. <br>

* 터미널에서 실행 시, 명령어는 다음과 같다. <br>
    &ensp; - baram : 해석 모듈<br>
    &ensp; - baram-snappy : 격자 생성 모듈<br>