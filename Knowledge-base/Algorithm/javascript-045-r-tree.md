---
title: [JavaScript] 045: R-트리
description: 
published: true
date: 2023-02-10T23:32:34.256Z
tags: 
editor: markdown
dateCreated: 2023-02-10T23:32:27.556Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 045: R-Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-045-r-tree)
{.links-list}


# R-트리

R-Tree는 점, 사각형 및 다각형과 같은 공간 데이터를 저장하는 데 사용되는 데이터 구조입니다. 각 노드가 직사각형 영역을 나타내는 유형의 공간 분할 트리입니다. 트리는 주어진 노드의 모든 직사각형이 해당 노드의 직사각형 내에 포함되도록 설계되었습니다.

R-트리는 종종 지리 정보 시스템(GIS), 컴퓨터 지원 설계(CAD) 및 이미지 처리에 사용됩니다.

## 작동 방식

R-Tree의 기본 아이디어는 2차원 공간을 겹치지 않는 직사각형 집합으로 나누는 것입니다. 각 사각형은 점, 선 또는 다각형과 같은 개체와 연결됩니다. 그런 다음 사각형은 전체 2차원 공간을 나타내는 루트 노드와 함께 트리 구조로 구성됩니다. 루트 노드의 자식 노드는 공간 내의 더 작은 사각형을 나타냅니다.

![RTree](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree.png)

R-Tree를 사용하면 주어진 지점에 가까운 객체를 빠르게 찾을 수 있다는 장점이 있습니다. 예를 들어, 주어진 점의 주어진 반경 내에 있는 모든 점을 찾으려면 반지름과 교차하는 모든 직사각형에 대해 R-Tree를 쿼리하면 됩니다. 이것은 반지름 내에 있는 점에 대해 전체 공간을 검색하는 것보다 훨씬 빠릅니다.

## 삽입

R-Tree에 삽입하는 것은 2단계 프로세스입니다. 먼저 새 사각형을 삽입해야 하는 리프 노드를 찾습니다. 이렇게 하려면 루트 노드에서 시작하여 새 사각형을 루트 노드의 각 사각형과 비교합니다. 그런 다음 새 사각형과 가장 일치하는 사각형을 선택하고 해당 사각형과 연결된 자식 노드로 프로세스를 반복합니다. 리프 노드에 도달할 때까지 이 프로세스를 계속합니다.

새 사각형을 삽입해야 하는 리프 노드를 찾으면 해당 노드에 새 사각형을 추가하기만 하면 됩니다.

![RTreeInsert](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree-insert.png)

## 삭제

R-Tree에서 삭제는 2단계 프로세스입니다. 먼저 삭제할 사각형이 있는 리프 노드를 찾습니다. 이를 위해 루트 노드에서 시작하여 삭제할 사각형을 루트 노드의 각 사각형과 비교합니다. 그런 다음 삭제할 사각형과 가장 일치하는 사각형을 선택하고 해당 사각형과 연결된 자식 노드로 프로세스를 반복합니다. 리프 노드에 도달할 때까지 이 프로세스를 계속합니다.

사각형이 있는 리프 노드를 찾으면 해당 노드에서 사각형을 제거하기만 하면 됩니다.

![RTreeDelete](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree-delete.png)

## 쿼리

R-Tree 쿼리는 2단계 프로세스입니다. 먼저 쿼리 사각형과 교차하는 리프 노드를 찾습니다. 이렇게 하려면 루트 노드에서 시작하여 쿼리 사각형을 루트 노드의 각 사각형과 비교합니다. 그런 다음 쿼리 사각형과 교차하는 사각형을 선택하고 해당 사각형과 연결된 자식 노드로 프로세스를 반복합니다. 리프 노드에 도달할 때까지 이 프로세스를 계속합니다.

쿼리 사각형과 교차하는 리프 노드를 찾으면 해당 사각형과 관련된 개체를 반환하기만 하면 됩니다.

![RTreeQuery](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree-query.png)

## 구현

R-Tree를 구현하는 방법에는 여러 가지가 있습니다. 인기 있는 방법 중 하나는 각 노드에 최대 4개의 하위 노드가 있는 일종의 공간 분할 트리인 쿼드트리를 사용하는 것입니다.

또 다른 인기 있는 방법은 k-d 트리를 사용하는 것인데, 이는 각 노드가 최대 두 개의 하위 노드를 갖는 일종의 공간 분할 트리입니다.

## 결론

R-트리는 공간 데이터를 저장하고 쿼리하기 위한 강력한 데이터 구조입니다. 효율적이고 구현하기 쉽습니다.