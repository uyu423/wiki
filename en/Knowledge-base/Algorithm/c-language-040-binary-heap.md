---
title: [C Language] 040: Binary Heap
description: 
published: true
date: 2023-02-13T20:32:24.176Z
tags: 
editor: markdown
dateCreated: 2023-02-13T20:32:17.156Z
---

- [[Lenguaje C] 040: montón binario***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-040-binary-heap)
{.links-list}
- [[C语言]040：二叉堆***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-040-binary-heap)
{.links-list}
- [[C언어] 040: 바이너리 힙***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-040-binary-heap)
{.links-list}


# 040: Binary Heap

A binary heap is a heap data structure that takes the form of a binary tree. A binary heap is defined as a binary tree with two special properties:

1. The tree is complete. That is, all levels of the tree are fully filled except possibly the last level, which is filled from left to right.
2. The tree satisfies the heap property. That is, each node is greater than or equal to the value of its children.

A binary heap is often used to implement a priority queue. A priority queue is a data structure that allows you to insert elements with a given priority and retrieve the element with the highest priority.

## Code Examples

### Insertion

To insert an element into a binary heap, we first add the element to the bottom level of the heap. Then, we compare the element to its parent. If the element is greater than its parent, we swap the two elements. We continue to compare the element to its parent and swap until the element is in the correct position.

```c
void insert(int value) {
  // Add the element to the bottom level of the heap.
  heap[size] = value;
  size++;

  // Compare the element to its parent.
  int index = size - 1;
  int parent = (index - 1) / 2;
  while (index > 0 && heap[parent] < heap[index]) {
    // Swap the two elements.
    int temp = heap[parent];
    heap[parent] = heap[index];
    heap[index] = temp;

    // Update the index and parent.
    index = parent;
    parent = (index - 1) / 2;
  }
}
```

### Deletion

To delete an element from a binary heap, we first remove the element from the top of the heap. Then, we replace the element with the last element in the heap. Finally, we compare the element to its children and swap until the element is in the correct position.

```c
void delete(int value) {
  // Remove the element from the top of the heap.
  int index = 0;
  heap[index] = heap[size - 1];
  size--;

  // Compare the element to its children.
  int left = 2 * index + 1;
  int right = 2 * index + 2;
  while (left < size && (heap[index] < heap[left] || heap[index] < heap[right])) {
    // Find the largest child.
    int largest = heap[left];
    int largestIndex = left;
    if (right < size && heap[right] > largest) {
      largest = heap[right];
      largestIndex = right;
    }

    // Swap the element with the largest child.
    int temp = heap[index];
    heap[index] = heap[largestIndex];
    heap[largestIndex] = temp;

    // Update the index and children.
    index = largestIndex;
    left = 2 * index + 1;
    right = 2 * index + 2;
  }
}
```

## Exercises

1. Implement a binary heap in your favorite programming language.
2. Use your binary heap implementation to implement a priority queue.
3. What is the time complexity of insertion and deletion in a binary heap?

## Answers

1. See the code examples for insertion and deletion.
2. The time complexity of insertion and deletion is O(log n).