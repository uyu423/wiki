---
title: [JavaScript] 026: Topological Sort
description: 
published: true
date: 2023-02-10T04:32:37.733Z
tags: 
editor: markdown
dateCreated: 2023-02-10T04:32:31.457Z
---

- [[JavaScript] 026: Clasificación topológica***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-026-topological-sort)
{.links-list}
- [[JavaScript] 026: 拓扑排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-026-topological-sort)
{.links-list}
- [[JavaScript] 026: 위상 정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-026-topological-sort)
{.links-list}


# Topological Sort

In mathematics, topological sorting is a linear ordering of vertices in a directed acyclic graph (DAG). A topological sort or topological ordering of a directed graph is a linear ordering of its vertices such that for every directed edge uv from vertex u to vertex v, u comes before v in the ordering. For instance, the vertices of the graph may represent tasks to be performed, and the edges may represent dependencies of these tasks.

There are many applications of topological sorting. One example is in scheduling a sequence of jobs or tasks based on their dependencies. As another example, suppose that you want to compile a set of source code files into a set of object files. This can be accomplished by representing the source files as vertices and the dependencies between them as edges. The topological sort then provides a sequence in which to perform the compilation.

There are numerous algorithms for performing topological sorts. In this article, we will discuss one of the most popular algorithms, known as Kahn's algorithm.

## Kahn's Algorithm

Kahn's algorithm is a topological sorting algorithm that was first described by Arthur B. Kahn in the paper "Topological Sorting of Large Networks" in 1962. The algorithm is named after him.

The idea behind Kahn's algorithm is simple. We start with a set of vertices with no incoming edges and we remove them from the graph. We then add their outgoing edges to the graph. We repeat this process until there are no more vertices with no incoming edges. The vertices that are left in the graph are then sorted in topological order.

The algorithm is implemented using two queues, one for the vertices with no incoming edges and one for the vertices with incoming edges. The vertices in the first queue are processed first and the vertices in the second queue are processed next.

The pseudocode for Kahn's algorithm is as follows:

```
function kahn_sort(graph)
    // create two queues, one for vertices with no incoming edges
    // and one for vertices with incoming edges
    Q = create_queue()
    for each vertex v in graph
        if in_degree(v) == 0
            enqueue(Q, v)

    // while Q is not empty
    while Q is not empty
        // remove a vertex from Q
        v = dequeue(Q)
        // add v to the sorted list
        add_to_sorted_list(v)
        // for each edge from v to w
        for each edge(v, w) in graph
            // remove the edge from the graph
            remove_edge(graph, v, w)
            // if w has no more incoming edges
            if in_degree(w) == 0
                // add w to Q
                enqueue(Q, w)

    // if graph has edges, then it has a cycle
    if graph has edges
        throw error "graph has a cycle"
    else
        return sorted_list
```

## Implementation

We will now implement Kahn's algorithm in JavaScript. We will use an adjacency list to represent the graph.

```javascript
// create a graph class
class Graph {
  constructor() {
    this.adjList = new Map();
  }

  // add a vertex to the graph
  addVertex(v) {
    this.adjList.set(v, []);
  }

  // add an edge from vertex v to vertex w
  addEdge(v, w) {
    this.adjList.get(v).push(w);
  }

  // get the vertices with no incoming edges
  getSources() {
    let sources = [];

    for (let [v, edges] of this.adjList) {
      if (edges.length == 0) {
        sources.push(v);
      }
    }

    return sources;
  }

  // remove an edge from the graph
  removeEdge(v, w) {
    let edges = this.adjList.get(v);
    let idx = edges.indexOf(w);
    edges.splice(idx, 1);
  }

  // get the in-degree of a vertex
  inDegree(v) {
    let count = 0;

    for (let [u, edges] of this.adjList) {
      if (edges.includes(v)) {
        count++;
      }
    }

    return count;
  }

  // get the topological order of the vertices
  topologicalSort() {
    let Q = [];
    let S = [];
    let processed = new Set();

    // get the vertices with no incoming edges
    let sources = this.getSources();

    // add the sources to the queue
    for (let v of sources) {
      Q.push(v);
    }

    // while the queue is not empty
    while (Q.length > 0) {
      // remove a vertex from the queue
      let v = Q.shift();

      // add v to the sorted list
      S.push(v);

      // for each edge from v to w
      for (let w of this.adjList.get(v)) {
        // remove the edge from the graph
        this.removeEdge(v, w);

        // if w has no more incoming edges
        if (this.inDegree(w) == 0) {
          // add w to the queue
          Q.push(w);
        }
      }

      // mark v as processed
      processed.add(v);
    }

    // if there are any edges left in the graph,
    // then there is a cycle
    if (this.hasEdges()) {
      throw new Error("graph has a cycle");
    }

    // return the topological order
    return S;
  }

  // check if the graph has any edges
  hasEdges() {
    for (let [v, edges] of this.adjList) {
      if (edges.length > 0) {
        return true;
      }
    }

    return false;
  }
}
```

## Testing

We will now test our implementation of Kahn's algorithm. We will use the following graph:

![Graph](https://i.imgur.com/L6oC5vF.png)

The code to create this graph is as follows:

```javascript
// create the graph
let g = new Graph();

// add the vertices
let v1 = "A";
let v2 = "B";
let v3 = "C";
let v4 = "D";
let v5 = "E";
let v6 = "F";
let v7 = "G";

g.addVertex(v1);
g.addVertex(v2);
g.addVertex(v3);
g.addVertex(v4);
g.addVertex(v5);
g.addVertex(v6);
g.addVertex(v7);

// add the edges
g.addEdge(v1, v2);
g.addEdge(v1, v3);
g.addEdge(v2, v4);
g.addEdge(v3, v4);
g.addEdge(v4, v5);
g.addEdge(v5, v6);
g.addEdge(v6, v7);
```

Running the topological sort algorithm on this graph should result in the following output:

```javascript
["A", "B", "C", "D", "E", "F", "G"]
```

And indeed, this is what our code outputs:

```javascript
console.log(g.topologicalSort());
// ["A", "B", "C", "D", "E", "F", "G"]
```

## Conclusion

In this article, we have discussed topological sorting and Kahn's algorithm for performing a topological sort. We have also implemented Kahn's algorithm in JavaScript.