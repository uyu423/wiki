---
title: [JavaScript] 026: 拓扑排序
description: 
published: true
date: 2023-02-10T04:32:33.096Z
tags: 
editor: markdown
dateCreated: 2023-02-10T04:32:31.448Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 026: Topological Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-026-topological-sort)
{.links-list}


# 拓扑排序

在数学中，拓扑排序是有向无环图 (DAG) 中顶点的线性排序。有向图的拓扑排序或拓扑排序是其顶点的线性排序，使得对于从顶点 u 到顶点 v 的每条有向边 uv，u 在排序中排在 v 之前。例如，图的顶点可以表示要执行的任务，而边可以表示这些任务的依赖关系。

拓扑排序有很多应用。一个例子是根据它们的依赖关系安排一系列作业或任务。再举一个例子，假设您要将一组源代码文件编译成一组目标文件。这可以通过将源文件表示为顶点并将它们之间的依赖关系表示为边来实现。拓扑排序然后提供执行编译的顺序。

有许多算法可用于执行拓扑排序。在本文中，我们将讨论一种最流行的算法，称为 Kahn 算法。

## 卡恩算法

Kahn算法是一种拓扑排序算法，最早由Arthur B. Kahn于1962年在论文《大型网络的拓扑排序》中描述，该算法以他的名字命名。

Kahn 算法背后的想法很简单。我们从一组没有传入边的顶点开始，然后将它们从图中删除。然后我们将它们的出边添加到图中。我们重复这个过程，直到不再有没有传入边的顶点。留在图中的顶点然后按拓扑顺序排序。

该算法使用两个队列实现，一个队列用于没有传入边的顶点，一个用于有传入边的顶点。首先处理第一个队列中的顶点，然后处理第二个队列中的顶点。

卡恩算法的伪代码如下：

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

## 执行

我们现在将在 JavaScript 中实现 Kahn 的算法。我们将使用邻接表来表示图。

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

## 测试

我们现在将测试 Kahn 算法的实现。我们将使用下图：

![图表](https://i.imgur.com/L6oC5vF.png)

创建此图的代码如下：

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

在此图上运行拓扑排序算法应产生以下输出：

```javascript
["A", "B", "C", "D", "E", "F", "G"]
```

事实上，这就是我们的代码输出：

```javascript
console.log(g.topologicalSort());
// ["A", "B", "C", "D", "E", "F", "G"]
```

## 结论

在本文中，我们讨论了拓扑排序和用于执行拓扑排序的 Kahn 算法。我们还在 JavaScript 中实现了 Kahn 的算法。