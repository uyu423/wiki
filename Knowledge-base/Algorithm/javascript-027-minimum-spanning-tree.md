---
title: [JavaScript] 027: 최소 스패닝 트리
description: 
published: true
date: 2023-02-10T05:33:08.401Z
tags: 
editor: markdown
dateCreated: 2023-02-10T05:33:06.758Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 027: Minimum Spanning Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-027-minimum-spanning-tree)
{.links-list}


# 최소 스패닝 트리

컴퓨터 과학에서 최소 스패닝 트리(MST) 또는 최소 가중치 스패닝 트리는 모든 꼭지점을 함께 연결하는 방향이 지정되지 않은 가중 그래프의 에지의 하위 집합으로, 사이클 없이 가능한 최소 총 에지 가중치를 사용합니다.

최소 스패닝 트리에 대한 많은 응용 프로그램이 있습니다. 예를 들어, 도로나 통신 회선의 네트워크에서 최소 스패닝 트리를 사용하여 모든 노드를 함께 연결하는 가장 저렴한 방법을 찾을 수 있습니다. 또 다른 예는 군집 분석에서 최소 스패닝 트리를 사용하여 유사한 개체 그룹을 찾을 수 있습니다.

## 크루스칼 알고리즘

Kruskal의 알고리즘은 연결된 가중 그래프에 대한 최소 스패닝 트리를 찾는 그리디 알고리즘입니다. 가중치가 가장 작은 에지부터 시작하여 트리에 도달할 때까지 에지를 추가합니다.

알고리즘은 다음과 같이 작동합니다.

1. 가장 작은 것부터 가장 큰 것까지 가중치를 기준으로 가장자리를 정렬합니다.

2. 무게가 가장 작은 가장자리부터 시작합니다. 에지가 순환을 생성하지 않으면 트리에 추가하십시오.

3. 더 이상 추가할 모서리가 없을 때까지 2단계를 반복합니다.

Kruskal 알고리즘의 시간 복잡도는 O(E log V)이며, 여기서 E는 모서리의 수이고 V는 정점의 수입니다.

## 프림의 알고리즘

Prim의 알고리즘은 연결된 가중 그래프에 대한 최소 스패닝 트리를 찾는 그리디 알고리즘입니다. 꼭짓점에서 시작하여 트리에 도달할 때까지 가장 저렴한 가장자리를 추가합니다.

알고리즘은 다음과 같이 작동합니다.

1. 정점으로 시작합니다.

2. 꼭짓점에서 다른 꼭짓점까지 가장 저렴한 가장자리를 찾습니다.

3. 트리에 가장자리를 추가합니다.

4. 더 이상 추가할 모서리가 없을 때까지 2단계를 반복합니다.

Prim 알고리즘의 시간 복잡도는 O(E log V)이며, 여기서 E는 모서리의 수이고 V는 정점의 수입니다.

## 코드 예시

다음은 Kruskal 알고리즘의 JavaScript 구현입니다.

```javascript
function kruskals(edges) {
  // sort edges by weight
  edges.sort((a, b) => a.weight - b.weight);

  // make a set for each vertex
  const sets = [];
  for (let i = 0; i < edges.length; i++) {
    sets.push(new Set([i]));
  }

  // list of edges in the MST
  const mst = [];

  // for each edge, check if it creates a cycle
  for (const edge of edges) {
    const [u, v] = edge.vertices;

    // if the edge doesn't create a cycle, add it to the MST
    if (!sets[u].has(v)) {
      mst.push(edge);

      // union the two sets
      const setU = sets[u];
      const setV = sets[v];
      for (const vertex of setV) {
        setU.add(vertex);
        sets[vertex] = setU;
      }
    }
  }

  return mst;
}
```

## 운동

1. Kruskal 알고리즘을 사용하여 다음 그래프에 대한 최소 스패닝 트리를 찾습니다.

    ![](https://i.imgur.com/lVqnqj7.png)

2. Prim의 알고리즘을 사용하여 다음 그래프에 대한 최소 스패닝 트리를 찾습니다.

    ![](https://i.imgur.com/kzFcNcu.png)

## 답변

1. 그래프의 최소 스패닝 트리는 아래와 같습니다. 나무의 총 무게는 9입니다.

    ![](https://i.imgur.com/zM0FtqD.png)

2. 그래프의 최소 스패닝 트리는 다음과 같습니다. 나무의 총 무게는 10입니다.

    ![](https://i.imgur.com/kzFcNcu.png)