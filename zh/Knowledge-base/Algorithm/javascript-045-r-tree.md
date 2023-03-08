---
title: [JavaScript] 045：R 树
description: 
published: true
date: 2023-02-10T23:32:34.256Z
tags: 
editor: markdown
dateCreated: 2023-02-10T23:32:27.553Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 045: R-Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-045-r-tree)
{.links-list}


# R-树

R-Tree 是一种数据结构，用于存储空间数据，例如点、矩形和多边形。它是一种空间划分树，其中每个节点代表一个矩形区域。树的设计方式是给定节点中的所有矩形都包含在该节点的矩形内。

R 树通常用于地理信息系统 (GIS)、计算机辅助设计 (CAD) 和图像处理。

## 怎么运行的

R-Tree 背后的基本思想是将二维空间划分为一组不重叠的矩形。每个矩形都与一个对象相关联，例如点、线或多边形。然后将矩形组织成树结构，根节点代表整个二维空间。根节点的子节点表示空间内较小的矩形，依此类推。

![RTree](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree.png)

使用 R-Tree 的好处是它可以用来快速找到靠近给定点的对象。例如，如果我们想找到给定点的给定半径内的所有点，我们可以简单地查询 R-Tree 以查找与该半径相交的所有矩形。这比在整个空间中搜索落在半径内的点要快得多。

## 插入

插入 R-Tree 是一个两步过程。首先，我们找到应该插入新矩形的叶节点。为此，我们从根节点开始，将新矩形与根节点中的每个矩形进行比较。然后，我们选择与新矩形最匹配的矩形，并对与该矩形关联的子节点重复该过程。我们继续这个过程，直到我们到达叶节点。

一旦找到应该插入新矩形的叶节点，我们只需将新矩形添加到该节点即可。

![RTreeInsert](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree-insert.png)

## 删除

从 R-Tree 中删除是一个两步过程。首先，我们找到要删除的矩形所在的叶子节点。为此，我们从根节点开始，将要删除的矩形与根节点中的每个矩形进行比较。然后我们选择与要删除的矩形最匹配的矩形，并对与该矩形关联的子节点重复该过程。我们继续这个过程，直到我们到达叶节点。

一旦我们找到矩形所在的叶节点，我们只需从该节点删除矩形。

![RTreeDelete](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree-delete.png)

## 查询

查询 R-Tree 是一个两步过程。首先，我们找到与查询矩形相交的叶节点。为此，我们从根节点开始，将查询矩形与根节点中的每个矩形进行比较。然后我们选择与查询矩形相交的矩形，并对与这些矩形关联的子节点重复该过程。我们继续这个过程，直到我们到达叶节点。

一旦找到与查询矩形相交的叶节点，我们只需返回与这些矩形关联的对象。

![RTreeQuery](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree-query.png)

## 执行

有很多方法可以实现 R-Tree。一种流行的方法是使用四叉树，这是一种空间分区树，其中每个节点最多有四个子节点。

另一种流行的方法是使用 k-d 树，这是一种空间分区树，其中每个节点最多有两个子节点。

## 结论

R 树是一种用于存储和查询空间数据的强大数据结构。它们高效且易于实施。