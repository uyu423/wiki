---
title: [JavaScript] 044: K-D Tree
description: 
published: true
date: 2023-02-10T22:32:23.387Z
tags: 
editor: markdown
dateCreated: 2023-02-10T22:32:16.871Z
---

- [[JavaScript] 044: Árbol K-D***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-044-k-d-tree)
{.links-list}
- [[JavaScript] 044：K-D 树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-044-k-d-tree)
{.links-list}
- [[JavaScript] 044: K-D 트리***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-044-k-d-tree)
{.links-list}


# JavaScript 044: K-D Tree

A K-D tree (short for k-dimensional tree) is a space-partitioning data structure for organizing points in a k-dimensional space. K-D trees are a useful data structure for several applications, such as searches involving a multidimensional search key (e.g. range searches and nearest neighbor searches).

A K-D tree is a binary tree in which each internal node represents a point in k-dimensional space. The tree is constructed by recursively partitioning the points in the space into two halves along the median value of one of the k dimensions. This process is repeated recursively until all points are contained in leaves of the tree.

## Construction

The K-D tree can be constructed in O(n log n) time, where n is the number of points in the space.

The construction algorithm begins by selecting a dimension (k-dimension) at random. The points are then sorted along this dimension and the median point is chosen as the root of the tree. The points to the left of the median are recursively partitioned into a left subtree and the points to the right of the median are recursively partitioned into a right subtree. This process is repeated until all points are contained in leaves of the tree.

## Search

Given a query point q, the nearest neighbor of q can be found in O(log n) time by traversing the tree. The search begins at the root of the tree and proceeds as follows:

- If q is less than the value at the current node, search the left subtree.
- If q is greater than the value at the current node, search the right subtree.
- If q is equal to the value at the current node, return the node.

The search terminates when a leaf node is reached. At this point, the nearest neighbor of q is the point in the leaf node that is closest to q.

## Applications

K-D trees are commonly used for nearest neighbor search, a type of search that is used to find the point in a space that is closest to a given query point. Nearest neighbor search is often used in applications such as pattern recognition and computer graphics.

K-D trees are also used for range search, a type of search that is used to find all points in a space that are within a given distance of a query point. Range search is often used in applications such as scientific visualization and geographic information systems.