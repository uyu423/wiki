---
title: [JavaScript] 041：斐波那契堆
description: 
published: true
date: 2023-02-10T19:32:29.761Z
tags: 
editor: markdown
dateCreated: 2023-02-10T19:32:28.109Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 041: Fibonacci Heap***English** document is available*](/en/Knowledge-base/Algorithm/javascript-041-fibonacci-heap)
{.links-list}


# 斐波那契堆

在计算机科学中，斐波那契堆是一种用于优先队列操作的数据结构，由堆有序树的集合组成。它比许多其他优先级队列数据结构（包括二叉堆和二项式堆）具有更好的摊销运行时间。 Michael L. Fredman 和 Robert E. Tarjan 于 1984 年开发了斐波那契堆，并于 1987 年在科学期刊上发表了它们。

斐波那契堆是最小堆有序树的集合。每个节点都有一个关联的值，称为键。最小堆属性如下：节点的值至少是其子节点的值。也就是说，堆的根具有最小键。

Fibonacci 堆数据结构支持两种操作：insert 和 extract-min。这两个操作的最坏情况时间复杂度为 O(log n)。

## 代码示例

### 插入

为了向 Fibonacci 堆中插入一个新键，我们只需使用该键创建一个新节点并将其插入到根列表中。这个新节点相对于根列表中的其他节点自动按堆排序，因此无需执行任何进一步的堆操作。

```javascript
function insert(key) {
    // create a new node with the given key
    var node = new Node(key);
    
    // insert the new node into the root list
    if (this.root == null) {
        this.root = node;
    } else {
        node.next = this.root;
        this.root.prev = node;
        this.root = node;
    }
    
    // update the size of the heap
    this.size++;
}
```

### 提取分钟

为了从 Fibonacci 堆中提取最小键，我们只需从根列表中删除最小节点并将其返回。由于根列表现在可能为空，我们需要找到新的最小节点并将其作为根。我们还需要通过成对链接相同度数的树来合并堆。

```javascript
function extractMin() {
    // if the heap is empty, return null
    if (this.root == null) {
        return null;
    }
    
    // remove the minimum node from the root list
    var minNode = this.root;
    if (this.root.next == this.root) {
        this.root = null;
    } else {
        this.root.prev.next = this.root.next;
        this.root.next.prev = this.root.prev;
        this.root = this.root.next;
    }
    
    // update the size of the heap
    this.size--;
    
    // if the heap is now empty, return the minimum node
    if (this.root == null) {
        return minNode;
    }
    
    // create a new array for the root list
    var roots = [];
    
    // find the new minimum node and add the other nodes to the array
    var current = this.root;
    do {
        roots.push(current);
        current = current.next;
    } while (current != this.root);
    
    // consolidate the heap by pairwise-linking the trees of the same degree
    this.consolidate(roots);
    
    // return the minimum node
    return minNode;
}
```

## 练习

1. 用你喜欢的编程语言实现斐波那契堆数据结构。

2.使用斐波那契堆数据结构实现优先队列。

3. 使用斐波那契堆数据结构解决图中的最短路径问题。