---
title: [JavaScript] 008：链表
description: 
published: true
date: 2023-02-09T10:32:30.584Z
tags: 
editor: markdown
dateCreated: 2023-02-09T10:32:28.916Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 008: Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-008-linked-list)
{.links-list}


# JavaScript 008：链表

链表是一种数据结构，由一组节点组成，其中每个节点都包含对列表中下一个节点的引用。这种类型的列表对于插入和删除等操作非常有效，因为列表不需要重新排列。

有两种类型的链表：

- 单向链表：每个节点都有对下一个节点的引用。
- 双向链表：每个节点都有对下一个节点和前一个节点的引用。

在这篇文章中，我们将在 JavaScript 中实现一个单向链表。

## 创建节点

我们需要做的第一件事是创建一个节点类。每个节点都有两个属性：

- `data`：节点将保存的数据。
- `next`：对列表中下一个节点的引用。

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

## 创建链表

现在我们有了一个节点类，我们可以创建一个链表类。这个类将有两个属性：

- `head`：对列表中第一个节点的引用。
- `tail`：对列表中最后一个节点的引用。

链表类也会有几个方法：

- `append(data)`：将具有给定数据的新节点添加到列表的末尾。
- `prepend(data)`：将具有给定数据的新节点添加到列表的开头。
- `delete(data)`：从列表中删除具有给定数据的第一个节点。
- `print()`：按顺序打印列表中的所有节点。

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  append(data) {
    // code here
  }

  prepend(data) {
    // code here
  }

  delete(data) {
    // code here
  }

  print() {
    // code here
  }
}
```

## 追加节点

`append` 方法会将具有给定数据的新节点添加到列表的末尾。

```javascript
append(data) {
  // create a new node with the given data
  const newNode = new Node(data);

  // if the list is empty, set the new node as the head and tail
  if (!this.head) {
    this.head = newNode;
    this.tail = newNode;
  } else {
    // set the current tail's next property to the new node
    this.tail.next = newNode;

    // set the new node as the current tail
    this.tail = newNode;
  }
}
```

## 前置节点

`prepend` 方法会将具有给定数据的新节点添加到列表的开头。

```javascript
prepend(data) {
  // create a new node with the given data
  const newNode = new Node(data);

  // if the list is empty, set the new node as the head and tail
  if (!this.head) {
    this.head = newNode;
    this.tail = newNode;
  } else {
    // set the new node's next property to the current head
    newNode.next = this.head;

    // set the new node as the current head
    this.head = newNode;
  }
}
```

## 删除节点

`delete` 方法将从列表中删除具有给定数据的第一个节点。

```javascript
delete(data) {
  // if the list is empty, do nothing
  if (!this.head) {
    return;
  }

  // if the head contains the data to be deleted, delete it and set the next node as the new head
  if (this.head.data === data) {
    this.head = this.head.next;
    return;
  }

  // start at the head
  let currentNode = this.head;

  // loop until the tail
  while (currentNode.next) {
    // if the next node contains the data to be deleted, delete it and set the current node's next property to the next node's next property
    if (currentNode.next.data === data) {
      currentNode.next = currentNode.next.next;
      return;
    }

    // if the data is not found, move to the next node
    currentNode = currentNode.next;
  }
}
```

## 打印列表

`print` 方法将按顺序打印列表中的所有节点。

```javascript
print() {
  // if the list is empty, do nothing
  if (!this.head) {
    return;
  }

  // start at the head
  let currentNode = this.head;

  // loop until the tail
  while (currentNode) {
    // print the current node's data
    console.log(currentNode.data);

    // move to the next node
    currentNode = currentNode.next;
  }
}
```

## 把它们放在一起

现在我们已经实现了链表类，让我们看看它的实际应用。

```javascript
// create a new linked list
const list = new LinkedList();

// append some nodes
list.append(1);
list.append(2);
list.append(3);

// prepend a node
list.prepend(0);

// delete a node
list.delete(2);

// print the list
list.print();
// 0 -> 1 -> 3
```

这里的所有都是它的！链表是一种简单但功能强大的数据结构，可用于各种应用程序。