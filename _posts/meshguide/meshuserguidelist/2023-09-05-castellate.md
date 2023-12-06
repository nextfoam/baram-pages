---
layout: post
title: 06. Castellation
category: meshuserguidelist
---

# Castellation

Castellation에서는 지정한 영역의 격자를 분할하여 조밀하게 만들어 주고 계산 영역 바깥의 격자를 삭제한다.

격자의 조밀도는 size level로 조절하는데 base grid 격자의 크기를 기준 0으로 사용하고, 1만큼 커질 때 마다 육면제를 4개로 분할한다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_castell.png"><br> Base Grid to Castellation
</p>


Configuration 설정괴 Advance 설정이 있다. 격자를 나눌 부분은 Surface/Feature 혹은 volume에 대해 설정할 수 있다.

## Configuration

+ __Number of Cells between Levels__ : 
셀 크기의 급격한 변화는 격자 시스템에 좋지 않기 때문에, 레벨 변경시 완충영역을 두는 것이다. snappyHexMeshDict의 castellatedMeshControls.nCellsBetweenLevels에 해당한다. 아래 그림에서 원의 격자 레벨이 1일 때 1,2,3일 때의 결과를 나타내었다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_nCellsBetweenLevels.png"><br> Number of Cells between Levels (좌) 1, (중) 2, (우) 3
</p>


+ __Feature Angle Threshold__ : 인접한 두 격자의 법선이 이루는 각이 이 값보다 클 때 주어진 size level 보다 1더 큰 값을 사용한다. snappyHexMeshDict의 castellatedMeshControls.resolveFeatureAngle에 해당한다. 아래 그림은 두 개의 육면체가 있고 내부의 육면체의 사이즈 레벨을 1로 주었을 때, 이 값에 따른 castellation 결과를 보여준다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_resolveFeature.png"><br> Feature Angle Threshold 영향 (좌) 형상, (중) 100, (우) 30
</p>

+ __Keep Non-Manifold Edges__ : surface의 feature를 extract할 때 사용하는 옵션으로 3개 이상의 연결된 면을 갖는 edge를 포함할 것인지에 대한 옵션이다.

+ __Keep Open Edges__ : surface의 feature를 extract할 때 사용하는 옵션으로 연결된 면이 1개 뿐인 edge를 포함할 것인지에 대한 옵션이다.


## Advanced

+ __Max. Global Cell Count__ : 전체 셀 개수의 제한으로 이 값에 도달하면 셀 분할이 중단된다. castellation 과정에서 계산영역이 아닌 부분의 격자를 제거하기 전의 격자수로 판단한다. snappyHexMeshDict의 castellatedMeshControls.maxGlobalCells에 해당한다.

+ __Max. Local Cell Count__ : 병렬 연산시 각 코어당 최대 셀 개수이다. 병렬 연산시 refinement-followed-by 방식의 밸런싱을 사용하는데, 이 값에 도달하면 weighted balancing 방법을 사용하게 된다. 이 경우 속도가 느려질 수 있다. snappyHexMeshDict의 castellatedMeshControls.maxLocalCells에 해당한다.

+ __Min. Refinement Cell count__ : 격자 세분화 과정이 소수의 셀 때문에 많은 시간이 소비되는 문제가 있을 수 있다. 남은 셀들이 여기서 지정한 값에 도달하면 격자 세분화 과정을 중단한다. snappyHexMeshDict의 castellatedMeshControls.minRefinementCells에 해당한다.

+ __Max. Load Unbalance__ : 병렬 연산에서 프로세스 당 셀 수의 상대적인 차이이다. 낮은 값은 더 자주 로드 밸런싱을 하게 되고 높은 값은 로드 밸런싱을 비활성화 할 수도 있다. snappyHexMeshDict의 castellatedMeshControls.maxLoadUnbalance에 해당한다.

+ __Allow Free Standing Zone Faces__ : faceZone이 baffle과 같이 독립적일 때 true로 설정해 주어야 한다. snappyHexMeshDict의 castellatedMeshControls.allowFreeStandingZoneFaces에 해당한다.

## Surface/Feature Refinement

오른쪽의 (+)를 클릭하면 생성된다.

Surface와 Feature 각각에 대한 레벨을 지정하고 적용할 surface를 선택한다. Surface는 geometry에서 만들어진 것들이 니타난다. Feature는 geometry를 만들 때 baramMesh에서 만들어 주기 때문에 따로 선택할 필요는 없다.

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_surfaceRefinement.png"><br> Surface Refinement 설정
</p>

## Volume Refinement

Volume의 레벨을 지정하고 적용할 volume을 선택한다. Volume은 geometry에서 만들어진 것들이 니타난다. 

<p style="text-align: center">
    <img src="https://github.com/nextfoam/baram-pages/raw/main/screenshots/pic/mesh_volumeRefinement.png"><br> Volume Refinement 설정
</p>






