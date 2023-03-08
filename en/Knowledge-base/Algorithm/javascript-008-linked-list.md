---
title: [JavaScript] 008: Linked List
description: 
published: true
date: 2023-02-09T10:32:35.135Z
tags: 
editor: markdown
dateCreated: 2023-02-09T10:32:28.925Z
---

- [[JavaScript] 008: Lista vinculada***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-008-linked-list)
{.links-list}
- [[JavaScript] 008：链表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-008-linked-list)
{.links-list}
- [[JavaScript] 008: 연결된 목록***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-008-linked-list)
{.links-list}


# JavaScript 008: Linked List

A linked list is a data structure that consists of a set of nodes where each node contains a reference to the next node in the list. This type of list is very efficient for operations such as insertion and deletion as the list does not need to be rearranged.

There are two types of linked lists:

- Singly linked list: Each node has a reference to the next node.
- Doubly linked list: Each node has a reference to the next node and the previous node.

In this post, we will be implementing a singly linked list in JavaScript.

## Creating a Node

The first thing we need to do is create a node class. Each node will have two properties:

- `data`: The data that the node will hold.
- `next`: A reference to the next node in the list.

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

## Creating a Linked List

Now that we have a node class, we can create a linked list class. This class will have two properties:

- `head`: A reference to the first node in the list.
- `tail`: A reference to the last node in the list.

The linked list class will also have a few methods:

- `append(data)`: Adds a new node with the given data to the end of the list.
- `prepend(data)`: Adds a new node with the given data to the beginning of the list.
- `delete(data)`: Deletes the first node with the given data from the list.
- `print()`: Prints all the nodes in the list in order.

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

## Appending Nodes

The `append` method will add a new node with the given data to the end of the list.

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

## Prepending Nodes

The `prepend` method will add a new node with the given data to the beginning of the list.

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

## Deleting Nodes

The `delete` method will delete the first node with the given data from the list.

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

## Printing the List

The `print` method will print all the nodes in the list in order.

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

## Putting It All Together

Now that we have implemented our linked list class, let's see it in action.

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

That's all there is to it! Linked lists are a simple yet powerful data structure that can be used in a variety of applications.