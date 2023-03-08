---
title: [JavaScript] 010：循环链表
description: 
published: true
date: 2023-02-09T12:32:50.674Z
tags: 
editor: markdown
dateCreated: 2023-02-09T12:32:49.027Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 010: Circular Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-010-circular-linked-list)
{.links-list}


# JavaScript 010：循环链表

链表是一种线性数据结构，由指向列表中下一个节点的节点组成。循环链表是一个链表，其中最后一个节点指向第一个节点，从而创建一个循环。

## 概念

链表是一种线性数据结构，由指向列表中下一个节点的节点组成。循环链表是一个链表，其中最后一个节点指向第一个节点，从而创建一个循环。

循环链表可以是单链表，其中每个节点只引用下一个节点，也可以是双向链表，其中每个节点都有对下一个节点和前一个节点的引用。

循环链表是一种可用于存储项目列表的数据结构。它类似于单向链表，只是链表中的最后一个节点指向第一个节点。这会创建一个循环，以便您可以无休止地浏览列表。

与单向链表相比，使用循环链表有几个优点。首先，它更容易实现，因为您不需要跟踪列表的末尾。其次，它更高效，因为您可以从列表中的任何一点开始并遍历整个列表，而无需从头开始重新启动。最后，它更加灵活，因为您可以在列表中的任意位置插入和删除项目。

## 代码示例

下面是 JavaScript 中循环链表的简单实现。

```javascript
function Node(data) {
  this.data = data;
  this.next = null;
}

function CircularLinkedList() {
  this.head = null;
  this.tail = null;
  this.length = 0;
}

CircularLinkedList.prototype.add = function(data) {
  var node = new Node(data);

  if (this.length === 0) {
    this.head = node;
  } else {
    this.tail.next = node;
  }

  node.next = this.head;
  this.tail = node;
  this.length++;
};

CircularLinkedList.prototype.remove = function(data) {
  var current = this.head;
  var previous = null;
  var index = 0;

  if (this.length === 0) {
    return null;
  }

  if (this.length === 1) {
    this.head = null;
    this.tail = null;
    this.length--;
    return current.data;
  }

  while (current) {
    if (current.data === data) {
      previous.next = current.next;
      this.length--;
      return current.data;
    }

    previous = current;
    current = current.next;
    index++;
  }

  return null;
};

CircularLinkedList.prototype.get = function(index) {
  var current = this.head;
  var count = 0;

  while (count < index) {
    current = current.next;
    count++;
  }

  return current.data;
};

CircularLinkedList.prototype.contains = function(data) {
  var current = this.head;

  while (current) {
    if (current.data === data) {
      return true;
    }

    current = current.next;
  }

  return false;
};

CircularLinkedList.prototype.size = function() {
  return this.length;
};

CircularLinkedList.prototype.toString = function() {
  var current = this.head;
  var string = '';

  while (current) {
    string += current.data + ' ';
    current = current.next;
  }

  return string.trim();
};

var list = new CircularLinkedList();
list.add('a');
list.add('b');
list.add('c');
list.add('d');
console.log(list.toString()); // a b c d
list.remove('c');
console.log(list.toString()); // a b d
console.log(list.contains('a')); // true
console.log(list.contains('b')); // true
console.log(list.contains('c')); // false
console.log(list.contains('d')); // true
console.log(list.get(0)); // a
console.log(list.get(1)); // b
console.log(list.get(2)); // d
console.log(list.size()); // 3
```

## 练习

1. 实现一种在列表中的特定索引处插入项目的方法。

2. 实现一个反转列表的方法。

## 答案

1.

```javascript
CircularLinkedList.prototype.insert = function(index, data) {
  if (index < 0 || index > this.length) {
    return null;
  }

  var node = new Node(data);
  var current = this.head;
  var previous = null;
  var count = 0;

  if (index === 0) {
    if (this.head) {
      node.next = this.head;
    }

    this.head = node;
  } else {
    while (count < index) {
      previous = current;
      current = current.next;
      count++;
    }

    node.next = current;
    previous.next = node;
  }

  this.length++;
  return node.data;
};
```

2.

```javascript
CircularLinkedList.prototype.reverse = function() {
  var current = this.head;
  var previous = null;
  var next = null;

  while (current) {
    next = current.next;
    current.next = previous;
    previous = current;
    current = next;
  }

  this.tail = this.head;
  this.head = previous;
};
```