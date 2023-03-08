---
title: [JavaScript] 010: Circular Linked List
description: 
published: true
date: 2023-02-09T12:32:55.111Z
tags: 
editor: markdown
dateCreated: 2023-02-09T12:32:49.065Z
---

- [[JavaScript] 010: Lista enlazada circular***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-010-circular-linked-list)
{.links-list}
- [[JavaScript] 010：循环链表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-010-circular-linked-list)
{.links-list}
- [[JavaScript] 010: 순환 연결 목록***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-010-circular-linked-list)
{.links-list}


# JavaScript 010: Circular Linked List

A linked list is a linear data structure, made up of nodes that point to the next node in the list. A circular linked list is a linked list where the last node points back to the first node, creating a loop.

## Concept

A linked list is a linear data structure, made up of nodes that point to the next node in the list. A circular linked list is a linked list where the last node points back to the first node, creating a loop.

A circular linked list can be a singly linked list, where each node only has a reference to the next node, or a doubly linked list, where each node has a reference to the next node and the previous node.

A circular linked list is a data structure that can be used to store a list of items. It is similar to a singly linked list, except that the last node in the list points back to the first node. This creates a loop, so that you can go through the list endlessly.

There are several advantages to using a circular linked list over a singly linked list. First, it is easier to implement because you do not need to keep track of the end of the list. Second, it is more efficient because you can start at any point in the list and traverse the entire list without having to restart at the beginning. Finally, it is more flexible because you can insert and delete items at any point in the list.

## Code Examples

Here is a simple implementation of a circular linked list in JavaScript.

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

## Exercises

1. Implement a method to insert an item at a specific index in the list.

2. Implement a method to reverse the list.

## Answers

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