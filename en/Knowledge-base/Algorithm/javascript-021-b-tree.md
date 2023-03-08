---
title: [JavaScript] 021: B-Tree
description: 
published: true
date: 2023-02-09T23:32:57.348Z
tags: 
editor: markdown
dateCreated: 2023-02-09T23:32:51.279Z
---

- [[JavaScript] 021: Árbol B***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-021-b-tree)
{.links-list}
- [[JavaScript] 021：B 树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-021-b-tree)
{.links-list}
- [[JavaScript] 021: B-트리***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-021-b-tree)
{.links-list}


# JavaScript 021: B-Tree

A B-tree is a self-balancing tree data structure that maintains sorted data and allows searches, insertions, and deletions in logarithmic time. The B-tree is a generalization of a binary search tree in that a node can have more than two children.

## Concept

A B-tree is a tree data structure that keeps data sorted and allows for searches, insertions, and deletions in logarithmic time. A B-tree is a generalization of a binary search tree in that a node can have more than two children. The advantage of a B-tree over a binary search tree is that it requires less disk accesses for operations such as insertion and deletion.

A B-tree of order m is a tree in which each node has at most m children. The root node has at least two children. A B-tree is balanced if the difference in the number of children of any two nodes is at most 1.

The height of a B-tree is the number of levels in the tree. The height of a tree is the length of the longest path from the root to a leaf.

A B-tree of order m can have a height of at most m.

## Code Examples

Here is a simple implementation of a B-tree in JavaScript.

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

## Exercises

1. Implement the delete operation for a B-tree.

2. Implement the range search operation for a B-tree. Range search should take two keys, a lower bound and an upper bound, and return all keys in the tree that are between the two bounds.

## Answers

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