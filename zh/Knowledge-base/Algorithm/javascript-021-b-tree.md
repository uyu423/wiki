---
title: [JavaScript] 021：B 树
description: 
published: true
date: 2023-02-09T23:32:52.880Z
tags: 
editor: markdown
dateCreated: 2023-02-09T23:32:51.275Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 021: B-Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-021-b-tree)
{.links-list}


# JavaScript 021：B 树

B 树是一种自平衡树数据结构，它维护已排序的数据并允许在对数时间内进行搜索、插入和删除。 B 树是二叉搜索树的推广，因为一个节点可以有两个以上的子节点。

## 概念

B 树是一种树状数据结构，它保持数据排序并允许在对数时间内进行搜索、插入和删除。 B 树是二叉搜索树的推广，因为一个节点可以有两个以上的子节点。 B 树相对于二叉搜索树的优势在于它需要更少的磁盘访问来执行插入和删除等操作。

m 阶 B 树是每个节点至多有 m 个子节点的树。根节点至少有两个孩子。如果任意两个节点的孩子数量之差至多为 1，则 B 树是平衡的。

B 树的高度是树中的层数。树的高度是从根到叶子的最长路径的长度。

m 阶 B 树的高度最多为 m。

## 代码示例

下面是 JavaScript 中 B 树的简单实现。

```javascript
class Node {
  constructor(keys, children) {
    this.keys = keys;
    this.children = children;
  }
}

class BTree {
  constructor(order) {
    this.order = order;
    this.root = null;
  }
  
  insert(key) {
    if (this.root === null) {
      this.root = new Node([key], []);
    } else {
      this._insert(key, this.root);
    }
  }
  
  _insert(key, node) {
    if (node.keys.length < this.order - 1) {
      this._insertKey(key, node);
    } else {
      const medianIndex = Math.floor((this.order - 1) / 2);
      const median = node.keys[medianIndex];
      const leftKeys = node.keys.slice(0, medianIndex);
      const rightKeys = node.keys.slice(medianIndex + 1);
      const leftChildren = node.children.slice(0, medianIndex + 1);
      const rightChildren = node.children.slice(medianIndex + 1);
      const newNode = new Node([median], [
        new Node(leftKeys, leftChildren),
        new Node(rightKeys, rightChildren)
      ]);
      if (key < median) {
        this._insert(key, newNode.children[0]);
      } else {
        this._insert(key, newNode.children[1]);
      }
      this.root = newNode;
    }
  }
  
  _insertKey(key, node) {
    let i = 0;
    while (i < node.keys.length && key > node.keys[i]) {
      i++;
    }
    node.keys = [
      ...node.keys.slice(0, i),
      key,
      ...node.keys.slice(i)
    ];
    node.children = [
      ...node.children.slice(0, i + 1),
      new Node([], []),
      ...node.children.slice(i + 1)
    ];
  }
  
  search(key) {
    return this._search(key, this.root);
  }
  
  _search(key, node) {
    if (node === null) {
      return false;
    }
    let i = 0;
    while (i < node.keys.length && key > node.keys[i]) {
      i++;
    }
    if (i < node.keys.length && key === node.keys[i]) {
      return true;
    }
    return this._search(key, node.children[i]);
  }
}
```

## 练习

1. 实现B树的删除操作。

2. 实现B树的范围搜索操作。范围搜索应该采用两个键，一个下限和一个上限，并返回树中位于两个范围之间的所有键。

## 答案

1.

```javascript
class BTree {
  delete(key) {
    if (this.root === null) {
      return;
    }
    this._delete(key, this.root);
  }
  
  _delete(key, node) {
    let i = 0;
    while (i < node.keys.length && key > node.keys[i]) {
      i++;
    }
    if (i < node.keys.length && key === node.keys[i]) {
      if (node.children[i].keys.length >= this.order) {
        const predecessor = this._getPredecessor(node.children[i]);
        node.keys[i] = predecessor;
        this._delete(predecessor, node.children[i]);
      } else if (node.children[i + 1].keys.length >= this.order) {
        const successor = this._getSuccessor(node.children[i + 1]);
        node.keys[i] = successor;
        this._delete(successor, node.children[i + 1]);
      } else {
        this._merge(node, i);
        this._delete(key, node.children[i]);
      }
    } else {
      this._delete(key, node.children[i]);
    }
  }
  
  _getPredecessor(node) {
    let current = node;
    while (current.children.length !== 0) {
      current = current.children[current.children.length - 1];
    }
    return current.keys[current.keys.length - 1];
  }
  
  _getSuccessor(node) {
    let current = node;
    while (current.children.length !== 0) {
      current = current.children[0];
    }
    return current.keys[0];
  }
  
  _merge(node, i) {
    const left = node.children[i];
    const right = node.children[i + 1];
    const key = node.keys[i];
    left.keys = [...left.keys, key, ...right.keys];
    left.children = [...left.children, ...right.children];
    node.keys = node.keys.filter((k, index) => index !== i);
    node.children = node.children.filter((child, index) => index !== i + 1);
  }
}
```

2.

```javascript
class BTree {
  rangeSearch(lowerBound, upperBound) {
    if (this.root === null) {
      return [];
    }
    return this._rangeSearch(lowerBound, upperBound, this.root);
  }
  
  _rangeSearch(lowerBound, upperBound, node) {
    let i = 0;
    while (i < node.keys.length && lowerBound > node.keys[i]) {
      i++;
    }
    let results = [];
    while (i < node.keys.length && upperBound >= node.keys[i]) {
      if (node.children.length === 0) {
        results.push(node.keys[i]);
      } else {
        results = [...results, ...this._rangeSearch(lowerBound, upperBound, node.children[i])];
      }
      i++;
    }
    if (node.children.length > 0) {
      results = [...results, ...this._rangeSearch(lowerBound, upperBound, node.children[i])];
    }
    return results;
  }
}
```