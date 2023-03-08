---
title: [JavaScript] 028: 최단 경로 알고리즘(Dijkstra, Bellman-Ford 등)
description: 
published: true
date: 2023-02-10T06:32:34.954Z
tags: 
editor: markdown
dateCreated: 2023-02-10T06:32:28.598Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 028: Shortest Path Algorithms (Dijkstra, Bellman-Ford, etc.)***English** document is available*](/en/Knowledge-base/Algorithm/javascript-028-shortest-path-algorithms-dijkstra-bellman-ford-etc-)
{.links-list}


# 최단 경로 알고리즘

컴퓨터 과학에서 최단 경로 알고리즘은 최단 경로 문제를 해결하는 알고리즘입니다. 최단 경로 문제는 경로를 따라 에지의 가중치 합이 최소화되도록 그래프에서 두 정점(또는 노드) 사이의 경로를 찾는 문제입니다.

잘 알려진 Dijkstra의 알고리즘과 Bellman-Ford 알고리즘을 포함하여 최단 경로 문제를 해결하기 위한 다양한 알고리즘이 있습니다. 이 게시물에서는 가장 인기 있는 최단 경로 알고리즘을 살펴보고 작동 방식을 살펴보겠습니다.

## Dijkstra의 알고리즘

Dijkstra의 알고리즘은 최단 경로 문제를 해결하는 그리디 알고리즘입니다. 이 알고리즘은 시작 정점에서 그래프의 다른 모든 정점까지의 최단 경로를 추적하여 작동합니다.

알고리즘은 시작 정점부터 시작하여 그래프의 각 정점을 방문하여 작동합니다. 각 정점에 대해 알고리즘은 시작 정점에서 해당 정점까지의 최단 경로를 계산합니다. 더 짧은 경로가 발견되면 최단 경로가 업데이트됩니다.

알고리즘은 모든 정점을 방문할 때까지 계속됩니다. 결국 시작 정점에서 다른 모든 정점까지의 최단 경로가 발견됩니다.

다음은 Dijkstra 알고리즘의 의사 코드 구현입니다.

```
function dijkstra(graph, start) {
  // create an empty set to track visited vertices
  let visited = new Set();
  
  // create an empty set to track unvisited vertices
  let unvisited = new Set();
  
  // add all vertices to the unvisited set
  for (let vertex of graph.vertices) {
    unvisited.add(vertex);
  }
  
  // create an empty map to track the shortest path from the starting vertex to all other vertices
  let shortestPath = new Map();
  
  // set the starting vertex's shortest path to 0
  shortestPath.set(start, 0);
  
  // while there are still unvisited vertices
  while (unvisited.size > 0) {
    // find the unvisited vertex with the shortest path from the starting vertex
    let currentVertex = findVertexWithShortestPath(unvisited, shortestPath);
    
    // remove the current vertex from the unvisited set
    unvisited.delete(currentVertex);
    
    // for each neighbor of the current vertex
    for (let neighbor of currentVertex.neighbors) {
      // if the neighbor has not been visited
      if (!visited.has(neighbor)) {
        // calculate the shortest path from the starting vertex to the neighbor
        let path = shortestPath.get(currentVertex) + currentVertex.weight(neighbor);
        
        // if the neighbor does not have a shortest path or if the path to the neighbor is shorter than the current shortest path
        if (!shortestPath.has(neighbor) || path < shortestPath.get(neighbor)) {
          // update the shortest path for the neighbor
          shortestPath.set(neighbor, path);
        }
      }
    }
    
    // add the current vertex to the visited set
    visited.add(currentVertex);
  }
  
  // return the shortest path from the starting vertex to all other vertices
  return shortestPath;
}
```

## 벨만-포드 알고리즘

Bellman-Ford 알고리즘은 최단 경로 문제를 해결하는 동적 프로그래밍 알고리즘입니다. 이 알고리즘은 시작 정점에서 그래프의 다른 모든 정점까지의 최단 경로를 추적하여 작동합니다.

알고리즘은 시작 정점부터 시작하여 그래프의 각 정점을 방문하여 작동합니다. 각 정점에 대해 알고리즘은 시작 정점에서 해당 정점까지의 최단 경로를 계산합니다. 더 짧은 경로가 발견되면 최단 경로가 업데이트됩니다.

알고리즘은 모든 정점을 방문할 때까지 계속됩니다. 결국 시작 정점에서 다른 모든 정점까지의 최단 경로가 발견됩니다.

다음은 Bellman-Ford 알고리즘의 의사 코드 구현입니다.

```
function bellmanFord(graph, start) {
  // create an empty map to track the shortest path from the starting vertex to all other vertices
  let shortestPath = new Map();
  
  // set the starting vertex's shortest path to 0
  shortestPath.set(start, 0);
  
  // for each vertex in the graph
  for (let vertex of graph.vertices) {
    // for each neighbor of the vertex
    for (let neighbor of vertex.neighbors) {
      // if the neighbor does not have a shortest path or if the path to the neighbor is shorter than the current shortest path
      if (!shortestPath.has(neighbor) || shortestPath.get(vertex) + vertex.weight(neighbor) < shortestPath.get(neighbor)) {
        // update the shortest path for the neighbor
        shortestPath.set(neighbor, shortestPath.get(vertex) + vertex.weight(neighbor));
      }
    }
  }
  
  // return the shortest path from the starting vertex to all other vertices
  return shortestPath;
}
```

## 결론

이 게시물에서는 가장 인기 있는 최단 경로 알고리즘을 살펴보았습니다. 이 알고리즘은 그래프에서 두 정점 사이의 최단 경로를 찾는 데 사용됩니다.

우리는 Dijkstra의 알고리즘과 Bellman-Ford 알고리즘이 어떻게 작동하는지 살펴보았습니다. 이 알고리즘은 둘 다 그래프에서 두 정점 사이의 최단 경로를 찾는 효율적인 방법입니다.