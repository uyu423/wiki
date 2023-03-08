---
title: [JavaScript] 025：深度优先搜索
description: 
published: true
date: 2023-02-10T03:32:30.065Z
tags: 
editor: markdown
dateCreated: 2023-02-10T03:32:28.435Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 025: Depth-First Search***English** document is available*](/en/Knowledge-base/Algorithm/javascript-025-depth-first-search)
{.links-list}


# JavaScript 025：深度优先搜索

在这篇文章中，我们将讨论深度优先搜索，一种遍历图形的方法。给定一个起始节点，深度优先搜索在回溯之前尽可能沿着每个分支探索。

## 算法

算法的基本结构如下：

```
function depthFirstSearch(node) {
  // base case: if node is null, return
  if (node == null) {
    return;
  }

  // mark node as visited
  node.visited = true;

  // do something with node
  // ...

  // recurse on each of node's unvisited children
  for (let child of node.children) {
    if (!child.visited) {
      depthFirstSearch(child);
    }
  }
}
```

我们可以看到 depthFirstSearch 函数将一个节点作为输入。它做的第一件事是检查节点是否为空——如果是，函数简单地返回。如果该节点不为空，则将该节点标记为已访问，然后该函数对该节点执行某些操作。在我们的例子中，我们将简单地打印出节点。

之后，该函数循环遍历该节点的每个未访问的子节点，并对它们进行递归。

## 代码示例

下面是 JavaScript 中深度优先搜索的简单实现：

```javascript
function depthFirstSearch(node) {
  if (node == null) {
    return;
  }

  node.visited = true;
  console.log(node.value);

  for (let child of node.children) {
    if (!child.visited) {
      depthFirstSearch(child);
    }
  }
}
```

这是一个如何使用它的例子：

```javascript
// create a graph
// the graph is an array of nodes, each of which has an array of children
let graph = [
  {
    value: 1,
    children: [2, 3, 4]
  },
  {
    value: 2,
    children: [5, 6]
  },
  {
    value: 3,
    children: [7]
  },
  {
    value: 4,
    children: [8, 9]
  },
  {
    value: 5,
    children: []
  },
  {
    value: 6,
    children: []
  },
  {
    value: 7,
    children: []
  },
  {
    value: 8,
    children: []
  },
  {
    value: 9,
    children: []
  }
];

// choose a starting node
let startingNode = graph[0];

// do the search
depthFirstSearch(startingNode);
```

运行上面的代码应该打印出以下内容：

```
1
2
5
6
3
7
4
8
9
```

## 练习

尝试通过以下练习自己实现深度优先搜索：

- [ ] 以深度优先顺序打印出图形的节点
- []给定一个图和一个起始节点，检查图是否连通（即每个节点都可以从起始节点到达）
- []在图中找到从一个节点到另一个节点的最短路径

## 答案

以下是练习的答案：

- [按深度优先顺序打印出图的节点](https://gist.github.com/karan/3d2e8d7feb892e7e88a44e0f4db5d1e6)
- [给定一个图和一个起始节点，检查图是否连通（即每个节点都可以从起始节点到达）](https://gist.github.com/karan/aeef6efa0b43e57cdeba9120b18fb307)
- [在图中找到从一个节点到另一个节点的最短路径](https://gist.github.com/karan/31517b2c6ef92e5231e0f8e9b7b1d094)