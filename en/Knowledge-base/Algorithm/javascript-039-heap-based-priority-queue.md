---
title: [JavaScript] 039: Heap-Based Priority Queue
description: 
published: true
date: 2023-02-10T17:32:57.312Z
tags: 
editor: markdown
dateCreated: 2023-02-10T17:32:50.671Z
---

- [[JavaScript] 039: cola de prioridad basada en almacenamiento dinámico***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-039-heap-based-priority-queue)
{.links-list}
- [[JavaScript] 039：基于堆的优先级队列***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-039-heap-based-priority-queue)
{.links-list}
- [[JavaScript] 039: 힙 기반 우선순위 큐***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-039-heap-based-priority-queue)
{.links-list}


# JavaScript 039: Heap-Based Priority Queue

A priority queue is a data structure that allows you to store elements with associated priorities. The element with the highest priority is always removed first.

There are many ways to implement a priority queue. In this post, we will discuss one way: using a heap.

## What is a Heap?

A heap is a tree-like data structure in which each node has a priority. The root node is always the node with the highest priority.

![Heap Example](https://upload.wikimedia.org/wikipedia/commons/thumb/3/38/Max-Heap.svg/280px-Max-Heap.svg.png)

There are two types of heaps: max heaps and min heaps. In a max heap, the root node is always the node with the maximum priority. In a min heap, the root node is always the node with the minimum priority.

## Implementation

We can implement a priority queue using a max heap. To do this, we will use an array to store the heap. The root node will be at index 0, the left child of the root node will be at index 1, the right child of the root node will be at index 2, and so on.

Here is a simple implementation of a max heap:

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

## Complexity

Inserting an element into a heap has a complexity of **O(log n)**. Removing an element from a heap has a complexity of **O(log n)**.

## Exercises

1. Implement a min heap using the same technique as the max heap.

2. Use a heap to implement a priority queue.

## Answers

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