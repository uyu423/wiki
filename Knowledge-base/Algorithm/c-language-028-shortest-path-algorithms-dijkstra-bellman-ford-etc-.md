---
title: [C 언어] 028: 최단 경로 알고리즘(Dijkstra, Bellman-Ford 등)
description: 
published: true
date: 2023-02-13T09:32:55.505Z
tags: 
editor: markdown
dateCreated: 2023-02-13T09:32:53.197Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 028: Shortest Path Algorithms (Dijkstra, Bellman-Ford, etc.)***English** document is available*](/en/Knowledge-base/Algorithm/c-language-028-shortest-path-algorithms-dijkstra-bellman-ford-etc-)
{.links-list}


# 028: 최단 경로 알고리즘(Dijkstra, Bellman-Ford 등)

이번 포스팅에서는 최단경로 알고리즘에 대해 알아보겠습니다. 특히 Dijkstra, Bellman-Ford 및 A*의 세 가지 알고리즘에 중점을 둘 것입니다.

## 다익스트라

Dijkstra의 알고리즘은 그래프의 시작 정점에서 다른 모든 정점까지의 최단 경로를 찾는 그리디 알고리즘입니다. 이 알고리즘은 방문한 정점 집합과 방문하지 않은 정점 집합을 유지하는 방식으로 작동합니다. 알고리즘은 시작 정점에서 시작하여 모든 가장자리를 완화합니다. 즉, 새 거리가 이전 거리보다 짧은 경우 인접한 모든 정점까지의 거리를 업데이트합니다. 그런 다음 알고리즘은 방문하지 않은 다음 정점으로 이동하고 프로세스를 반복합니다. 모든 정점을 방문하면 알고리즘이 종료됩니다.

다음은 Dijkstra 알고리즘의 의사 코드입니다.

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

## 벨만-포드

Bellman-Ford의 알고리즘은 그래프의 시작 정점에서 다른 모든 정점까지의 최단 경로를 찾는다는 점에서 Dijkstra의 알고리즘과 유사합니다. 그러나 Dijkstra의 알고리즘과 달리 Bellman-Ford의 알고리즘은 음수 간선 가중치가 있는 그래프를 처리할 수 있습니다. 이 알고리즘은 시작 정점에서 다른 모든 정점까지의 거리 배열을 유지하는 방식으로 작동합니다. 그런 다음 알고리즘은 그래프의 모든 가장자리를 완화합니다. 즉, 새 거리가 이전 거리보다 짧은 경우 인접한 모든 정점까지의 거리를 업데이트합니다. 그런 다음 알고리즘은 모든 가장자리가 특정 횟수(즉, 그래프의 정점 수)만큼 완화될 때까지 이 프로세스를 반복합니다.

다음은 Bellman-Ford 알고리즘의 의사 코드입니다.

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

## ㅏ*

A*는 그래프의 시작 정점에서 목표 정점까지의 최단 경로를 찾는 알고리즘입니다. 이 알고리즘은 방문한 정점 집합과 방문하지 않은 정점 집합을 유지하는 방식으로 작동합니다. 알고리즘은 휴리스틱 함수를 기반으로 정점의 우선순위 대기열도 유지합니다. 휴리스틱 함수는 정점에서 목표 정점까지의 거리를 추정합니다. 알고리즘은 시작 정점에서 시작하여 모든 가장자리를 완화합니다. 즉, 새 거리가 이전 거리보다 짧은 경우 인접한 모든 정점까지의 거리를 업데이트합니다. 그런 다음 알고리즘은 우선 순위 대기열의 다음 정점으로 이동하고 프로세스를 반복합니다. 목표 정점을 방문하면 알고리즘이 종료됩니다.

다음은 A*에 대한 의사 코드입니다.

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

## 결론

이 게시물에서는 Dijkstra, Bellman-Ford 및 A*의 세 가지 최단 경로 알고리즘에 대해 논의했습니다. 우리는 각 알고리즘이 고유한 강점과 약점을 가지고 있음을 확인했습니다. Dijkstra의 알고리즘은 세 가지 알고리즘 중 가장 단순하며 에지 가중치가 양수일 때 사용할 수 있습니다. 에지 가중치가 음수일 때 Bellman-Ford 알고리즘을 사용할 수 있습니다. A*는 목표 정점을 알고 있을 때 사용할 수 있습니다.