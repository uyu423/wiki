---
title: [JavaScript] 040：二叉堆
description: 
published: true
date: 2023-02-10T18:32:41.254Z
tags: 
editor: markdown
dateCreated: 2023-02-10T18:32:34.935Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 040: Binary Heap***English** document is available*](/en/Knowledge-base/Algorithm/javascript-040-binary-heap)
{.links-list}


# 二叉堆

二叉堆是一种采用二叉树形式的堆数据结构。二叉堆是一种特殊类型的二叉树，其中根节点大于或等于其任一子节点，并且每个节点最多是两个子节点的父节点。二叉堆通常用于实现优先级队列。

有两种类型的二叉堆：最小堆和最大堆。在最小堆中，根节点始终是堆中的最小元素。在最大堆中，根节点始终是堆中最大的元素。

## 代码示例

这是 JavaScript 中最小堆的简单实现。

```javascript
class BinaryHeap {
  constructor() {
    this.heap = [];
  }

  // Returns the index of the left child of the node at the given index.
  getLeftChildIndex(parentIndex) {
    return 2 * parentIndex + 1;
  }

  // Returns the index of the right child of the node at the given index.
  getRightChildIndex(parentIndex) {
    return 2 * parentIndex + 2;
  }

  // Returns the index of the parent of the node at the given index.
  getParentIndex(childIndex) {
    return Math.floor((childIndex - 1) / 2);
  }

  // Returns true if the node at the given index has a left child.
  hasLeftChild(index) {
    return this.getLeftChildIndex(index) < this.heap.length;
  }

  // Returns true if the node at the given index has a right child.
  hasRightChild(index) {
    return this.getRightChildIndex(index) < this.heap.length;
  }

  // Returns true if the node at the given index is the root node.
  isRoot(index) {
    return index === 0;
  }

  // Swaps the elements at the given indices in the heap.
  swap(index1, index2) {
    const temp = this.heap[index1];
    this.heap[index1] = this.heap[index2];
    this.heap[index2] = temp;
  }

  // Peek at the root element.
  peek() {
    if (this.heap.length === 0) {
      throw new Error('Heap is empty');
    }

    return this.heap[0];
  }

  // Add an element to the heap.
  add(element) {
    this.heap.push(element);
    this.heapifyUp();
  }

  // Remove and return the root element.
  remove() {
    if (this.heap.length === 0) {
      throw new Error('Heap is empty');
    }

    const element = this.heap[0];
    this.heap[0] = this.heap[this.heap.length - 1];
    this.heap.pop();
    this.heapifyDown();
    return element;
  }

  // Heapify up.
  heapifyUp() {
    let index = this.heap.length - 1;

    while (!this.isRoot(index) && this.heap[index] < this.heap[this.getParentIndex(index)]) {
      this.swap(index, this.getParentIndex(index));
      index = this.getParentIndex(index);
    }
  }

  // Heapify down.
  heapifyDown() {
    let index = 0;

    while (this.hasLeftChild(index)) {
      let smallerChildIndex = this.getLeftChildIndex(index);

      if (this.hasRightChild(index) && this.heap[this.getRightChildIndex(index)] < this.heap[smallerChildIndex]) {
        smallerChildIndex = this.getRightChildIndex(index);
      }

      if (this.heap[index] < this.heap[smallerChildIndex]) {
        break;
      } else {
        this.swap(index, smallerChildIndex);
      }

      index = smallerChildIndex;
    }
  }
}
```

## 练习

1. 实现最大堆。

2.使用二叉堆实现优先队列。