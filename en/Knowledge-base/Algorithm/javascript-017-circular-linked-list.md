---
title: [JavaScript] 017: Circular Linked List
description: 
published: true
date: 2023-02-09T19:33:15.405Z
tags: 
editor: markdown
dateCreated: 2023-02-09T19:33:08.933Z
---

- [[JavaScript] 017: Lista enlazada circular***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-017-circular-linked-list)
{.links-list}
- [[JavaScript] 017：循环链表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-017-circular-linked-list)
{.links-list}
- [[JavaScript] 017: 순환 연결 목록***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-017-circular-linked-list)
{.links-list}


# JavaScript 017: Circular Linked List

In this post we will be discussing circular linked lists. We will talk about what they are, how they are different from regular linked lists, and how to implement them. We will also go over some of the advantages and disadvantages of using circular linked lists.

## What is a Circular Linked List?

A circular linked list is a type of linked list where the last node in the list points to the first node in the list. This creates a cycle in the list which allows us to traverse the list endlessly.

Here is an example of a circular linked list:

![Circular Linked List](https://i.imgur.com/kzgW4vD.png)

As you can see, the last node in the list (node 4) points to the first node in the list (node 1). This creates a cycle in the list.

## Difference Between Circular and Regular Linked Lists

The main difference between circular and regular linked lists is that a regular linked list will have a null pointer at the end of the list to indicate that the end of the list has been reached. A circular linked list, on the other hand, will have a pointer that points back to the first node in the list.

Here is an example of a regular linked list:

![Regular Linked List](https://i.imgur.com/FgwJKwB.png)

As you can see, the last node in the list (node 4) has a null pointer. This indicates that the end of the list has been reached.

## How to Implement a Circular Linked List

There are two ways to implement a circular linked list:

**1. Using an Array**

The first way to implement a circular linked list is to use an array. The advantage of using an array is that it is easy to implement and it is easy to traverse the list. The disadvantage of using an array is that it is not very flexible. For example, if you want to insert a new node in the middle of the list, you would have to shift all the elements in the array to make room for the new node.

Here is an example of how to implement a circular linked list using an array:

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

**2. Using a Linked List**

The second way to implement a circular linked list is to use a linked list. The advantage of using a linked list is that it is more flexible than an array. For example, if you want to insert a new node in the middle of the list, you can simply change the pointers of the nodes around the new node to point to the new node. The disadvantage of using a linked list is that it is more difficult to traverse the list.

Here is an example of how to implement a circular linked list using a linked list:

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

## Advantages and Disadvantages of Circular Linked Lists

There are both advantages and disadvantages to using circular linked lists.

**Advantages:**

- **They can be used to implement queues.** A queue is a data structure that allows you to insert elements at the back of the list and remove elements from the front of the list. This is called a First In First Out (FIFO) data structure. A circular linked list can be used to implement a queue because it allows you to insert and remove elements from the list in a FIFO manner.

- **They can be used to implement stacks.** A stack is a data structure that allows you to insert elements at the top of the list and remove elements from the top of the list. This is called a Last In First Out (LIFO) data structure. A circular linked list can be used to implement a stack because it allows you to insert and remove elements from the list in a LIFO manner.

- **They can be used to implement deques.** A deque is a data structure that allows you to insert and remove elements from both the front and the back of the list. A circular linked list can be used to implement a deque because it allows you to insert and remove elements from the list from both the front and the back.

- **They can be used to implement circular buffers.** A circular buffer is a type of queue where the last element in the list is connected to the first element in the list. This allows the queue to wrap around and reuse the elements that have already been used. A circular linked list can be used to implement a circular buffer because it allows the queue to wrap around and reuse the elements that have already been used.

- **They can be used to implement priority queues.** A priority queue is a type of queue where the elements are inserted into the queue in order of priority. This means that the element with the highest priority will be at the front of the queue and the element with the lowest priority will be at the back of the queue. A circular linked list can be used to implement a priority queue because it allows you to insert and remove elements from the list in a FIFO manner.

**Disadvantages:**

-