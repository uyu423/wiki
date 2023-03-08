---
title: [JavaScript] 009：双链表
description: 
published: true
date: 2023-02-09T11:32:54.013Z
tags: 
editor: markdown
dateCreated: 2023-02-09T11:32:47.796Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 009: Double Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-009-double-linked-list)
{.links-list}


# JavaScript 009：双链表

## 什么是双向链表？

**双链表**是一种由一组节点组成的数据结构，每个节点都指向列表中的下一个和前一个节点。当我们需要能够前后移动数据时，通常会使用这种类型的链表。

## 节点对象

在双向链表中，每个节点都有两个指针：
* `next`: 指向列表中的下一个节点
* `prev`: 指向列表中的前一个节点

此外，每个节点都有一个保存实际数据的“数据”属性。

## 创建双链表

让我们创建一个具有三个节点的简单双链表。我们将从创建一个 `Node` 类开始：

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
    this.prev = null;
  }
}
```

现在我们可以创建我们的 LinkedList 类：

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }
}
```

我们的 LinkedList 有两个属性：
* `head`: 指向列表中的第一个节点
* `tail`: 指向列表中的最后一个节点

## 插入节点

将节点插入双链表有两种方式：
* 在列表的**头部**
* 在列表的**尾部**

我们将从“insertAtHead”方法开始。此方法采用“数据”参数并使用该数据创建一个新节点。然后将新节点指定为列表的“头”，并将新节点的“下一个”指针设置为指向旧头节点。最后，将旧头节点的 `prev` 指针设置为指向新节点。

```javascript
insertAtHead(data) {
  const newNode = new Node(data);
  newNode.next = this.head;
  this.head.prev = newNode;
  this.head = newNode;
}
```

`insertAtTail` 方法类似，但是新节点被赋值为链表的`tail`，并将新节点的`prev` 指针设置为指向旧的尾节点。最后，旧尾节点的 next 指针被设置为指向新节点。

```javascript
insertAtTail(data) {
  const newNode = new Node(data);
  newNode.prev = this.tail;
  this.tail.next = newNode;
  this.tail = newNode;
}
```

## 删除节点

从双链表中删除节点也有两种方法：
* 来自列表的**头部**
* 来自列表的**尾部**

我们将从 deleteFromHead 方法开始。此方法只是将列表的“head”分配给当前头节点的“next”指针所指向的节点。然后，新头节点的 `prev` 指针被设置为 `null`。

```javascript
deleteFromHead() {
  this.head = this.head.next;
  this.head.prev = null;
}
```

`deleteFromTail` 方法类似，只是将链表的`tail` 赋值给当前尾节点的`prev` 指针所指向的节点。然后，将新尾节点的“next”指针设置为“null”。

```javascript
deleteFromTail() {
  this.tail = this.tail.prev;
  this.tail.next = null;
}
```

## 搜索列表

我们可以使用 `search` 方法在列表中搜索特定数据。此方法采用“数据”参数并返回包含该数据的节点。如果未找到数据，则该方法返回“null”。

```javascript
search(data) {
  let current = this.head;

  while (current) {
    if (current.data === data) {
      return current;
    }
    current = current.next;
  }

  return null;
}
```

## 遍历列表

我们可以使用 `traverse` 方法遍历列表。此方法采用在列表中的每个节点上调用的“回调”函数。

```javascript
traverse(callback) {
  let current = this.head;

  while (current) {
    callback(current);
    current = current.next;
  }
}
```

## 反转列表

我们可以使用 `reverse` 方法反转列表。此方法只是交换列表中每个节点的“next”和“prev”指针。

```javascript
reverse() {
  let current = this.head;

  while (current) {
    const temp = current.next;
    current.next = current.prev;
    current.prev = temp;
    current = current.next;
  }

  const temp = this.head;
  this.head = this.tail;
  this.tail = temp;
}
```

## 结论

在本文中，我们了解了如何创建和使用双向链表。当我们需要能够前后移动数据时，这种数据结构会很有用。