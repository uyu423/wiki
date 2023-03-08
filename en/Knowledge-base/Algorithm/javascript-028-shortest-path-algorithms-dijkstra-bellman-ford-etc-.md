---
title: [JavaScript] 028: Shortest Path Algorithms (Dijkstra, Bellman-Ford, etc.)
description: 
published: true
date: 2023-02-10T06:32:30.308Z
tags: 
editor: markdown
dateCreated: 2023-02-10T06:32:28.606Z
---

- [[JavaScript] 028: algoritmos de ruta más corta (Dijkstra, Bellman-Ford, etc.)***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-028-shortest-path-algorithms-dijkstra-bellman-ford-etc-)
{.links-list}
- [[JavaScript] 028：最短路径算法（Dijkstra、Bellman-Ford等）***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-028-shortest-path-algorithms-dijkstra-bellman-ford-etc-)
{.links-list}
- [[JavaScript] 028: 최단 경로 알고리즘(Dijkstra, Bellman-Ford 등)***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-028-shortest-path-algorithms-dijkstra-bellman-ford-etc-)
{.links-list}


# Shortest Path Algorithms

In computer science, a shortest path algorithm is an algorithm that solves the shortest path problem. The shortest path problem is the problem of finding a path between two vertices (or nodes) in a graph such that the sum of the weights of the edges along the path is minimized.

There are many different algorithms for solving the shortest path problem, including the well-known Dijkstra's algorithm and the Bellman-Ford algorithm. In this post, we will take a look at some of the most popular shortest path algorithms and see how they work.

## Dijkstra's Algorithm

Dijkstra's algorithm is a greedy algorithm that solves the shortest path problem. The algorithm works by keeping track of the shortest path from the starting vertex to all other vertices in the graph.

The algorithm works by visiting each vertex in the graph, starting with the starting vertex. For each vertex, the algorithm calculates the shortest path from the starting vertex to that vertex. The shortest path is then updated if a shorter path is found.

The algorithm continues until all vertices have been visited. At the end, the shortest path from the starting vertex to all other vertices will have been found.

Here is a pseudocode implementation of Dijkstra's algorithm:

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

## Bellman-Ford Algorithm

The Bellman-Ford algorithm is a dynamic programming algorithm that solves the shortest path problem. The algorithm works by keeping track of the shortest path from the starting vertex to all other vertices in the graph.

The algorithm works by visiting each vertex in the graph, starting with the starting vertex. For each vertex, the algorithm calculates the shortest path from the starting vertex to that vertex. The shortest path is then updated if a shorter path is found.

The algorithm continues until all vertices have been visited. At the end, the shortest path from the starting vertex to all other vertices will have been found.

Here is a pseudocode implementation of the Bellman-Ford algorithm:

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

## Conclusion

In this post, we have looked at some of the most popular shortest path algorithms. These algorithms are used to find the shortest path between two vertices in a graph.

We have seen how the Dijkstra's algorithm and the Bellman-Ford algorithm work. These algorithms are both efficient ways to find the shortest path between two vertices in a graph.