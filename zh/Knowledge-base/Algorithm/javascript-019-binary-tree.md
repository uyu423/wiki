---
title: [JavaScript] 019：二叉树
description: 
published: true
date: 2023-02-09T21:32:36.263Z
tags: 
editor: markdown
dateCreated: 2023-02-09T21:32:34.692Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 019: Binary Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-019-binary-tree)
{.links-list}


# 二叉树

在计算机科学中，二叉树是一种树状数据结构，其中每个节点最多有两个孩子，称为左孩子和右孩子。

二叉树是一种允许两种操作的结构：

- 寻找树中的最大元素。
- 寻找树中的最小元素。

这两个操作的时间复杂度都是 O(log n)，其中 n 是树中的节点数。

二叉树用于实现二叉搜索树和堆。

## 代码示例

下面是 JavaScript 中的二叉树示例：

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

## 寻找最大元素

要找到二叉树中的最大元素，我们可以使用递归算法。

这个想法是将根节点与其左右子节点进行比较。如果根节点大于它的两个子节点，那么它就是最大元素。否则，最大元素将是两个子节点中较大的一个。

然后我们可以递归地在左右子节点上调用相同的算法。

下面是该算法的伪代码：

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

## 寻找最小元素

要找到二叉树中的最小元素，我们可以使用递归算法。

这个想法是将根节点与其左右子节点进行比较。如果根节点小于它的两个子节点，那么它就是最小元素。否则，最小元素将是两个子节点中较小的一个。

然后我们可以递归地在左右子节点上调用相同的算法。

下面是该算法的伪代码：

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

## 相关练习

- [二叉树的最大深度](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- [二叉树的最小深度](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
- [对称树](https://leetcode.com/problems/symmetric-tree/)
- [二叉树中序遍历](https://leetcode.com/problems/binary-tree-inorder-traversal/)
- [二叉树后序遍历](https://leetcode.com/problems/binary-tree-postorder-traversal/)
- [二叉树前序遍历](https://leetcode.com/problems/binary-tree-preorder-traversal/)