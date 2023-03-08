---
title: [JavaScript] 039：基于堆的优先级队列
description: 
published: true
date: 2023-02-10T17:32:52.264Z
tags: 
editor: markdown
dateCreated: 2023-02-10T17:32:50.663Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 039: Heap-Based Priority Queue***English** document is available*](/en/Knowledge-base/Algorithm/javascript-039-heap-based-priority-queue)
{.links-list}


# JavaScript 039：基于堆的优先级队列

优先级队列是一种数据结构，允许您存储具有关联优先级的元素。具有最高优先级的元素总是首先被删除。

有很多方法可以实现优先级队列。在这篇文章中，我们将讨论一种方法：使用堆。

## 什么是堆？

堆是一种树状数据结构，其中每个节点都有一个优先级。根节点始终是具有最高优先级的节点。

![堆示例](https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Max-Heap.svg/280px-Max-Heap.svg.png)

有两种类型的堆：最大堆和最小堆。在最大堆中，根节点始终是具有最大优先级的节点。在最小堆中，根节点始终是具有最小优先级的节点。

## 执行

我们可以使用最大堆实现优先级队列。为此，我们将使用一个数组来存储堆。根节点将在索引 0 处，根节点的左子节点将在索引 1 处，根节点的右子节点将在索引 2 处，依此类推。

这是最大堆的简单实现：

```javascript
class MaxHeap {
  constructor() {
    this.heap = [];
  }

  insert(element) {
    // Add the new element to the end of the array
    this.heap.push(element);

    // Find the index of the new element
    let index = this.heap.length - 1;

    // Get the parent index
    let parentIndex = Math.floor((index - 1) / 2);

    // Keep swapping the element with its parent until it is at the correct position
    while (index > 0 && this.heap[parentIndex] < this.heap[index]) {
      // Swap the element with its parent
      let temp = this.heap[parentIndex];
      this.heap[parentIndex] = this.heap[index];
      this.heap[index] = temp;

      // Update the index and parentIndex variables
      index = parentIndex;
      parentIndex = Math.floor((index - 1) / 2);
    }
  }

  remove() {
    // If the heap is empty, return undefined
    if (this.heap.length === 0) return undefined;

    // Remove the root element from the heap
    let removed = this.heap.shift();

    // If there are no more elements in the heap, return the removed element
    if (this.heap.length === 0) return removed;

    // Add the last element in the heap to the root position
    this.heap.unshift(this.heap.pop());

    // Get the index of the new root element
    let index = 0;

    // Get the indices of the child elements
    let leftChildIndex = 2 * index + 1;
    let rightChildIndex = 2 * index + 2;

    // Keep swapping the element with its children until it is at the correct position
    while (
      (leftChildIndex < this.heap.length && this.heap[index] < this.heap[leftChildIndex]) ||
      (rightChildIndex < this.heap.length && this.heap[index] < this.heap[rightChildIndex])
    ) {
      // If the left child is larger than the right child, swap with the left child
      if (
        rightChildIndex >= this.heap.length ||
        this.heap[leftChildIndex] > this.heap[rightChildIndex]
      ) {
        // Swap the element with its left child
        let temp = this.heap[leftChildIndex];
        this.heap[leftChildIndex] = this.heap[index];
        this.heap[index] = temp;

        // Update the index and childIndex variables
        index = leftChildIndex;
        leftChildIndex = 2 * index + 1;
        rightChildIndex = 2 * index + 2;
      }
      // Otherwise, swap with the right child
      else {
        // Swap the element with its right child
        let temp = this.heap[rightChildIndex];
        this.heap[rightChildIndex] = this.heap[index];
        this.heap[index] = temp;

        // Update the index and childIndex variables
        index = rightChildIndex;
        leftChildIndex = 2 * index + 1;
        rightChildIndex = 2 * index + 2;
      }
    }

    // Return the removed element
    return removed;
  }
}

let heap = new MaxHeap();
heap.insert(10);
heap.insert(5);
heap.insert(3);
heap.insert(4);
heap.insert(1);
console.log(heap.remove()); // 10
console.log(heap.remove()); // 5
console.log(heap.remove()); // 4
console.log(heap.remove()); // 3
console.log(heap.remove()); // 1
console.log(heap.remove()); // undefined
```

