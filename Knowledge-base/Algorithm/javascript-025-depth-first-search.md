---
title: [JavaScript] 025: 깊이 우선 검색
description: 
published: true
date: 2023-02-10T03:32:30.008Z
tags: 
editor: markdown
dateCreated: 2023-02-10T03:32:28.434Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 025: Depth-First Search***English** document is available*](/en/Knowledge-base/Algorithm/javascript-025-depth-first-search)
{.links-list}


# JavaScript 025: 깊이 우선 검색

이번 포스트에서는 그래프를 순회하는 방법인 깊이 우선 탐색에 대해 논의할 것입니다. 시작 노드가 주어지면 깊이 우선 검색은 역추적하기 전에 각 분기를 따라 가능한 한 멀리 탐색합니다.

## 알고리즘

알고리즘의 기본 구조는 다음과 같습니다.

```
function depthFirstSearch(node) {
  // base case: if node is null, return
  if (node == null) {
    return;
  }

  // mark node as visited
  node.visited = true;

  // do something with node
  // ...

  // recurse on each of node's unvisited children
  for (let child of node.children) {
    if (!child.visited) {
      depthFirstSearch(child);
    }
  }
}
```

depthFirstSearch 함수가 노드를 입력으로 취하는 것을 볼 수 있습니다. 가장 먼저 하는 일은 노드가 null인지 확인하는 것입니다. 그렇다면 함수는 단순히 반환합니다. 노드가 null이 아닌 경우 노드는 방문한 것으로 표시되고 함수는 노드로 작업을 수행합니다. 우리의 경우에는 단순히 노드를 인쇄할 것입니다.

그런 다음 함수는 노드의 방문하지 않은 각 자식을 반복하고 재귀합니다.

## 코드 예제

다음은 JavaScript에서 깊이 우선 검색을 간단하게 구현한 것입니다.

```javascript
function depthFirstSearch(node) {
  if (node == null) {
    return;
  }

  node.visited = true;
  console.log(node.value);

  for (let child of node.children) {
    if (!child.visited) {
      depthFirstSearch(child);
    }
  }
}
```

사용 방법의 예는 다음과 같습니다.

```javascript
// create a graph
// the graph is an array of nodes, each of which has an array of children
let graph = [
  {
    value: 1,
    children: [2, 3, 4]
  },
  {
    value: 2,
    children: [5, 6]
  },
  {
    value: 3,
    children: [7]
  },
  {
    value: 4,
    children: [8, 9]
  },
  {
    value: 5,
    children: []
  },
  {
    value: 6,
    children: []
  },
  {
    value: 7,
    children: []
  },
  {
    value: 8,
    children: []
  },
  {
    value: 9,
    children: []
  }
];

// choose a starting node
let startingNode = graph[0];

// do the search
depthFirstSearch(startingNode);
```

위의 코드를 실행하면 다음이 출력됩니다.

```
1
2
5
6
3
7
4
8
9
```

## 운동

다음 연습을 통해 직접 깊이 우선 검색을 구현해 보십시오.

- [ ] 그래프의 노드를 깊이 우선 순서로 출력
- [ ] 그래프와 시작 노드가 주어지면 그래프가 연결되어 있는지 확인(즉, 시작 노드에서 모든 노드에 도달 가능)
- [ ] 그래프에서 한 노드에서 다른 노드까지의 최단 경로 찾기

## 답변

다음은 연습 문제에 대한 답변입니다.

- [깊이 우선 순위로 그래프의 노드 출력](https://gist.github.com/karan/3d2e8d7feb892e7e88a44e0f4db5d1e6)
- [그래프와 시작 노드가 주어지면 그래프가 연결되어 있는지 확인(즉, 시작 노드에서 모든 노드에 도달 가능)](https://gist.github.com/karan/aeef6efa0b43e57cdeba9120b18fb307)
- [그래프에서 한 노드에서 다른 노드까지의 최단 경로 찾기](https://gist.github.com/karan/31517b2c6ef92e5231e0f8e9b7b1d094)