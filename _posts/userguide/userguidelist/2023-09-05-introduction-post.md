---
layout: post
title: 01. Introduction
category: userguidelist
---

# BARAM 이란

BARAM-v24는 압축성 유동, 비압축성 유동, 다상유동, 열전달 해석, 화학종 혼합 계산을 위한 전산유체역학 프로그램 패키지이며, 공개 소스 CFD 도구 상자인 OpenFOAM 기반으로 개발되었다.

BARAM-v24에서 사용하는 OpenFOAM은 NextFOAM-v24이다. NextFOAM-v24는 ESI의 v2406 기반으로 (주)넥스트폼에서 개발한 포크로, 안정성, 수렴성, 정확성 향상과 새로운 기능을 위한 다양한 라이브러리, 유틸리티, 솔버를 포함한다. BARAM-v24를 설치하면 NextFOAM-v24의 바이너리가 설치된다. 소스코드는 github에서 다운 받을 수 있다.[https://github.com/nextfoam/baram](https://github.com/nextfoam/nextfoam-cfd) 

BARAM은 격자 생성 모듈인 baramMesh와 해석 모듈인 baramFlow로 구성된다.

격자 생성 모듈 BaramMesh는 OpenFOAM의 유틸리티인 blockMesh와 snappyHexMesh를 사용하여 격자를 생성하는 모듈이다. 형상은 STL 파일을 가져올 수 있고 육면체, 구, 실린더 형상을 생성할 수 있다. 경계층 격자를 포함한 octree 방식의 3차원 격자를 생성할 수 있으며 region, cell zone, interface를 만들 수 있다.

해석 모듈 BaramFlow는 전산유체역학 해석을 위한 모듈로 비압축성유동, 열전달, 압축성유동, 다상유동, 화학종 혼합을 해석할 수 있다.

BARAM은 다양한 프로그램을 사용하여 개발되었으며 모두 공개소스 프로그램만 사용되었다. 그래픽 사용자 환경은 python, Qt, vtk를 이용하여 개발 되었으며, 공개소스 프로그램인 paraview를 이용하여 후처리 작업을 할 수 있다.

(주)넥스트폼이 개발하여 GNU GPL 라이선스로 공개하였다.

BARAM-v24에서 사용하는 솔버는 다음과 같다. 

* buoyantSimpleNFoam : 정상상태 아음속, 열전달, 화학종 혼합 해석(넥스트폼 개발)
* buoyantPimpleNFoam : 비정상상태 아음속, 열전달, 화학종 혼합 해석(넥스트폼 개발)
* chtMultiRegionSimpleNFoam : 정상상태 multi-region 해석(넥스트폼 개발)
* chtMultiRegionPimpleNFoam : 비정상상태 multi-region 해석(넥스트폼 개발)
* interFoam : 2상 유동의 자유수면 해석
* interPhaseChangeFoam : 캐비테이션 해석
* multiphaseInterFoam : 3종 이상의 물질에 대한 VOF 다상유동 해석
* TSLAeroFoam : 밀도기반 정상상태 압축성 유동 해석(넥스트폼 개발)
* <span style="color:gray">압력기반 비압축성/압축성 전체 속도 영역 솔버(곧 지원 예정)</span>
  
# 주요 기능

* 난류
  + Euler  
  + Laminar  
  + Standard $k-\epsilon$, RNG $k-\epsilon$, Realizable $k-\epsilon$ with standard & two-layer wall function  
  + SST $k-\omega$  
  + Spalart-Allmara  
  + LES/DES
  
* 열전달
  + Forced convection  
  + Natural convection  
  + conjugate heat transfer  
  + <span style="color:gray">Radiation : P1, fvDOM(곧 지원 예정)</span>
  
* Cell zone 모델
  + MRF  
  + Sliding mesh  
  + Porous media : Darcy-Forchheimer / power law  
  + Fixed velocity  
  + Scalar source  
  + Scalar fixed value

* Paremeter를 이용한 일괄 계산(batch run)
  
* Passive scalar 계산
 
* 격자 생성
  + snappyHexMesh  
  + <span style="color:gray">cfMesh(곧 지원 예정)</span>
  
* 격자 파일 변환 
  + Fluent msh/cas : 넥스트폼이 수정한 fluentToFoam 유틸리티 사용  
  + Star-CCM+ ccm : ccmToFoam 유틸리티 사용  
  + ideasUnv : ideasUnvToFoam 유틸리티 사용  
  + gmsh : gmshToFoam 유틸리티 사용  
  + <span style="color:gray">plot3D : plot3dToFoam(곧 지원 예정)</span>
  
* STL 파일 처리 : 특성 각도에 따른 표면 분할(surfaceAutoPatch)

* 격자 처리  
  + Mesh information : cell 정보, 도메인의 범위 표시  
  + Mesh transform : scale, translate, rotate
  + convert to axi-symmetric mesh  
  + converr to 2d mesh  
  + <span style="color:gray">Refine wall layer(곧 지원 예정)</span>  
  + <span style="color:gray">Create baffle / interior : from faceSet, faceZone(곧 지원 예정)</span>
  
* 후처리
  + monitoring - point value, surface value, volume value, force
  + data extraction : point value, surface value, volume value, force
  + ParaView
  + <span style="color:gray">경계면에서 스칼라 분포 및 벡터(곧 지원 예정)</span>  
  + <span style="color:gray">축단면에서 스칼라 분포 및 벡터(곧 지원 예정)</span>  
  + <span style="color:gray">iso-surface(곧 지원 예정)</span>  
  + <span style="color:gray">clip data(곧 지원 예정)</span>  
  + <span style="color:gray">streamline(곧 지원 예정)</span> 

# 폴더 구조

BARAM은 작업 프로젝트를 폴더 단위로 관리한다. 

프로젝트 폴더에는 case라는 폴더와 baram.cfg, baram.log, configuration, configuration.h5 등의 파일이 있다. 

case 폴더는 openfoam 계산 폴더이다. openfoam에서 사용하는 0, constant, system, postProcessing, [time] 등의 폴더가 있으며 baram.foam, stderr.log, stdout.log 파일이 있다. baram.foam은 후처리를 위한 paraview 실행을 위한 파일이며 stdout.log는 솔버를 포함한 각종 실행파일 실행시 생성되는 로그 파일이며, stderr.log는 실행시 나타난 에러 메세지이다.

그래픽 인터페이스의 각종 설정은 HDF5 파일 형식으로 configuration.h5에 있다. HDF5는 Hierarchical Data Format version 5의 약어로, 계층적 데이터 형식으로 대량의 데이터를 저장하고 관리하기 위한 파일 형식 및 라이브러리이다.(https://www.hdfgroup.org/solutions/hdf5/)
 


 
  


