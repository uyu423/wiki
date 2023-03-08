---
title: [JavaScript] 028: algoritmos de ruta más corta (Dijkstra, Bellman-Ford, etc.)
description: 
published: true
date: 2023-02-10T06:32:34.954Z
tags: 
editor: markdown
dateCreated: 2023-02-10T06:32:28.603Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 028: Shortest Path Algorithms (Dijkstra, Bellman-Ford, etc.)***English** document is available*](/en/Knowledge-base/Algorithm/javascript-028-shortest-path-algorithms-dijkstra-bellman-ford-etc-)
{.links-list}


# Algoritmos de ruta más corta

En informática, un algoritmo de ruta más corta es un algoritmo que resuelve el problema de la ruta más corta. El problema del camino más corto es el problema de encontrar un camino entre dos vértices (o nodos) en un gráfico tal que la suma de los pesos de los bordes a lo largo del camino se minimice.

Hay muchos algoritmos diferentes para resolver el problema del camino más corto, incluido el conocido algoritmo de Dijkstra y el algoritmo de Bellman-Ford. En esta publicación, veremos algunos de los algoritmos de ruta más corta más populares y veremos cómo funcionan.

## Algoritmo de Dijkstra

El algoritmo de Dijkstra es un algoritmo codicioso que resuelve el problema del camino más corto. El algoritmo funciona haciendo un seguimiento del camino más corto desde el vértice inicial hasta todos los demás vértices del gráfico.

El algoritmo funciona visitando cada vértice del gráfico, comenzando por el vértice inicial. Para cada vértice, el algoritmo calcula el camino más corto desde el vértice inicial hasta ese vértice. La ruta más corta se actualiza si se encuentra una ruta más corta.

El algoritmo continúa hasta que se han visitado todos los vértices. Al final, se habrá encontrado el camino más corto desde el vértice inicial hasta todos los demás vértices.

Aquí hay una implementación de pseudocódigo del algoritmo de Dijkstra:

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

## Algoritmo Bellman-Ford

El algoritmo Bellman-Ford es un algoritmo de programación dinámica que resuelve el problema del camino más corto. El algoritmo funciona haciendo un seguimiento del camino más corto desde el vértice inicial hasta todos los demás vértices del gráfico.

El algoritmo funciona visitando cada vértice del gráfico, comenzando por el vértice inicial. Para cada vértice, el algoritmo calcula el camino más corto desde el vértice inicial hasta ese vértice. La ruta más corta se actualiza si se encuentra una ruta más corta.

El algoritmo continúa hasta que se han visitado todos los vértices. Al final, se habrá encontrado el camino más corto desde el vértice inicial hasta todos los demás vértices.

Aquí hay una implementación de pseudocódigo del algoritmo Bellman-Ford:

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

## Conclusión

En esta publicación, hemos analizado algunos de los algoritmos de ruta más corta más populares. Estos algoritmos se utilizan para encontrar el camino más corto entre dos vértices en un gráfico.

Hemos visto cómo funcionan el algoritmo de Dijkstra y el algoritmo de Bellman-Ford. Estos algoritmos son formas eficientes de encontrar el camino más corto entre dos vértices en un gráfico.