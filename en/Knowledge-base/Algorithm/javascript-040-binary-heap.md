---
title: [JavaScript] 040: Binary Heap
description: 
published: true
date: 2023-02-10T18:32:36.584Z
tags: 
editor: markdown
dateCreated: 2023-02-10T18:32:34.939Z
---

- [[JavaScript] 040: montón binario***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-040-binary-heap)
{.links-list}
- [[JavaScript] 040：二叉堆***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-040-binary-heap)
{.links-list}
- [[JavaScript] 040: 바이너리 힙***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-040-binary-heap)
{.links-list}


# Binary Heap

A binary heap is a heap data structure that takes the form of a binary tree. Binary heaps are a specific type of binary tree where the root node is greater than or equal to either of its children, and each node is the parent of at most two child nodes. A binary heap is often used to implement a priority queue.

There are two types of binary heaps: min-heaps and max-heaps. In a min-heap, the root node is always the smallest element in the heap. In a max-heap, the root node is always the largest element in the heap.

## Code Example

Here is a simple implementation of a min-heap in JavaScript.

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

## Exercises

1. Implement a max-heap.

2. Use a binary heap to implement a priority queue.