---
title: [C语言]028：最短路径算法（Dijkstra、Bellman-Ford等）
description: 
published: true
date: 2023-02-13T09:32:54.966Z
tags: 
editor: markdown
dateCreated: 2023-02-13T09:32:53.193Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 028: Shortest Path Algorithms (Dijkstra, Bellman-Ford, etc.)***English** document is available*](/en/Knowledge-base/Algorithm/c-language-028-shortest-path-algorithms-dijkstra-bellman-ford-etc-)
{.links-list}


# 028：最短路径算法（Dijkstra、Bellman-Ford 等）

在这篇文章中，我们将讨论最短路径算法。我们将特别关注三种算法：Dijkstra、Bellman-Ford 和 A*。

## 迪克斯特拉

Dijkstra 算法是一种贪心算法，它寻找从起始顶点到图中所有其他顶点的最短路径。该算法通过维护一组已访问的顶点和一组未访问的顶点来工作。该算法从起始顶点开始并放松其所有边。也就是说，如果新距离小于旧距离，它会更新到所有相邻顶点的距离。然后算法移动到下一个未访问的顶点并重复该过程。当所有顶点都被访问时，算法终止。

以下是 Dijkstra 算法的伪代码：

```
function Dijkstra(G, s):
  for each vertex v in G:
    distance[v] := infinity
    previous[v] := null
  distance[s] := 0
  Q := G.vertices
  while Q is not empty:
    u := vertex in Q with smallest distance[]
    remove u from Q
    for each neighbor v of u:
      alt := distance[u] + length(u, v)
      if alt < distance[v]:
        distance[v] := alt
        previous[v] := u
  return distance[], previous[]
```

## 贝尔曼-福特

Bellman-Ford 算法与 Dijkstra 算法的相似之处在于它寻找从起始顶点到图中所有其他顶点的最短路径。但是，与 Dijkstra 算法不同，Bellman-Ford 算法可以处理边权为负的图。该算法通过维护从起始顶点到所有其他顶点的距离数组来工作。该算法然后松弛图中的所有边。也就是说，如果新距离小于旧距离，它会更新到所有相邻顶点的距离。然后该算法重复此过程，直到所有边都松弛了一定次数（即图中的顶点数）。

以下是 Bellman-Ford 算法的伪代码：

```
function BellmanFord(G, s):
  for each vertex v in G:
    distance[v] := infinity
    previous[v] := null
  distance[s] := 0
  for i := 1 to size(G):
    for each edge (u, v) in G:
      alt := distance[u] + length(u, v)
      if alt < distance[v]:
        distance[v] := alt
        previous[v] := u
  return distance[], previous[]
```

## A*

A* 是一种算法，用于查找图中从起始顶点到目标顶点的最短路径。该算法通过维护一组已访问的顶点和一组未访问的顶点来工作。该算法还维护一个基于启发式函数的顶点优先级队列。启发式函数估计从顶点到目标顶点的距离。该算法从起始顶点开始并放松其所有边。也就是说，如果新距离小于旧距离，它会更新到所有相邻顶点的距离。然后算法移动到优先级队列中的下一个顶点并重复该过程。当访问了目标顶点时，算法终止。

以下是 A* 的伪代码：

```
function A*(G, s, g):
  for each vertex v in G:
    distance[v] := infinity
    previous[v] := null
    heuristic[v] := estimateDistance(v, g)
  distance[s] := 0
  Q := G.vertices
  while Q is not empty:
    u := vertex in Q with smallest heuristic[]
    remove u from Q
    for each neighbor v of u:
      alt := distance[u] + length(u, v)
      if alt < distance[v]:
        distance[v] := alt
        previous[v] := u
  return distance[], previous[]
```

## 结论

在本文中，我们讨论了三种最短路径算法：Dijkstra、Bellman-Ford 和 A*。我们已经看到每种算法都有自己的优点和缺点。 Dijkstra 算法是三种算法中最简单的，当边权为正时可以使用。当边权为负时，可以使用 Bellman-Ford 算法。当目标顶点已知时可以使用 A*。