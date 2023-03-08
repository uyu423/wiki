---
title: [JavaScript] 027：最小生成树
description: 
published: true
date: 2023-02-10T05:33:08.879Z
tags: 
editor: markdown
dateCreated: 2023-02-10T05:33:06.749Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 027: Minimum Spanning Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-027-minimum-spanning-tree)
{.links-list}


# 最小生成树

在计算机科学中，最小生成树 (MST) 或最小权重生成树是无向加权图的边的子集，该图将所有顶点连接在一起，没有任何循环，并且具有最小可能的总边权重。

最小生成树有很多应用。例如，在道路或通信线路网络中，可以使用最小生成树找到将所有节点连接在一起的最便宜的方式。另一个例子是聚类分析，其中最小生成树可用于查找类似对象的组。

## Kruskal 算法

Kruskal 算法是一种贪心算法，它为连通的加权图寻找最小生成树。它从权重最小的边开始，然后添加边，直到到达一棵树。

该算法的工作原理如下：

1.按权重从小到大对边进行排序。

2. 从权重最小的边开始。如果边缘没有创建循环，则将其添加到树中。

3. 重复步骤 2，直到没有更多的边可以添加。

Kruskal 算法的时间复杂度为 O(E log V)，其中 E 为边数，V 为顶点数。

## 普里姆算法

Prim 算法是一种贪心算法，它为连通的加权图寻找最小生成树。它从一个顶点开始，添加最便宜的边，直到它到达一棵树。

该算法的工作原理如下：

1. 从一个顶点开始。

2. 找到从一个顶点到另一个顶点的最便宜的边。

3. 将边添加到树中。

4. 重复步骤 2，直到没有更多的边可以添加。

Prim 算法的时间复杂度为 O(E log V)，其中 E 为边数，V 为顶点数。

## 代码示例

以下是 Kruskal 算法的 JavaScript 实现。

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

## 锻炼

1. 使用 Kruskal 算法求下图的最小生成树：

    ![](https://i.imgur.com/lVqnqj7.png)

2. 使用 Prim 算法求下图的最小生成树：

    ![](https://i.imgur.com/kzFcNcu.png)

## 答案

1.图的最小生成树如下图所示。树的总重量为 9。

    ![](https://i.imgur.com/zM0FtqD.png)

2. 图的最小生成树如下所示。树的总重量为 10。

    ![](https://i.imgur.com/kzFcNcu.png)