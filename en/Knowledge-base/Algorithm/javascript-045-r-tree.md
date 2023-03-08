---
title: [JavaScript] 045: R-Tree
description: 
published: true
date: 2023-02-10T23:32:29.304Z
tags: 
editor: markdown
dateCreated: 2023-02-10T23:32:27.557Z
---

- [[JavaScript] 045: R-Árbol***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-045-r-tree)
{.links-list}
- [[JavaScript] 045：R 树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-045-r-tree)
{.links-list}
- [[JavaScript] 045: R-트리***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-045-r-tree)
{.links-list}


# R-Tree

R-Tree is a data structure that is used for storing spatial data, such as points, rectangles, and polygons. It is a type of space-partitioning tree in which each node represents a rectangular area. The tree is designed in such a way that all of the rectangles in a given node are contained within that node's rectangle. 

R-Trees are often used in geographic information systems (GIS), computer-aided design (CAD), and image processing.

## How it works

The basic idea behind an R-Tree is to divide a 2-dimensional space into a set of non-overlapping rectangles. Each rectangle is associated with an object, such as a point, a line, or a polygon. The rectangles are then organized into a tree structure, with the root node representing the entire 2-dimensional space. The child nodes of the root node represent smaller rectangles within the space, and so on. 

![RTree](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree.png)

The advantage of using an R-Tree is that it can be used to quickly find objects that are close to a given point. For example, if we want to find all of the points within a given radius of a given point, we can simply query the R-Tree for all of the rectangles that intersect with the radius. This is much faster than searching the entire space for points that fall within the radius.

## Insertion

Insertion into an R-Tree is a two-step process. First, we find the leaf node where the new rectangle should be inserted. To do this, we start at the root node and compare the new rectangle to each of the rectangles in the root node. We then select the rectangle that is the closest match to the new rectangle and repeat the process with the child node associated with that rectangle. We continue this process until we reach a leaf node. 

Once we have found the leaf node where the new rectangle should be inserted, we simply add the new rectangle to that node. 

![RTreeInsert](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree-insert.png)

## Deletion

Deletion from an R-Tree is a two-step process. First, we find the leaf node where the rectangle to be deleted is located. To do this, we start at the root node and compare the rectangle to be deleted to each of the rectangles in the root node. We then select the rectangle that is the closest match to the rectangle to be deleted and repeat the process with the child node associated with that rectangle. We continue this process until we reach a leaf node. 

Once we have found the leaf node where the rectangle is located, we simply remove the rectangle from that node. 

![RTreeDelete](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree-delete.png)

## Querying

Querying an R-Tree is a two-step process. First, we find the leaf nodes that intersect with the query rectangle. To do this, we start at the root node and compare the query rectangle to each of the rectangles in the root node. We then select the rectangles that intersect with the query rectangle and repeat the process with the child nodes associated with those rectangles. We continue this process until we reach a leaf node. 

Once we have found the leaf nodes that intersect with the query rectangle, we simply return the objects associated with those rectangles. 

![RTreeQuery](https://github.com/mykeels/45-JavaScript-Data-Structures-Algorithms/blob/master/assets/045-rtree-query.png)

## Implementation

There are many ways to implement an R-Tree. One popular method is to use a quadtree, which is a type of space-partitioning tree in which each node has up to four child nodes. 

Another popular method is to use a k-d tree, which is a type of space-partitioning tree in which each node has up to two child nodes. 

## Conclusion

R-Trees are a powerful data structure for storing and querying spatial data. They are efficient and easy to implement.