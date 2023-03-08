---
title: [JavaScript] 014：优先队列
description: 
published: true
date: 2023-02-09T16:32:46.529Z
tags: 
editor: markdown
dateCreated: 2023-02-09T16:32:40.306Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 014: Priority Queue***English** document is available*](/en/Knowledge-base/Algorithm/javascript-014-priority-queue)
{.links-list}


# 优先队列

优先级队列是一种数据结构，其中每个元素都有一个与之关联的“优先级”。具有较高优先级的元素在具有较低优先级的元素之前被处理。

在优先级队列中，具有最高优先级的元素总是在队列的前面。当元素具有相同的优先级时，它们将按照它们被添加到队列中的顺序进行处理。

## 执行

有很多方法可以实现优先级队列。一种方法是使用数组。

```javascript
function PriorityQueue() {
  this.items = [];
}

PriorityQueue.prototype.enqueue = function(item, priority) {
  this.items.push({item: item, priority: priority});
};

PriorityQueue.prototype.dequeue = function() {
  return this.items.shift();
};

PriorityQueue.prototype.isEmpty = function() {
  return this.items.length === 0;
};
```

实现优先级队列的另一种方法是使用最小堆。最小堆是二叉树，其中根节点是优先级最低的元素。父节点的左右子节点是优先级高于父节点的元素。

```javascript
function Heap() {
  this.items = [];
}

Heap.prototype.enqueue = function(item, priority) {
  this.items.push({item: item, priority: priority});
  this.heapifyUp();
};

Heap.prototype.dequeue = function() {
  var item = this.items[0];
  this.items[0] = this.items[this.items.length - 1];
  this.items.pop();
  this.heapifyDown();
  return item;
};

Heap.prototype.heapifyUp = function() {
  var index = this.items.length - 1;
  var parentIndex = Math.floor((index - 1) / 2);
  var item = this.items[index];
  while(index > 0 && this.items[parentIndex].priority > item.priority) {
    this.items[index] = this.items[parentIndex];
    index = parentIndex;
    parentIndex = Math.floor((index - 1) / 2);
  }
  this.items[index] = item;
};

Heap.prototype.heapifyDown = function() {
  var index = 0;
  var leftChildIndex = 2 * index + 1;
  var rightChildIndex = 2 * index + 2;
  var item = this.items[index];
  while(leftChildIndex < this.items.length) {
    var minIndex = index;
    if(this.items[leftChildIndex].priority < item.priority) {
      minIndex = leftChildIndex;
    }
    if(rightChildIndex < this.items.length && this.items[rightChildIndex].priority < this.items[minIndex].priority) {
      minIndex = rightChildIndex;
    }
    if(minIndex !== index) {
      this.items[index] = this.items[minIndex];
      index = minIndex;
      leftChildIndex = 2 * index + 1;
      rightChildIndex = 2 * index + 2;
    } else {
      break;
    }
  }
  this.items[index] = item;
};

Heap.prototype.isEmpty = function() {
  return this.items.length === 0;
};
```

## 用法

优先队列可用于多种目的。一个常见的用途是调度。例如，优先级队列可用于安排计算机执行的任务。

可以安排更重要的任务（例如具有更高优先级的任务）比不太重要的任务（例如具有较低优先级的任务）更快地执行。

优先级队列的另一个常见用途是在需要处理“接近”某个目标的数据的算法中。例如，A* 寻路算法使用优先级队列来寻找从起始节点到目标节点的最短路径。

## 锻炼

1.使用数组实现优先级队列。

2. 使用最小堆实现优先级队列。

3. 使用优先级队列来安排计算机执行的任务。

4. 使用优先级队列寻找图中的最短路径。