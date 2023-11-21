---
layout: post
title: 03. Folder Structure
category: userguidelist
---

# Baram의 폴더 구조

## 해석 모듈(BaramFlow)

폴더에 case라는 폴더와 baram.cfg, baram.log, configuration, configuration.h5 파일이 있다. 

case 폴더는 openfoam 계산 폴더이다. openfoam에서 사용하는 0, constant, system, postProcessing, _time__등의 폴더가 있으며 baram.foam, stderr.log, stdout.log 파일이 있다. baram.foam은 후처리를 위한 paraview 실행을 위한 파일이며 stdout.log는 솔버를 포함한 각종 실행파일 실행시 생성되는 로그 파일이며, stderr.log는 실행파일 실행시 나타난 에러 메세지이다.

그래픽 인터페이스의 각종 설정은 HDF5 파일 형식으로 configuration.h5에 있다. HDF5는 Hierarchical Data Format version 5의 약어로, 계층적 데이터 형식으로 대량의 데이터를 저장하고 관리하기 위한 파일 형식 및 라이브러리이다.(https://www.hdfgroup.org/solutions/hdf5/)
 

## 격자 생성 모듈(BaramMesh)

폴더에 case라는 폴더와 baram.cfg, case.lock, configuration.h5 파일이 있다. 

case 폴더는 snappyHexMesh 실행 폴더이다. 0, constant, system, [time] 등의 폴더가 있으며 baram.foam 파일이 있다. baram.foam은 후처리를 위한 paraview 실행을 위한 파일이다.

그래픽 인터페이스의 각종 설정은 HDF5 파일 형식으로 configuration.h5에 있다.


