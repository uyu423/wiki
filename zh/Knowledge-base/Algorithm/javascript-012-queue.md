---
title: [JavaScript] 012：队列
description: 
published: true
date: 2023-02-09T14:32:49.000Z
tags: 
editor: markdown
dateCreated: 2023-02-09T14:32:47.395Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 012: Queue***English** document is available*](/en/Knowledge-base/Algorithm/javascript-012-queue)
{.links-list}


# JavaScript 012：队列

队列是一种以先进先出 (FIFO) 方式存储项目的数据结构。也就是说，添加到队列中的第一个项目将是从队列中删除的第一个项目。队列有时称为先进先出 (FIFO) 列表。

队列的常见类比是银行排队。排在第一位的人是第一个被服务的人，排在最后一个的人是最后一个被服务的人。

队列有两个主要操作：入队和出队。 Enqueue 将一个项目添加到队列的后面，dequeue 从队列的前面删除一个项目。

## 执行

有很多方法可以实现队列。最常见的方法是使用数组。

### 数组实现

实现队列最简单的方法是使用数组。数组中的第一个元素是队列的前端，数组中的最后一个元素是队列的后端。

#### 排队

要排队一个项目，我们将项目添加到数组的末尾。

```javascript
function enqueue(item) {
  queue.push(item);
}
```

#### 出队

要使一个项目出队，我们删除数组中的第一个项目。

```javascript
function dequeue() {
  return queue.shift();
}
```

### 链表实现

实现队列的一种更有效的方法是使用链表。使用链表，我们可以避免在出队时移动数组中所有元素的昂贵操作。

#### 排队

要排队一个项目，我们将项目添加到链接列表的末尾。

```javascript
function enqueue(item) {
  var node = {
    data: item,
    next: null
  };

  if (queue.length === 0) {
    queue.head = node;
  } else {
    queue.tail.next = node;
  }

  queue.tail = node;
}
```

#### 出队

要使一个项目出队，我们删除链表中的第一个项目。

```javascript
function dequeue() {
  var node = queue.head;

  if (queue.length === 1) {
    queue.tail = null;
  }

  queue.head = node.next;
  queue.length--;

  return node.data;
}
```

## 时间复杂度

队列的数组和链表实现的时间复杂度都是 O(1)。也就是说，入队和出队都是常量时间操作。

## 例子

下面是一些使用队列的例子。

### 示例 1：数字队列

在这个例子中，我们将创建一个号码队列。我们将按顺序排列数字 0 到 9。然后我们将出列并打印每个数字，直到队列为空。

```javascript
var queue = [];

for (var i = 0; i < 10; i++) {
  enqueue(i);
}

while (queue.length > 0) {
  console.log(dequeue());
}
```

运行上面的代码将按顺序打印数字 0 到 9。

### 示例 2：模拟打印机队列

在这个例子中，我们将模拟一个打印机队列。我们将有一个打印作业队列，每个作业都有一个优先级。具有最高优先级的作业将最先出列。

```javascript
var queue = [];

function enqueue(item, priority) {
  var node = {
    data: item,
    priority: priority,
    next: null
  };

  if (queue.length === 0) {
    queue.head = node;
  } else {
    var current = queue.head;
    var previous;

    while (current && current.priority >= node.priority) {
      previous = current;
      current = current.next;
    }

    if (!previous) {
      node.next = queue.head;
      queue.head = node;
    } else {
      node.next = current;
      previous.next = node;
    }
  }

  queue.length++;
}

function dequeue() {
  var node = queue.head;
  queue.head = node.next;
  queue.length--;
  return node.data;
}

enqueue('A', 1);
enqueue('B', 2);
enqueue('C', 3);
enqueue('D', 4);
enqueue('E', 5);

console.log(dequeue()); // A
console.log(dequeue()); // B
console.log(dequeue()); // C
console.log(dequeue()); // D
console.log(dequeue()); // E
```

运行上面的代码将按顺序打印字母 A 到 E。