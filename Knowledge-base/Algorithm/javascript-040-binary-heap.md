---
title: [JavaScript] 040: 바이너리 힙
description: 
published: true
date: 2023-02-10T18:32:41.254Z
tags: 
editor: markdown
dateCreated: 2023-02-10T18:32:34.936Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 040: Binary Heap***English** document is available*](/en/Knowledge-base/Algorithm/javascript-040-binary-heap)
{.links-list}


# 바이너리 힙

이진 힙은 이진 트리 형식을 취하는 힙 데이터 구조입니다. 이진 힙은 루트 노드가 자식 노드보다 크거나 같고 각 노드가 최대 두 자식 노드의 부모인 특정 유형의 이진 트리입니다. 바이너리 힙은 종종 우선 순위 큐를 구현하는 데 사용됩니다.

이진 힙에는 최소 힙과 최대 힙의 두 가지 유형이 있습니다. 최소 힙에서 루트 노드는 항상 힙에서 가장 작은 요소입니다. 최대 힙에서 루트 노드는 항상 힙에서 가장 큰 요소입니다.

## 코드 예

다음은 JavaScript에서 최소 힙을 간단하게 구현한 것입니다.

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

## 운동

1. 최대 힙을 구현합니다.

2. 바이너리 힙을 사용하여 우선 순위 큐를 구현합니다.