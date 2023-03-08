---
title: [JavaScript] 023：图形表示
description: 
published: true
date: 2023-02-10T01:32:29.859Z
tags: 
editor: markdown
dateCreated: 2023-02-10T01:32:28.216Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 023: Graph Representation***English** document is available*](/en/Knowledge-base/Algorithm/javascript-023-graph-representation)
{.links-list}


# 图表示

图可以用多种方式表示，但主要有两种方式：邻接表和邻接矩阵。在本文中，我们将研究这两种方法并了解它们的优缺点。

## 邻接表

邻接表只是与给定顶点相邻的所有顶点的列表。例如，考虑下图：

![替代文字](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/adjacency_list_1.png)

该图的邻接表为：

```
A: B, C
B: A, C, D
C: A, B, D
D: B, C
```

如您所见，列出了每个顶点及其相邻的所有顶点。

邻接表的优点是简单易行。它们也比邻接矩阵使用更少的空间，因为我们只需要存储每个顶点的边，而不是整个图的所有边。

邻接表的缺点是查询速度较慢。例如，如果我们想知道顶点 A 和 D 之间是否有边，我们需要查看 A 和 D 的邻接表以查看它们是否列出了另一个。相反，对于邻接矩阵，我们可以只查看 A 和 D 的条目，看看它是否非零。

## 邻接矩阵

邻接矩阵是一个矩阵（二维数组），其中每一行和每一列代表一个顶点，每一行/列交点处的值是这两个顶点之间边的权重。例如，考虑下图：

![替代文字](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/adjacency_matrix_1.png)

该图的邻接矩阵为：

```
  A B C D
A 0 1 1 0
B 1 0 1 1
C 1 1 0 1
D 0 1 1 0
```

如您所见，每行和每列代表一个顶点，每个行/列交点处的值是这两个顶点之间的边的权重。如果两个顶点之间没有边，则权重为 0。

邻接矩阵的优点是查询速度非常快。例如，如果我们想知道顶点 A 和 D 之间是否有边，我们可以只查看 A 和 D 的条目，看看它是否非零。相比之下，对于邻接表，我们需要查看 A 和 D 的邻接表，看看它们中的任何一个是否列出了另一个。

邻接矩阵的缺点是它们可以使用比邻接列表更多的空间。例如，在我们上面的图中，只有 16 条边，但邻接矩阵有 16 * 4 = 64 个条目。通常，邻接矩阵将使用 O(V^2) 空间，其中 V 是顶点数。

## 我应该使用哪个？

当图形稀疏时通常使用邻接列表，这意味着没有很多边。邻接矩阵通常在图形密集时使用，这意味着有很多边。

没有正确或错误的答案，通常可以使用任何一种表示。一般来说，邻接表更容易实现，但邻接矩阵查询起来更快。