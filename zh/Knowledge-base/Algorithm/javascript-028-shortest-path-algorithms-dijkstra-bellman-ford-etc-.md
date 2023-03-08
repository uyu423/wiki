---
title: [JavaScript] 028：最短路径算法（Dijkstra、Bellman-Ford等）
description: 
published: true
date: 2023-02-10T06:32:34.954Z
tags: 
editor: markdown
dateCreated: 2023-02-10T06:32:28.602Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 028: Shortest Path Algorithms (Dijkstra, Bellman-Ford, etc.)***English** document is available*](/en/Knowledge-base/Algorithm/javascript-028-shortest-path-algorithms-dijkstra-bellman-ford-etc-)
{.links-list}


# 最短路径算法

在计算机科学中，最短路径算法是解决最短路径问题的算法。最短路径问题是在图中的两个顶点（或节点）之间找到一条路径，使得沿路径的边的权重之和最小的问题。

解决最短路径问题的算法有很多种，包括著名的 Dijkstra 算法和 Bellman-Ford 算法。在本文中，我们将了解一些最流行的最短路径算法并了解它们的工作原理。

## Dijkstra 算法

Dijkstra 算法是解决最短路径问题的贪心算法。该算法通过跟踪从起始顶点到图中所有其他顶点的最短路径来工作。

该算法通过访问图中的每个顶点来工作，从起始顶点开始。对于每个顶点，该算法计算从起始顶点到该顶点的最短路径。如果找到更短的路径，则更新最短路径。

该算法一直持续到所有顶点都被访问过为止。最后，将找到从起始顶点到所有其他顶点的最短路径。

下面是 Dijkstra 算法的伪代码实现：

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

## 贝尔曼-福特算法

Bellman-Ford算法是一种求解最短路径问题的动态规划算法。该算法通过跟踪从起始顶点到图中所有其他顶点的最短路径来工作。

该算法通过访问图中的每个顶点来工作，从起始顶点开始。对于每个顶点，该算法计算从起始顶点到该顶点的最短路径。如果找到更短的路径，则更新最短路径。

该算法一直持续到所有顶点都被访问过为止。最后，将找到从起始顶点到所有其他顶点的最短路径。

下面是 Bellman-Ford 算法的伪代码实现：

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

## 结论

在这篇文章中，我们研究了一些最流行的最短路径算法。这些算法用于查找图中两个顶点之间的最短路径。

我们已经了解了 Dijkstra 算法和 Bellman-Ford 算法的工作原理。这些算法都是寻找图中两个顶点之间最短路径的有效方法。