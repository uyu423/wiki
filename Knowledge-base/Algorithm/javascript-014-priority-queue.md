---
title: [JavaScript] 014: 우선순위 큐
description: 
published: true
date: 2023-02-09T16:32:46.529Z
tags: 
editor: markdown
dateCreated: 2023-02-09T16:32:40.306Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 014: Priority Queue***English** document is available*](/en/Knowledge-base/Algorithm/javascript-014-priority-queue)
{.links-list}


# 우선순위 대기열

우선 순위 큐는 각 요소에 관련된 "우선 순위"가 있는 데이터 구조입니다. 우선 순위가 높은 요소는 우선 순위가 낮은 요소보다 먼저 처리됩니다.

우선순위 큐에서 우선순위가 가장 높은 요소는 항상 큐의 맨 앞에 있습니다. 요소의 우선 순위가 같으면 대기열에 추가된 순서대로 처리됩니다.

## 구현

우선순위 큐를 구현하는 방법에는 여러 가지가 있습니다. 한 가지 방법은 배열을 사용하는 것입니다.

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

우선 순위 큐를 구현하는 또 다른 방법은 최소 힙을 사용하는 것입니다. 최소 힙은 루트 노드가 우선 순위가 가장 낮은 요소인 이진 트리입니다. 부모 노드의 좌우 자식 노드는 부모 노드보다 우선순위가 높은 요소입니다.

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

## 용법

우선 순위 큐는 다양한 용도로 사용할 수 있습니다. 한 가지 일반적인 용도는 스케줄링입니다. 예를 들어 우선 순위 대기열을 사용하여 컴퓨터에서 실행할 작업을 예약할 수 있습니다.

더 중요한 작업(예: 우선순위가 높은 작업)은 덜 중요한 작업(예: 우선순위가 낮은 작업)보다 더 빨리 실행되도록 예약할 수 있습니다.

우선 순위 대기열의 또 다른 일반적인 용도는 특정 대상에 "가까운" 데이터를 처리해야 하는 알고리즘입니다. 예를 들어 A* 경로 찾기 알고리즘은 우선순위 큐를 사용하여 시작 노드에서 목표 노드까지의 최단 경로를 찾습니다.

## 운동

1. 배열을 사용하여 우선 순위 대기열을 구현합니다.

2. 최소 힙을 사용하여 우선 순위 큐를 구현합니다.

3. 우선 순위 대기열을 사용하여 컴퓨터에서 실행할 작업을 예약합니다.

4. 우선 순위 대기열을 사용하여 그래프에서 최단 경로를 찾습니다.