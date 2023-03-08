---
title: [JavaScript] 013: Deque
description: 
published: true
date: 2023-02-09T15:32:34.873Z
tags: 
editor: markdown
dateCreated: 2023-02-09T15:32:28.707Z
---

- [[JavaScript] 013: Entonces***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-013-deque)
{.links-list}
- [[JavaScript] 013：所以***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-013-deque)
{.links-list}
- [[JavaScript] 013: 그래서***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-013-deque)
{.links-list}


# Deque

A deque, also known as a double-ended queue, is an ordered collection of items that allows the addition or removal of elements from either end of the queue. Deques are a generalization of stacks and queues and are often implemented as a doubly-linked list.

## Operations

Deques support the following operations:

* ```push(x)```: Adds an item x to the back of the deque.
* ```pop()```: Removes and returns the item at the back of the deque.
* ```unshift(x)```: Adds an item x to the front of the deque.
* ```shift()```: Removes and returns the item at the front of the deque.

## Implementation

In JavaScript, we can implement a deque using an array:

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

## Usage

We can use a deque to implement a queue, where the ```unshift()``` and ```shift()``` operations are used:

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

We can also use a deque to implement a stack, where the ```push()``` and ```pop()``` operations are used:

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

## Exercises

1. Implement a queue using a deque.

2. Implement a stack using a deque.

3. Implement a palindrome checker using a deque.