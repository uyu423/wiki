---
title: [Lenguaje C] 028: algoritmos de ruta más corta (Dijkstra, Bellman-Ford, etc.)
description: 
published: true
date: 2023-02-13T09:32:54.963Z
tags: 
editor: markdown
dateCreated: 2023-02-13T09:32:53.194Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 028: Shortest Path Algorithms (Dijkstra, Bellman-Ford, etc.)***English** document is available*](/en/Knowledge-base/Algorithm/c-language-028-shortest-path-algorithms-dijkstra-bellman-ford-etc-)
{.links-list}


# 028: Algoritmos de ruta más corta (Dijkstra, Bellman-Ford, etc.)

En esta publicación, discutiremos los algoritmos de ruta más corta. En particular, nos centraremos en tres algoritmos: Dijkstra, Bellman-Ford y A*.

## Dijkstra

El algoritmo de Dijkstra es un algoritmo codicioso que encuentra el camino más corto desde un vértice inicial a todos los demás vértices en un gráfico. El algoritmo funciona manteniendo un conjunto de vértices visitados y un conjunto de vértices no visitados. El algoritmo comienza en el vértice inicial y relaja todos sus bordes. Es decir, actualiza la distancia a todos los vértices adyacentes si la nueva distancia es más corta que la anterior. Luego, el algoritmo pasa al siguiente vértice no visitado y repite el proceso. El algoritmo termina cuando se han visitado todos los vértices.

El siguiente es el pseudocódigo del algoritmo de Dijkstra:

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

El algoritmo de Bellman-Ford es similar al algoritmo de Dijkstra en que encuentra el camino más corto desde un vértice inicial a todos los demás vértices en un gráfico. Sin embargo, a diferencia del algoritmo de Dijkstra, el algoritmo de Bellman-Ford puede manejar gráficos con pesos de borde negativos. El algoritmo funciona manteniendo una serie de distancias desde el vértice inicial hasta todos los demás vértices. Luego, el algoritmo relaja todos los bordes del gráfico. Es decir, actualiza la distancia a todos los vértices adyacentes si la nueva distancia es más corta que la anterior. Luego, el algoritmo repite este proceso hasta que todos los bordes se hayan relajado una cierta cantidad de veces (es decir, la cantidad de vértices en el gráfico).

El siguiente es un pseudocódigo para el algoritmo de Bellman-Ford:

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

A* es un algoritmo que encuentra el camino más corto desde un vértice inicial hasta un vértice objetivo en un gráfico. El algoritmo funciona manteniendo un conjunto de vértices visitados y un conjunto de vértices no visitados. El algoritmo también mantiene una cola de prioridad de vértices basada en una función heurística. La función heurística estima la distancia desde un vértice hasta el vértice objetivo. El algoritmo comienza en el vértice inicial y relaja todos sus bordes. Es decir, actualiza la distancia a todos los vértices adyacentes si la nueva distancia es más corta que la anterior. Luego, el algoritmo pasa al siguiente vértice en la cola de prioridad y repite el proceso. El algoritmo termina cuando se ha visitado el vértice objetivo.

El siguiente es el pseudocódigo para A*:

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

## Conclusión

En esta publicación, hemos discutido tres algoritmos de ruta más corta: Dijkstra, Bellman-Ford y A*. Hemos visto que cada algoritmo tiene sus propias fortalezas y debilidades. El algoritmo de Dijkstra es el más simple de los tres algoritmos y se puede usar cuando los pesos de los bordes son positivos. El algoritmo de Bellman-Ford se puede utilizar cuando los pesos de los bordes son negativos. Se puede utilizar A* cuando se conoce el vértice de la meta.