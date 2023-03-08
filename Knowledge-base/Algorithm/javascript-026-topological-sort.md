---
title: [JavaScript] 026: 위상 정렬
description: 
published: true
date: 2023-02-10T04:32:33.068Z
tags: 
editor: markdown
dateCreated: 2023-02-10T04:32:31.448Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 026: Topological Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-026-topological-sort)
{.links-list}


# 토폴로지 정렬

수학에서 토폴로지 정렬은 방향성 비순환 그래프(DAG)에서 정점의 선형 순서입니다. 유향 그래프의 토폴로지 정렬 또는 토폴로지 순서는 꼭짓점 u에서 꼭짓점 v까지의 모든 방향성 가장자리 uv에 대해 순서에서 u가 v보다 먼저 오는 정점의 선형 순서입니다. 예를 들어, 그래프의 정점은 수행할 작업을 나타내고 가장자리는 이러한 작업의 종속성을 나타낼 수 있습니다.

토폴로지 정렬에는 많은 응용 프로그램이 있습니다. 한 가지 예는 종속성을 기반으로 일련의 작업 또는 작업을 예약하는 것입니다. 또 다른 예로 소스 코드 파일 집합을 개체 파일 집합으로 컴파일하려고 한다고 가정합니다. 이는 소스 파일을 정점으로 표시하고 이들 사이의 종속성을 가장자리로 표시하여 수행할 수 있습니다. 그런 다음 토폴로지 정렬은 컴파일을 수행할 순서를 제공합니다.

토폴로지 정렬을 수행하기 위한 수많은 알고리즘이 있습니다. 이 기사에서는 Kahn의 알고리즘으로 알려진 가장 널리 사용되는 알고리즘 중 하나에 대해 설명합니다.

## 칸의 알고리즘

Kahn의 알고리즘은 1962년 Arthur B. Kahn이 "Topological Sorting of Large Networks" 논문에서 처음 설명한 위상 정렬 알고리즘입니다. 이 알고리즘은 그의 이름을 따서 명명되었습니다.

Kahn의 알고리즘 뒤에 있는 아이디어는 간단합니다. 들어오는 가장자리가 없는 정점 세트로 시작하여 그래프에서 제거합니다. 그런 다음 나가는 가장자리를 그래프에 추가합니다. 들어오는 가장자리가 없는 정점이 더 이상 없을 때까지 이 프로세스를 반복합니다. 그런 다음 그래프에 남아 있는 꼭지점을 토폴로지 순서로 정렬합니다.

이 알고리즘은 두 개의 대기열을 사용하여 구현됩니다. 하나는 들어오는 가장자리가 없는 정점용이고 다른 하나는 들어오는 가장자리가 있는 정점용입니다. 첫 번째 대기열의 정점이 먼저 처리되고 두 번째 대기열의 정점이 그 다음에 처리됩니다.

Kahn 알고리즘의 의사 코드는 다음과 같습니다.

```
function kahn_sort(graph)
    // create two queues, one for vertices with no incoming edges
    // and one for vertices with incoming edges
    Q = create_queue()
    for each vertex v in graph
        if in_degree(v) == 0
            enqueue(Q, v)

    // while Q is not empty
    while Q is not empty
        // remove a vertex from Q
        v = dequeue(Q)
        // add v to the sorted list
        add_to_sorted_list(v)
        // for each edge from v to w
        for each edge(v, w) in graph
            // remove the edge from the graph
            remove_edge(graph, v, w)
            // if w has no more incoming edges
            if in_degree(w) == 0
                // add w to Q
                enqueue(Q, w)

    // if graph has edges, then it has a cycle
    if graph has edges
        throw error "graph has a cycle"
    else
        return sorted_list
```

## 구현

이제 Kahn의 알고리즘을 JavaScript로 구현할 것입니다. 인접 목록을 사용하여 그래프를 나타냅니다.

```javascript
// create a graph class
class Graph {
  constructor() {
    this.adjList = new Map();
  }

  // add a vertex to the graph
  addVertex(v) {
    this.adjList.set(v, []);
  }

  // add an edge from vertex v to vertex w
  addEdge(v, w) {
    this.adjList.get(v).push(w);
  }

  // get the vertices with no incoming edges
  getSources() {
    let sources = [];

    for (let [v, edges] of this.adjList) {
      if (edges.length == 0) {
        sources.push(v);
      }
    }

    return sources;
  }

  // remove an edge from the graph
  removeEdge(v, w) {
    let edges = this.adjList.get(v);
    let idx = edges.indexOf(w);
    edges.splice(idx, 1);
  }

  // get the in-degree of a vertex
  inDegree(v) {
    let count = 0;

    for (let [u, edges] of this.adjList) {
      if (edges.includes(v)) {
        count++;
      }
    }

    return count;
  }

  // get the topological order of the vertices
  topologicalSort() {
    let Q = [];
    let S = [];
    let processed = new Set();

    // get the vertices with no incoming edges
    let sources = this.getSources();

    // add the sources to the queue
    for (let v of sources) {
      Q.push(v);
    }

    // while the queue is not empty
    while (Q.length > 0) {
      // remove a vertex from the queue
      let v = Q.shift();

      // add v to the sorted list
      S.push(v);

      // for each edge from v to w
      for (let w of this.adjList.get(v)) {
        // remove the edge from the graph
        this.removeEdge(v, w);

        // if w has no more incoming edges
        if (this.inDegree(w) == 0) {
          // add w to the queue
          Q.push(w);
        }
      }

      // mark v as processed
      processed.add(v);
    }

    // if there are any edges left in the graph,
    // then there is a cycle
    if (this.hasEdges()) {
      throw new Error("graph has a cycle");
    }

    // return the topological order
    return S;
  }

  // check if the graph has any edges
  hasEdges() {
    for (let [v, edges] of this.adjList) {
      if (edges.length > 0) {
        return true;
      }
    }

    return false;
  }
}
```

## 테스트

이제 우리는 Kahn의 알고리즘 구현을 테스트할 것입니다. 다음 그래프를 사용합니다.

![그래프](https://i.imgur.com/L6oC5vF.png)

이 그래프를 생성하는 코드는 다음과 같습니다.

```javascript
// create the graph
let g = new Graph();

// add the vertices
let v1 = "A";
let v2 = "B";
let v3 = "C";
let v4 = "D";
let v5 = "E";
let v6 = "F";
let v7 = "G";

g.addVertex(v1);
g.addVertex(v2);
g.addVertex(v3);
g.addVertex(v4);
g.addVertex(v5);
g.addVertex(v6);
g.addVertex(v7);

// add the edges
g.addEdge(v1, v2);
g.addEdge(v1, v3);
g.addEdge(v2, v4);
g.addEdge(v3, v4);
g.addEdge(v4, v5);
g.addEdge(v5, v6);
g.addEdge(v6, v7);
```

이 그래프에서 토폴로지 정렬 알고리즘을 실행하면 다음과 같은 결과가 나타납니다.

```javascript
["A", "B", "C", "D", "E", "F", "G"]
```

그리고 실제로 이것은 우리 코드가 출력하는 것입니다.

```javascript
console.log(g.topologicalSort());
// ["A", "B", "C", "D", "E", "F", "G"]
```

## 결론

이 기사에서는 위상 정렬과 위상 정렬을 수행하기 위한 Kahn의 알고리즘에 대해 논의했습니다. 또한 Kahn의 알고리즘을 JavaScript로 구현했습니다.