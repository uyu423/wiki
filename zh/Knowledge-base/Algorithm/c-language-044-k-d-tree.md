---
title: 【C语言】044：K-D树
description: 
published: true
date: 2023-02-13T22:32:20.188Z
tags: 
editor: markdown
dateCreated: 2023-02-13T22:32:18.231Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 044: K-D Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-044-k-d-tree)
{.links-list}


# 044：K-D树

k-d 树（k 维树的简称）是一种空间划分数据结构，用于在 k 维空间中组织点。 k-d 树是一种适用于多种应用的有用数据结构，例如涉及多维搜索关键字的搜索（例如范围搜索和最近邻搜索）。

k-d树是一种二叉树，其中每个节点都是一个k维点。该树以自上而下的方式递归构建，方法是沿着通过具有最大方差的点的超平面将点分成两组。这个过程在每个集合上递归重复，直到达到所需的粒度级别。

## 概念

k-d树是二叉搜索树数据结构的推广。在二叉搜索树中，点沿单个维度（例如 x 轴）进行分区，从而形成二维空间。在 k-d 树中，点沿多个维度进行划分，从而形成 k 维空间。

k-d 树中点的划分以自上而下的方式递归完成。通过从包含所有点的根节点开始构建树。然后根节点沿具有最大方差的维度进行划分，并将点分为两组：一组包含小于轴心点的所有点，另一组包含所有大于轴心点的点大于或等于枢轴点。

然后在两个集合中的每一个上递归地重复这个过程，直到达到所需的粒度级别。

## 代码示例

这是一个如何用伪代码构造 k-d 树的简单示例：

```
function kdtree(points, depth)
   if points is empty
      return

   select a pivot point, p, using some heuristic (e.g. median of points)
   partition points into two sets, S1 and S2, using p as the pivot
   create a new node, n, with p as the key
   n.left = kdtree(S1, depth + 1)
   n.right = kdtree(S2, depth + 1)
   return n
```

## 相关练习

- [ ] 用你最喜欢的编程语言实现一个 k-d 树。
- [ ] 给定一组点，构造一棵 k-d 树并查询给定点的最近邻居。
- [ ] 给定一组点，构建一个 k-d 树并查询给定范围内的所有点。