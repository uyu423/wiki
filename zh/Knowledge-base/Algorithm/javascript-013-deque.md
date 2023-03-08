---
title: [JavaScript] 013：所以
description: 
published: true
date: 2023-02-09T15:32:30.279Z
tags: 
editor: markdown
dateCreated: 2023-02-09T15:32:28.699Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 013: Deque***English** document is available*](/en/Knowledge-base/Algorithm/javascript-013-deque)
{.links-list}


# 双端队列

双端队列，也称为双端队列，是一个有序的项目集合，允许从队列的任一端添加或删除元素。双端队列是栈和队列的推广，通常以双向链表的形式实现。

## 操作

双端队列支持以下操作：

* ```push(x)```: 添加一个项目 x 到双端队列的后面。
*```pop()```：删除并返回双端队列后面的项目。
*```unshift(x)```：将项目 x 添加到双端队列的前面。
*```shift()```：删除并返回双端队列前面的项目。

## 执行

在 JavaScript 中，我们可以使用数组实现双端队列：

```javascript
function Deque() {
  this.dataStore = [];
  this.push = push;
  this.pop = pop;
  this.unshift = unshift;
  this.shift = shift;
}

function push(element) {
  this.dataStore.push(element);
}

function pop() {
  return this.dataStore.pop();
}

function unshift(element) {
  this.dataStore.unshift(element);
}

function shift() {
  return this.dataStore.shift();
}
```

## 用法

我们可以使用双端队列来实现队列，其中使用了 ```unshift()``` 和 ```shift()``` 操作：

```javascript
function Queue() {
  this.dataStore = [];
  this.enqueue = enqueue;
  this.dequeue = dequeue;
}

function enqueue(element) {
  this.dataStore.unshift(element);
}

function dequeue() {
  return this.dataStore.shift();
}
```

我们还可以使用双端队列来实现堆栈，其中使用了 ```push()``` 和 ```pop()``` 操作：

```javascript
function Stack() {
  this.dataStore = [];
  this.push = push;
  this.pop = pop;
}

function push(element) {
  this.dataStore.push(element);
}

function pop() {
  return this.dataStore.pop();
}
```

## 练习

1.使用双端队列实现队列。

2. 使用双端队列实现堆栈。

3. 使用双端队列实现回文检查器。