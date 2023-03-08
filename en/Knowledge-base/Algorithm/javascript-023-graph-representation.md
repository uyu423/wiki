---
title: [JavaScript] 023: Graph Representation
description: 
published: true
date: 2023-02-10T01:32:34.939Z
tags: 
editor: markdown
dateCreated: 2023-02-10T01:32:28.220Z
---

- [[JavaScript] 023: Representación gráfica***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-023-graph-representation)
{.links-list}
- [[JavaScript] 023：图形表示***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-023-graph-representation)
{.links-list}
- [[JavaScript] 023: 그래프 표현***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-023-graph-representation)
{.links-list}


# Graph Representation

A graph can be represented in many ways, but there are two main ways: adjacency lists and adjacency matrices. In this post, we'll look at both of these methods and see their pros and cons.

## Adjacency Lists

An adjacency list is simply a list of all the vertices adjacent to a given vertex. For example, consider the following graph:

![alt text](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/adjacency_list_1.png)

The adjacency list for this graph would be:

```
A: B, C
B: A, C, D
C: A, B, D
D: B, C
```

As you can see, each vertex is listed, along with all the vertices it is adjacent to.

Adjacency lists have the advantage of being simple and easy to implement. They also use less space than adjacency matrices, since we only need to store the edges for each vertex, not all the edges for the entire graph.

The downside of adjacency lists is that they can be slower to query. For example, if we want to know if there is an edge between vertices A and D, we would need to look at the adjacency list for both A and D to see if either of them lists the other. In contrast, with an adjacency matrix, we can just look at the entry for A and D and see if it is non-zero.

## Adjacency Matrices

An adjacency matrix is a matrix (2D array) where each row and column represents a vertex, and the value at each row/column intersection is the weight of the edge between those two vertices. For example, consider the following graph:

![alt text](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/adjacency_matrix_1.png)

The adjacency matrix for this graph would be:

```
  A B C D
A 0 1 1 0
B 1 0 1 1
C 1 1 0 1
D 0 1 1 0
```

As you can see, each row and column represents a vertex, and the value at each row/column intersection is the weight of the edge between those two vertices. If there is no edge between two vertices, the weight is 0.

Adjacency matrices have the advantage of being very fast to query. For example, if we want to know if there is an edge between vertices A and D, we can just look at the entry for A and D and see if it is non-zero. In contrast, with an adjacency list, we would need to look at the adjacency list for both A and D to see if either of them lists the other.

The downside of adjacency matrices is that they can use more space than adjacency lists. For example, in our graph above, there are only 16 edges, but the adjacency matrix has 16 * 4 = 64 entries. In general, an adjacency matrix will use O(V^2) space, where V is the number of vertices.

## Which Should I Use?

Adjacency lists are generally used when the graph is sparse, meaning there are not a lot of edges. Adjacency matrices are generally used when the graph is dense, meaning there are a lot of edges.

There is no right or wrong answer, and it is often possible to use either representation. In general, adjacency lists are easier to implement, but adjacency matrices are faster to query.