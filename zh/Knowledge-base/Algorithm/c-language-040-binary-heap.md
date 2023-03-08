---
title: [C语言]040：二叉堆
description: 
published: true
date: 2023-02-13T20:32:18.721Z
tags: 
editor: markdown
dateCreated: 2023-02-13T20:32:17.149Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 040: Binary Heap***English** document is available*](/en/Knowledge-base/Algorithm/c-language-040-binary-heap)
{.links-list}


# 040：二进制堆

二叉堆是一种采用二叉树形式的堆数据结构。二叉堆被定义为具有两个特殊属性的二叉树：

1.树完成了。也就是说，树的所有级别都被完全填充，除了最后一层可能是从左到右填充的。
2.树满足堆性质。也就是说，每个节点都大于或等于其子节点的值。

二叉堆通常用于实现优先级队列。优先级队列是一种数据结构，允许您插入具有给定优先级的元素并检索具有最高优先级的元素。

## 代码示例

### 插入

要将元素插入二叉堆，我们首先将元素添加到堆的底层。然后，我们将元素与其父元素进行比较。如果元素大于它的父元素，我们交换这两个元素。我们继续将元素与其父元素进行比较并交换，直到元素位于正确的位置。

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

### 删除

要从二叉堆中删除一个元素，我们首先从堆顶删除该元素。然后，我们用堆中的最后一个元素替换该元素。最后，我们将元素与其子元素进行比较并交换，直到元素位于正确的位置。

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

## 练习

1. 用你最喜欢的编程语言实现一个二叉堆。
2. 使用您的二叉堆实现来实现优先级队列。
3. 二叉堆中插入和删除的时间复杂度是多少？

## 答案

1、插入和删除见代码示例。
2、插入和删除的时间复杂度为O(log n)。