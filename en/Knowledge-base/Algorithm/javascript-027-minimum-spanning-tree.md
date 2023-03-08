---
title: [JavaScript] 027: Minimum Spanning Tree
description: 
published: true
date: 2023-02-10T05:33:13.275Z
tags: 
editor: markdown
dateCreated: 2023-02-10T05:33:06.786Z
---

- [[JavaScript] 027: árbol de expansión mínimo***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-027-minimum-spanning-tree)
{.links-list}
- [[JavaScript] 027：最小生成树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-027-minimum-spanning-tree)
{.links-list}
- [[JavaScript] 027: 최소 스패닝 트리***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-027-minimum-spanning-tree)
{.links-list}


# Minimum Spanning Tree

In computer science, a minimum spanning tree (MST) or minimum weight spanning tree is a subset of the edges of a undirected, weighted graph that connects all the vertices together, without any cycles and with the minimum possible total edge weight.

There are many applications for minimum spanning trees. For example, in a network of roads or communication lines, a minimum spanning tree can be used to find the cheapest way to connect all the nodes together. Another example is in cluster analysis, where a minimum spanning tree can be used to find groups of similar objects.

## Kruskal's algorithm

Kruskal's algorithm is a greedy algorithm that finds a minimum spanning tree for a connected weighted graph. It starts with the edges with the smallest weights and adds edges until it reaches a tree.

The algorithm works as follows:

1.  Sort the edges by weight from smallest to largest.

2.  Start with the edge with the smallest weight. If the edge doesn't create a cycle, add it to the tree.

3.  Repeat step 2 until there are no more edges to add.

The time complexity of Kruskal's algorithm is O(E log V), where E is the number of edges and V is the number of vertices.

## Prim's algorithm

Prim's algorithm is a greedy algorithm that finds a minimum spanning tree for a connected weighted graph. It starts with a vertex and adds the cheapest edges until it reaches a tree.

The algorithm works as follows:

1.  Start with a vertex.

2.  Find the cheapest edge from the vertex to another vertex.

3.  Add the edge to the tree.

4.  Repeat step 2 until there are no more edges to add.

The time complexity of Prim's algorithm is O(E log V), where E is the number of edges and V is the number of vertices.

## Code example

The following is a JavaScript implementation of Kruskal's algorithm.

```javascript
function kruskals(edges) {
  // sort edges by weight
  edges.sort((a, b) => a.weight - b.weight);

  // make a set for each vertex
  const sets = [];
  for (let i = 0; i < edges.length; i++) {
    sets.push(new Set([i]));
  }

  // list of edges in the MST
  const mst = [];

  // for each edge, check if it creates a cycle
  for (const edge of edges) {
    const [u, v] = edge.vertices;

    // if the edge doesn't create a cycle, add it to the MST
    if (!sets[u].has(v)) {
      mst.push(edge);

      // union the two sets
      const setU = sets[u];
      const setV = sets[v];
      for (const vertex of setV) {
        setU.add(vertex);
        sets[vertex] = setU;
      }
    }
  }

  return mst;
}
```

## Exercise

1.  Use Kruskal's algorithm to find the minimum spanning tree for the following graph:

    ![](https://i.imgur.com/lVqnqj7.png)

2.  Use Prim's algorithm to find the minimum spanning tree for the following graph:

    ![](https://i.imgur.com/kzFcNcu.png)

## Answers

1.  The minimum spanning tree for the graph is shown below. The total weight of the tree is 9.

    ![](https://i.imgur.com/zM0FtqD.png)

2.  The minimum spanning tree for the graph is shown below. The total weight of the tree is 10.

    ![](https://i.imgur.com/kzFcNcu.png)