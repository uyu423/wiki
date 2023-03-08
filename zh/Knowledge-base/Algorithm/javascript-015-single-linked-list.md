---
title: [JavaScript] 015：单链表
description: 
published: true
date: 2023-02-09T17:33:38.605Z
tags: 
editor: markdown
dateCreated: 2023-02-09T17:33:36.920Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 015: Single Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-015-single-linked-list)
{.links-list}


# JavaScript 015: 单链表

链表是一种在节点中存储数据集合的数据结构。链表中的每个节点都包含两件事：数据本身，以及对列表中下一个节点的引用。经常使用链表是因为它们易于操作并且不需要额外的内存来存储节点之间的链接。

有两种类型的链表：单链表和双向链表。在单向链表中，每个节点只有对链表中下一个节点的引用。在双向链表中，每个节点都有对下一个节点和前一个节点的引用。

## 创建链表

要创建链表，我们需要创建一个 `Node` 类。每个 `Node` 都有两个属性：`data`，它存储该节点的数据，以及 `next`，它存储对列表中下一个节点的引用。

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

现在我们有了一个 `Node` 类，我们可以创建一个 `LinkedList` 类。 `LinkedList` 类将有两个属性：`head`，它存储列表中的第一个节点，以及 `tail`，它存储列表中的最后一个节点。

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }
}
```

## 插入数据

向链表中插入数据有两种方式：在链表的头部，或者在链表的尾部。

### 在头部插入

要在列表的头部插入数据，我们需要用数据创建一个新节点，并将新节点的 `next` 属性设置为列表的当前头部。然后，我们将列表的头部设置为新节点。

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  insertAtHead(data) {
    const newNode = new Node(data);
    newNode.next = this.head;
    this.head = newNode;
  }
}
```

### 在尾部插入

要在列表的尾部插入数据，我们需要用数据创建一个新节点，并将列表当前尾部的 `next` 属性设置为新节点。然后，我们将列表的尾部设置为新节点。

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  insertAtTail(data) {
    const newNode = new Node(data);
    if (!this.head) {
      this.head = newNode;
    }
    if (this.tail) {
      this.tail.next = newNode;
    }
    this.tail = newNode;
  }
}
```

## 删除数据

从链表中删除数据有两种方法：从表头删除，或从表尾删除。

### 从头部删除

要从列表的头部删除数据，我们只需将列表的头部设置为当前头部之后的节点。

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  deleteFromHead() {
    if (!this.head) {
      return;
    }
    this.head = this.head.next;
  }
}
```

### 从尾部删除

要从列表的尾部删除数据，我们需要跟踪尾部之前的节点。然后，我们将尾部之前的节点的 next 属性设置为 null ，并将列表的尾部设置为尾部之前的节点。

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  deleteFromTail() {
    if (!this.tail) {
      return;
    }
    if (!this.head) {
      this.head = null;
      this.tail = null;
      return;
    }
    let current = this.head;
    while (current.next !== this.tail) {
      current = current.next;
    }
    current.next = null;
    this.tail = current;
  }
}
```

## 搜索数据

要在链表中搜索数据，我们需要从链表的头部开始，将每个节点的数据与我们要搜索的数据进行比较。如果找到数据，我们返回节点。如果未找到数据，我们将返回“null”。

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

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
}
```

## 遍历链表

要遍历链表，我们需要从链表的头部开始，依次访问每个节点。我们可以使用“while”循环来做到这一点。

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  traverse() {
    let current = this.head;
    while (current) {
      console.log(current.data);
      current = current.next;
    }
  }
}
```

## 反转链表

要反转链表，我们需要跟踪前一个节点、当前节点和下一个节点。然后，我们将当前节点的 `next` 属性设置为前一个节点，并移动到下一个节点。

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  reverse() {
    let current = this.head;
    let previous = null;
    let next = null;
    while (current) {
      next = current.next;
      current.next = previous;
      previous = current;
      current = next;
    }
    this.head = previous;
  }
}
```

## 对链表进行排序

有许多不同的方法可以对链表进行排序。一种方法是使用[选择排序算法](https://en.wikipedia.org/wiki/Selection_sort)。

要使用选择排序对链表进行排序，我们需要跟踪最小节点、当前节点和下一个节点。然后，我们将当前节点的数据与最小节点的数据进行比较。如果当前节点的数据小于最小节点的数据，我们将最小节点设置为当前节点。一旦我们遍历了整个列表，我们就将最小节点的数据与头节点的数据交换。然后，我们移动到下一个节点并重复该过程。

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  sort() {
    let current = this.head;
    let minimum = null;
    let next = null;
    while (current) {
      minimum = current;
      next = current.next;
      while (next) {
        if (next.data < minimum.data) {
          minimum = next;
        }
        next = next.next;
      }
      if (minimum !== current) {
        const temp = current.data;
        current.data = minimum.data;
        minimum.data = temp;
      }
      current = current.next;
    }
  }
}
```

## 结论

链表是一种在节点中存储数据集合的数据结构。链表中的每个节点都包含两件事：数据本身，以及对列表中下一个节点的引用。经常使用链表是因为它们易于操作并且不需要额外的内存来存储节点之间的链接。

有两种类型的链表：单链表和双向链表。在单向链表中，每个节点只有对链表中下一个节点的引用。在双向链表中，每个节点都有对下一个节点和前一个节点的引用。

要创建链表，我们需要创建一个 `Node` 类。每个 `Node` 都有两个属性：`data`，它存储该节点的数据，以及 `next`，它存储对列表中下一个节点的引用。

要向链表中插入数据，我们可以在链表的头部插入，也可以在链表的尾部插入。要从链表中删除数据，我们可以从链表的头部删除，也可以从链表的尾部删除。

要在链表中搜索数据，我们需要从链表的头部开始，将每个节点的数据与我们要搜索的数据进行比较。如果找到数据，我们返回节点。如果未找到数据，我们将返回“null”。

要遍历链表，我们需要从链表的头部开始，依次访问每个节点。要反转链表，我们需要跟踪前一个节点、当前节点和下一个节点。然后，我们将当前节点的 `next` 属性设置为前一个节点，并移动到下一个节点。

有许多不同的方法可以对链表进行排序。一种方法是使用[选择排序算法](https://en.wikipedia.org/wiki/Selection_sort)。要使用选择排序对链表进行排序，我们需要跟踪最小节点、当前节点和下一个节点。然后，我们将当前节点的数据与最小节点的数据进行比较。如果当前节点的数据小于最小节点的数据，我们将最小节点设置为当前节点。一旦我们遍历了整个列表，我们就将最小节点的数据与头节点的数据交换。然后，我们移动到下一个节点并重复该过程。