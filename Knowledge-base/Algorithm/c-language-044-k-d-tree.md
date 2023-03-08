---
title: [C언어] 044: K-D 트리
description: 
published: true
date: 2023-02-13T22:32:20.066Z
tags: 
editor: markdown
dateCreated: 2023-02-13T22:32:18.230Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 044: K-D Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-044-k-d-tree)
{.links-list}


# 044: K-D 트리

k-d 트리(k-차원 트리의 약자)는 k-차원 공간에서 점을 구성하기 위한 공간 분할 데이터 구조입니다. k-d 트리는 다차원 검색 키를 포함하는 검색(예: 범위 검색 및 최근접 이웃 검색)과 같은 여러 응용 프로그램에 유용한 데이터 구조입니다.

k-d 트리는 모든 노드가 k 차원 지점인 이진 트리입니다. 트리는 분산이 가장 큰 점을 통과하는 초평면을 따라 점을 두 세트로 분할하여 하향식 방식으로 재귀적으로 구성됩니다. 이 프로세스는 원하는 세분성 수준에 도달할 때까지 각 세트에서 재귀적으로 반복됩니다.

## 개념

k-d 트리는 이진 검색 트리 데이터 구조의 일반화입니다. 이진 검색 트리에서 포인트는 단일 차원(예: x축)을 따라 분할되어 2차원 공간이 됩니다. k-d 트리에서 점은 여러 차원에 따라 분할되어 k차원 공간이 됩니다.

k-d 트리의 포인트 분할은 하향식 방식으로 재귀적으로 수행됩니다. 트리는 모든 포인트를 포함하는 루트 노드로 시작하여 구성됩니다. 그런 다음 루트 노드는 분산이 가장 큰 차원을 따라 분할되고 포인트는 피벗 포인트보다 작은 모든 포인트를 포함하는 한 세트와 더 큰 모든 포인트를 포함하는 다른 세트의 두 세트로 분할됩니다. 피벗 포인트보다 크거나 같습니다.

그런 다음 이 프로세스는 원하는 세분성 수준에 도달할 때까지 두 세트 각각에서 재귀적으로 반복됩니다.

## 코드 예

의사 코드에서 k-d 트리를 구성하는 방법에 대한 간단한 예는 다음과 같습니다.

```
function kdtree(points, depth)
   if points is empty
      return

   select a pivot point, p, using some heuristic (e.g. median of points)
   partition points into two sets, S1 and S2, using p as the pivot
   create a new node, n, with p as the key
   n.left = kdtree(S1, depth + 1)
   n.right = kdtree(S2, depth + 1)
   return n
```

## 관련 연습

- [ ] 좋아하는 프로그래밍 언어로 k-d 트리를 구현합니다.
- [ ] 점 집합이 주어지면 k-d 트리를 구성하고 주어진 점의 가장 가까운 이웃을 쿼리합니다.
- [ ] 포인트 집합이 주어지면 k-d 트리를 구성하고 주어진 범위 내의 모든 포인트에 대해 쿼리합니다.