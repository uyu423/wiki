---
title: [JavaScript] 017：循环链表
description: 
published: true
date: 2023-02-09T19:33:10.617Z
tags: 
editor: markdown
dateCreated: 2023-02-09T19:33:08.905Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 017: Circular Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-017-circular-linked-list)
{.links-list}


# JavaScript 017：循环链表

在这篇文章中，我们将讨论循环链表。我们将讨论它们是什么，它们与常规链表有何不同，以及如何实现它们。我们还将讨论使用循环链表的一些优点和缺点。

## 什么是循环链表？

循环链表是一种链表，其中链表的最后一个节点指向链表的第一个节点。这在列表中创建了一个循环，使我们可以无休止地遍历列表。

下面是一个循环链表的例子：

![循环链表](https://i.imgur.com/kzgW4vD.png)

如您所见，列表中的最后一个节点（节点 4）指向列表中的第一个节点（节点 1）。这会在列表中创建一个循环。

## 循环链表和常规链表的区别

循环链表和常规链表的主要区别在于，常规链表在链表的末尾会有一个空指针，以指示已到达链表的末尾。另一方面，循环链表将有一个指针指向链表中的第一个节点。

下面是一个常规链表的例子：

![正则链表](https://i.imgur.com/FgwJKwB.png)

如您所见，列表中的最后一个节点（节点 4）有一个空指针。这表示已到达列表末尾。

## 如何实现循环链表

循环链表有两种实现方式：

**1。使用数组**

实现循环链表的第一种方法是使用数组。使用数组的好处是容易实现，容易遍历链表。使用数组的缺点是它不是很灵活。例如，如果要在列表中间插入一个新节点，则必须移动数组中的所有元素以为新节点腾出空间。

以下是如何使用数组实现循环链表的示例：

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class CircularLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  // add a new node to the end of the list
  append(data) {
    // create a new node
    let node = new Node(data);

    // if the list is empty, set the head and tail to the new node
    if (this.size === 0) {
      this.head = node;
      this.tail = node;
    } else {
      // otherwise, set the current tail's next pointer to the new node
      this.tail.next = node;
      // and set the new node as the current tail
      this.tail = node;
    }

    // set the new node's next pointer to the head
    node.next = this.head;

    // increment the size
    this.size++;
  }

  // remove the node at the given index
  removeAt(index) {
    // if the index is out of bounds, return null
    if (index < 0 || index >= this.size) {
      return null;
    }

    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // if the index is the same as the size of the list,
    // it means we want to remove the tail
    if (index === this.size - 1) {
      // so set the current tail's next pointer to the head
      this.tail.next = this.head;
      // and set the head as the current tail
      this.tail = this.tail.next;
    } else {
      // otherwise, we need to find the node at the given index
      // so set a pointer to the head
      let pointer = this.head;
      // and set a counter to keep track of our position
      let counter = 0;

      // loop through the list until we find the node at the given index
      while (counter < index) {
        pointer = pointer.next;
        counter++;
      }

      // set the next pointer of the node before the one we want to remove
      // to the node after the one we want to remove
      pointer.next = pointer.next.next;
    }

    // decrement the size
    this.size--;
  }

  // return the node at the given index
  get(index) {
    // if the index is out of bounds, return null
    if (index < 0 || index >= this.size) {
      return null;
    }

    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // set a pointer to the head
    let pointer = this.head;

    // loop through the list until we find the node at the given index
    for (let i = 0; i < index; i++) {
      pointer = pointer.next;
    }

    // return the node at the given index
    return pointer;
  }

  // return the size of the list
  getSize() {
    return this.size;
  }

  // return the head of the list
  getHead() {
    return this.head;
  }

  // return the tail of the list
  getTail() {
    return this.tail;
  }

  // return true if the list is empty, false otherwise
  isEmpty() {
    return this.size === 0;
  }

  // print the list
  print() {
    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // set a pointer to the head
    let pointer = this.head;

    // loop through the list until we reach the tail
    while (pointer.next !== this.tail) {
      // print the data of the current node
      console.log(pointer.data);
      // and set the pointer to the next node
      pointer = pointer.next;
    }

    // print the data of the tail
    console.log(pointer.data);
  }
}

// create a new linked list
let list = new CircularLinkedList();

// append some nodes
list.append(1);
list.append(2);
list.append(3);
list.append(4);

// print the list
list.print(); // 1 2 3 4

// remove a node
list.removeAt(2);

// print the list
list.print(); // 1 2 4

// get the node at the given index
let node = list.get(1);

// print the data of the node
console.log(node.data); // 2

// get the size of the list
let size = list.getSize();

// print the size of the list
console.log(size); // 3

// get the head of the list
let head = list.getHead();

// print the data of the head
console.log(head.data); // 1

// get the tail of the list
let tail = list.getTail();

// print the data of the tail
console.log(tail.data); // 4

// check if the list is empty
let isEmpty = list.isEmpty();

// print true if the list is empty, false otherwise
console.log(isEmpty); // false
```

**2。使用链表**

循环链表的第二种实现方式是使用链表。使用链表的好处是它比数组更灵活。例如，如果你想在链表的中间插入一个新节点，你可以简单地改变新节点周围节点的指针指向新节点。使用链表的缺点是遍历列表比较困难。

下面举例说明如何使用链表实现循环链表：

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class CircularLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  // add a new node to the end of the list
  append(data) {
    // create a new node
    let node = new Node(data);

    // if the list is empty, set the head and tail to the new node
    if (this.size === 0) {
      this.head = node;
      this.tail = node;
    } else {
      // otherwise, set the current tail's next pointer to the new node
      this.tail.next = node;
      // and set the new node as the current tail
      this.tail = node;
    }

    // set the new node's next pointer to the head
    node.next = this.head;

    // increment the size
    this.size++;
  }

  // remove the node at the given index
  removeAt(index) {
    // if the index is out of bounds, return null
    if (index < 0 || index >= this.size) {
      return null;
    }

    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // if the index is the same as the size of the list,
    // it means we want to remove the tail
    if (index === this.size - 1) {
      // so set the current tail's next pointer to the head
      this.tail.next = this.head;
      // and set the head as the current tail
      this.tail = this.tail.next;
    } else {
      // otherwise, we need to find the node at the given index
      // so set a pointer to the head
      let pointer = this.head;
      // and set a counter to keep track of our position
      let counter = 0;

      // loop through the list until we find the node before the one we want to remove
      while (counter < index - 1) {
        pointer = pointer.next;
        counter++;
      }

      // set the next pointer of the node before the one we want to remove
      // to the node after the one we want to remove
      pointer.next = pointer.next.next;
    }

    // decrement the size
    this.size--;
  }

  // return the node at the given index
  get(index) {
    // if the index is out of bounds, return null
    if (index < 0 || index >= this.size) {
      return null;
    }

    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // set a pointer to the head
    let pointer = this.head;

    // loop through the list until we find the node at the given index
    for (let i = 0; i < index; i++) {
      pointer = pointer.next;
    }

    // return the node at the given index
    return pointer;
  }

  // return the size of the list
  getSize() {
    return this.size;
  }

  // return the head of the list
  getHead() {
    return this.head;
  }

  // return the tail of the list
  getTail() {
    return this.tail;
  }

  // return true if the list is empty, false otherwise
  isEmpty() {
    return this.size === 0;
  }

  // print the list
  print() {
    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // set a pointer to the head
    let pointer = this.head;

    // loop through the list until we reach the tail
    while (pointer.next !== this.tail) {
      // print the data of the current node
      console.log(pointer.data);
      // and set the pointer to the next node
      pointer = pointer.next;
    }

    // print the data of the tail
    console.log(pointer.data);
  }
}

// create a new linked list
let list = new CircularLinkedList();

// append some nodes
list.append(1);
list.append(2);
list.append(3);
list.append(4);

// print the list
list.print(); // 1 2 3 4

// remove a node
list.removeAt(2);

// print the list
list.print(); // 1 2 4

// get the node at the given index
let node = list.get(1);

// print the data of the node
console.log(node.data); // 2

// get the size of the list
let size = list.getSize();

// print the size of the list
console.log(size); // 3

// get the head of the list
let head = list.getHead();

// print the data of the head
console.log(head.data); // 1

// get the tail of the list
let tail = list.getTail();

// print the data of the tail
console.log(tail.data); // 4

// check if the list is empty
let isEmpty = list.isEmpty();

// print true if the list is empty, false otherwise
console.log(isEmpty); // false
```

## 循环链表的优缺点

使用循环链表既有优点也有缺点。

**优点：**

- **它们可用于实现队列。** 队列是一种数据结构，允许您在列表的后面插入元素并从列表的前面删除元素。这称为先进先出 (FIFO) 数据结构。循环链表可用于实现队列，因为它允许您以 FIFO 方式从列表中插入和删除元素。

- **它们可用于实现堆栈。** 堆栈是一种数据结构，允许您在列表顶部插入元素并从列表顶部移除元素。这称为后进先出 (LIFO) 数据结构。循环链表可用于实现堆栈，因为它允许您以后进先出的方式在列表中插入和删除元素。

- **它们可用于实现双端队列。**双端队列是一种数据结构，允许您从列表的前面和后面插入和删除元素。循环链表可用于实现双端队列，因为它允许您从列表的前面和后面插入和删除元素。

- **它们可用于实现循环缓冲区。**循环缓冲区是一种队列，其中列表中的最后一个元素连接到列表中的第一个元素。这允许队列环绕并重用已经使用过的元素。循环链表可以用来实现循环缓冲区，因为它允许队列环绕并重用已经使用过的元素。

- **它们可用于实现优先级队列。**优先级队列是一种队列，其中元素按优先级顺序插入队列。这意味着具有最高优先级的元素将位于队列的前端，而具有最低优先级的元素将位于队列的后端。循环链表可用于实现优先级队列，因为它允许您以 FIFO 方式从列表中插入和删除元素。

**缺点：**

-