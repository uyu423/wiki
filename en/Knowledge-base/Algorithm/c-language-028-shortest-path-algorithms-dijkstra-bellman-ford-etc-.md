---
title: [C Language] 028: Shortest Path Algorithms (Dijkstra, Bellman-Ford, etc.)
description: 
published: true
date: 2023-02-13T09:33:00.724Z
tags: 
editor: markdown
dateCreated: 2023-02-13T09:32:53.202Z
---

- [[Lenguaje C] 028: algoritmos de ruta más corta (Dijkstra, Bellman-Ford, etc.)***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-028-shortest-path-algorithms-dijkstra-bellman-ford-etc-)
{.links-list}
- [[C语言]028：最短路径算法（Dijkstra、Bellman-Ford等）***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-028-shortest-path-algorithms-dijkstra-bellman-ford-etc-)
{.links-list}
- [[C 언어] 028: 최단 경로 알고리즘(Dijkstra, Bellman-Ford 등)***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-028-shortest-path-algorithms-dijkstra-bellman-ford-etc-)
{.links-list}


# 028: Shortest Path Algorithms (Dijkstra, Bellman-Ford, etc.)

In this post, we will be discussing shortest path algorithms. In particular, we will be focusing on three algorithms: Dijkstra, Bellman-Ford, and A*.

## Dijkstra

Dijkstra's algorithm is a greedy algorithm that finds the shortest path from a starting vertex to all other vertices in a graph. The algorithm works by maintaining a set of visited vertices and a set of unvisited vertices. The algorithm starts at the starting vertex and relaxes all of its edges. That is, it updates the distance to all adjacent vertices if the new distance is shorter than the old distance. The algorithm then moves on to the next unvisited vertex and repeats the process. The algorithm terminates when all vertices have been visited.

The following is pseudocode for Dijkstra's algorithm:

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

## Bellman-Ford

Bellman-Ford's algorithm is similar to Dijkstra's algorithm in that it finds the shortest path from a starting vertex to all other vertices in a graph. However, unlike Dijkstra's algorithm, Bellman-Ford's algorithm can handle graphs with negative edge weights. The algorithm works by maintaining an array of distances from the starting vertex to all other vertices. The algorithm then relaxes all edges in the graph. That is, it updates the distance to all adjacent vertices if the new distance is shorter than the old distance. The algorithm then repeats this process until all edges have been relaxed a certain number of times (i.e. the number of vertices in the graph).

The following is pseudocode for Bellman-Ford's algorithm:

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

A* is an algorithm that finds the shortest path from a starting vertex to a goal vertex in a graph. The algorithm works by maintaining a set of visited vertices and a set of unvisited vertices. The algorithm also maintain a priority queue of vertices based on a heuristic function. The heuristic function estimates the distance from a vertex to the goal vertex. The algorithm starts at the starting vertex and relaxes all of its edges. That is, it updates the distance to all adjacent vertices if the new distance is shorter than the old distance. The algorithm then moves on to the next vertex in the priority queue and repeats the process. The algorithm terminates when the goal vertex has been visited.

The following is pseudocode for A*:

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

## Conclusion

In this post, we have discussed three shortest path algorithms: Dijkstra, Bellman-Ford, and A*. We have seen that each algorithm has its own strengths and weaknesses. Dijkstra's algorithm is the simplest of the three algorithms and can be used when the edge weights are positive. Bellman-Ford's algorithm can be used when the edge weights are negative. A* can be used when the goal vertex is known.