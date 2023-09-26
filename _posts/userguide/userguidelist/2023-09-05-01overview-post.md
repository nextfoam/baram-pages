---
layout: post
title: 01. 개요
category: userguidelist
---

# 01. 개요 

[Features](/baram-pages/docs/feature_overview)를 참고해도 된다.

* BARAM v23은 비압축성, 압축성 유동과 열전달 해석을 위한 전산유체역학 (CFD) 프로그램으로 Open Source인 OpenFOAM v2212 기반으로 개발되었다. (2023년 9월 06일 기준)<br>

* 비압축성 유동과 열전달은 정확성, 안정성 향상을 위해 (주)넥스트폼이 개발한 솔버, 유틸리티, 라이브러리등을 사용한다.<br>

* 압축성 유동은 (주)넥스트폼이 개발한 밀도 기반 솔버인 (Density Based Solver) TSLAeroFoam을 사용한다.<br>

* 그리고 Kurganov-Tadmor 기법을 사용하여 아음속에서 초음속까지 영역을 계산할 수 있는 압력기발 솔버인 (Pressure Based Solver) PCNFoam을 사용한다.<br>

* BARAM의 그래픽 인터페이스는 다음 2개의 모듈로 구성되어 있다. <br>

 &ensp; - 해석 모듈 : BARAM<br>
 &ensp; - 격자 생성 모듈 : BARAM-snappy<br>

* 사용자 환경은 다음 프로그램을 이용하여 개발되었다 : Python, vtk<br>

* (주)넥스트폼이 개발하여 GNU GPL 라이센스로 공개한다.<br>

* BARAM v23의 기능은 다음과 같다. <br><br>
    &ensp; * Solver<br>
    &ensp; &ensp; - simpleNFoam : 정상상태 비압축성 유동 솔버 <br>
    &ensp; &ensp; - pimpleNFoam : 비정상상태 비압축성 유동 솔버 <br>
    &ensp; &ensp; - buoyantSimpleNFoam : 정상상태 비압축성 열전달 유동 솔버 <br>
    &ensp; &ensp; - buoyantPimpleNFoam : 비정상상태 비압축성 열전달 유동 솔버 <br>
    &ensp; &ensp; - interNFoam : 비정상상태 자유수면 해석 솔버 <br>
    &ensp; &ensp; - PCNFoam : 압력기반 비압축성/압축성 유동 솔버 <br>
    &ensp; &ensp; - TSLAeroFoam : 밀도기반 압축성 유동 솔버 <br><br>
    &ensp; * 난류 모델<br>
    &ensp; &ensp; - Inviscid <br>
    &ensp; &ensp; - Laminar <br>
    &ensp; &ensp; - Spalart-Allmaras (SA) <br>
    &ensp; &ensp; - k-ε <br>
    &ensp; &ensp; &ensp; - Standard <br>
    &ensp; &ensp; &ensp; - RNG <br>
    &ensp; &ensp; &ensp; - Realizable <br>
    &ensp; &ensp; - SST k-ω <br><br>
    &ensp; * 열전달<br>
    &ensp; &ensp; - Forced convection <br>
    &ensp; &ensp; - Natural convection <br>
    &ensp; &ensp; - Conjugate Heat Transfer (CHT) <br><br>
    &ensp; * Cell Zone 모델<br>
    &ensp; &ensp; - Multiple Refernce Frame (MRF) <br>
    &ensp; &ensp; - Sliding Mesh <br>
    &ensp; &ensp; - Actuator Disk <br>
    &ensp; &ensp; - Fixed Values <br>
    &ensp; &ensp; - Source Terms <br><br>
    &ensp; * 격자 생성 : snappyHexMesh<br><br>
    &ensp; * 격자 파일 변환 <br>
    &ensp; &ensp; - Fluent : .msh, .cas (ASCII 파일만 가능) <br>
    &ensp; &ensp; - Star-ccm+ :  <br>
    &ensp; &ensp; - gmsh (ASCII 파일만 가능) <br>
    &ensp; &ensp; - ideasUnv <br><br>
    &ensp; * 후처리 <br>
    &ensp; &ensp; - ParaView <br>