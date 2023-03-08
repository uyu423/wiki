---
title: [JavaScript] 019: Binary Tree
description: 
published: true
date: 2023-02-09T21:32:40.945Z
tags: 
editor: markdown
dateCreated: 2023-02-09T21:32:34.698Z
---

- [[JavaScript] 019: árbol binario***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-019-binary-tree)
{.links-list}
- [[JavaScript] 019：二叉树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-019-binary-tree)
{.links-list}
- [[JavaScript] 019: 이진 트리***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-019-binary-tree)
{.links-list}


# Binary Tree

In computer science, a binary tree is a tree data structure in which each node has at most two children, which are referred to as the left child and the right child.

A binary tree is a structure that allows two operations:

- Finding the maximum element in the tree.
- Finding the minimum element in the tree.

The time complexity of both of these operations is O(log n), where n is the number of nodes in the tree.

Binary trees are used to implement binary search trees and heaps.

## Code Example

Here is an example of a binary tree in JavaScript:

```javascript
var tree = {
  value: 10,
  left: {
    value: 5,
    left: {
      value: 2,
      left: null,
      right: null
    },
    right: {
      value: 7,
      left: null,
      right: null
    }
  },
  right: {
    value: 15,
    left: {
      value: 12,
      left: null,
      right: null
    },
    right: {
      value: 17,
      left: null,
      right: null
    }
  }
};
```

## Finding the Maximum Element

To find the maximum element in a binary tree, we can use a recursive algorithm.

The idea is to compare the root node with its left and right child nodes. If the root node is greater than both of its child nodes, then it is the maximum element. Otherwise, the maximum element will be the greater of the two child nodes.

We can then recursively call the same algorithm on the left and right child nodes.

Here is the pseudocode for the algorithm:

```
function findMax(node) {
  if (node is null) {
    return null;
  }
 
  var max = node.value;
  var leftMax = findMax(node.left);
  var rightMax = findMax(node.right);
 
  if (leftMax > max) {
    max = leftMax;
  }
 
  if (rightMax > max) {
    max = rightMax;
  }
 
  return max;
}
```

## Finding the Minimum Element

To find the minimum element in a binary tree, we can use a recursive algorithm.

The idea is to compare the root node with its left and right child nodes. If the root node is less than both of its child nodes, then it is the minimum element. Otherwise, the minimum element will be the lesser of the two child nodes.

We can then recursively call the same algorithm on the left and right child nodes.

Here is the pseudocode for the algorithm:

```
function findMin(node) {
  if (node is null) {
    return null;
  }
 
  var min = node.value;
  var leftMin = findMin(node.left);
  var rightMin = findMin(node.right);
 
  if (leftMin < min) {
    min = leftMin;
  }
 
  if (rightMin < min) {
    min = rightMin;
  }
 
  return min;
}
```

## Related Exercises

- [Maximum Depth of a Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- [Minimum Depth of a Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
- [Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)
- [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)
- [Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)
- [Binary Tree Preorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)