## 复杂性

向堆中插入一个元素的复杂度为 **O(log n)**。从堆中移除一个元素的复杂度为 **O(log n)**。

## 练习

1. 使用与最大堆相同的技术实现最小堆。

2、用堆实现优先队列。

## 答案

1.

```javascript
class MinHeap {
  constructor() {
    this.heap = [];
  }

  insert(element) {
    // Add the new element to the end of the array
    this.heap.push(element);

    // Find the index of the new element
    let index = this.heap.length - 1;

    // Get the parent index
    let parentIndex = Math.floor((index - 1) / 2);

    // Keep swapping the element with its parent until it is at the correct position
    while (index > 0 && this.heap[parentIndex] > this.heap[index]) {
      // Swap the element with its parent
      let temp = this.heap[parentIndex];
      this.heap[parentIndex] = this.heap[index];
      this.heap[index] = temp;

      // Update the index and parentIndex variables
      index = parentIndex;
      parentIndex = Math.floor((index - 1) / 2);
    }
  }

  remove() {
    // If the heap is empty, return undefined
    if (this.heap.length === 0) return undefined;

    // Remove the root element from the heap
    let removed = this.heap.shift();

    // If there are no more elements in the heap, return the removed element
    if (this.heap.length === 0) return removed;

    // Add the last element in the heap to the root position
    this.heap.unshift(this.heap.pop());

    // Get the index of the new root element
    let index = 0;

    // Get the indices of the child elements
    let leftChildIndex = 2 * index + 1;
    let rightChildIndex = 2 * index + 2;

    // Keep swapping the element with its children until it is at the correct position
    while (
      (leftChildIndex < this.heap.length && this.heap[index] > this.heap[leftChildIndex]) ||
      (rightChildIndex < this.heap.length && this.heap[index] > this.heap[rightChildIndex])
    ) {
      // If the left child is smaller than the right child, swap with the left child
      if (
        rightChildIndex >= this.heap.length ||
        this.heap[leftChildIndex] < this.heap[rightChildIndex]
      ) {
        // Swap the element with its left child
        let temp = this.heap[leftChildIndex];
        this.heap[leftChildIndex] = this.heap[index];
        this.heap[index] = temp;

        // Update the index and childIndex variables
        index = leftChildIndex;
        leftChildIndex = 2 * index + 1;
        rightChildIndex = 2 * index + 2;
      }
      // Otherwise, swap with the right child
      else {
        // Swap the element with its right child
        let temp = this.heap[rightChildIndex];
        this.heap[rightChildIndex] = this.heap[index];
        this.heap[index] = temp;

        // Update the index and childIndex variables
        index = rightChildIndex;
        leftChildIndex = 2 * index + 1;
        rightChildIndex = 2 * index + 2;
      }
    }

    // Return the removed element
    return removed;
  }
}

let heap = new MinHeap();
heap.insert(10);
heap.insert(5);
heap.insert(3);
heap.insert(4);
heap.insert(1);
console.log(heap.remove()); // 1
console.log(heap.remove()); // 3
console.log(heap.remove()); // 4
console.log(heap.remove()); // 5
console.log(heap.remove()); // 10
console.log(heap.remove()); // undefined
```

2.

```javascript
class PriorityQueue {
  constructor() {
    this.heap = new MaxHeap();
  }

  insert(element, priority) {
    let node = new Node(element, priority);
    this.heap.insert(node);
  }

  remove() {
    return this.heap.remove().element;
  }
}

class Node {
  constructor(element, priority) {
    this.element = element;
    this.priority = priority;
  }
}

let queue = new PriorityQueue();
queue.insert("A", 1);
queue.insert("B", 2);
queue.insert("C", 3);
queue.insert("D", 4);
queue.insert("E", 5);
console.log(queue.remove()); // E
console.log(queue.remove()); // D
console.log(queue.remove()); // C
console.log(queue.remove()); // B
console.log(queue.remove()); // A
console.log(queue.remove()); // undefined
```