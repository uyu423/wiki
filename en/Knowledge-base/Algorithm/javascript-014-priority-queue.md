---
title: [JavaScript] 014: Priority Queue
description: 
published: true
date: 2023-02-09T16:32:41.930Z
tags: 
editor: markdown
dateCreated: 2023-02-09T16:32:40.309Z
---

- [[JavaScript] 014: cola de prioridad***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-014-priority-queue)
{.links-list}
- [[JavaScript] 014：优先队列***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-014-priority-queue)
{.links-list}
- [[JavaScript] 014: 우선순위 큐***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-014-priority-queue)
{.links-list}


# Priority Queue

A priority queue is a data structure where each element has a "priority" associated with it. Elements with a higher priority are processed before elements with a lower priority.

In a priority queue, the element with the highest priority is always at the front of the queue. When elements have the same priority, they are processed in the order they were added to the queue.

## Implementation

There are many ways to implement a priority queue. One way is to use an array.

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

Another way to implement a priority queue is to use a min-heap. A min-heap is a binary tree where the root node is the element with the lowest priority. The left and right child nodes of a parent node are elements with a higher priority than the parent node.

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

## Usage

Priority queues can be used for a variety of purposes. One common use is for scheduling. For example, a priority queue can be used to schedule tasks to be executed by a computer.

Tasks that are more important (e.g. tasks with a higher priority) can be scheduled to be executed sooner than tasks that are less important (e.g. tasks with a lower priority).

Another common use for priority queues is in algorithms that need to process data that is "close" to a certain target. For example, the A* pathfinding algorithm uses a priority queue to find the shortest path from a start node to a goal node.

## Exercise

1. Implement a priority queue using an array.

2. Implement a priority queue using a min-heap.

3. Use a priority queue to schedule tasks to be executed by a computer.

4. Use a priority queue to find the shortest path in a graph.