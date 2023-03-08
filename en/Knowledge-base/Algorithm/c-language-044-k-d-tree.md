---
title: [C Language] 044: K-D Tree
description: 
published: true
date: 2023-02-13T22:32:25.468Z
tags: 
editor: markdown
dateCreated: 2023-02-13T22:32:18.235Z
---

- [[Lenguaje C] 044: Árbol K-D***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-044-k-d-tree)
{.links-list}
- [【C语言】044：K-D树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-044-k-d-tree)
{.links-list}
- [[C언어] 044: K-D 트리***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-044-k-d-tree)
{.links-list}


# 044: K-D Tree

A k-d tree (short for k-dimensional tree) is a space-partitioning data structure for organizing points in a k-dimensional space. k-d trees are a useful data structure for several applications, such as searches involving a multidimensional search key (e.g. range searches and nearest neighbor searches).

A k-d tree is a binary tree in which every node is a k-dimensional point. The tree is constructed recursively, in a top-down fashion, by partitioning the points into two sets along a hyperplane that passes through the point with the largest variance. This process is repeated recursively on each set, until the desired level of granularity is reached.

## Concept

The k-d tree is a generalization of the binary search tree data structure. In a binary search tree, the points are partitioned along a single dimension (e.g. the x-axis), which results in a two-dimensional space. In a k-d tree, the points are partitioned along multiple dimensions, which results in a k-dimensional space.

The partitioning of points in a k-d tree is done recursively, in a top-down fashion. The tree is constructed by starting with a root node that contains all of the points. The root node is then partitioned along the dimension with the largest variance, and the points are split into two sets: one set containing all of the points that are less than the pivot point, and the other set containing all of the points that are greater than or equal to the pivot point.

This process is then repeated recursively on each of the two sets, until the desired level of granularity is reached.

## Code Example

Here is a simple example of how to construct a k-d tree in pseudocode:

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

## Related Exercises

- [ ] Implement a k-d tree in your favorite programming language.
- [ ] Given a set of points, construct a k-d tree and query it for the nearest neighbor of a given point.
- [ ] Given a set of points, construct a k-d tree and query it for all points within a given range.