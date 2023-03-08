---
title: [JavaScript] 015: Single Linked List
description: 
published: true
date: 2023-02-09T17:33:43.125Z
tags: 
editor: markdown
dateCreated: 2023-02-09T17:33:36.926Z
---

- [[JavaScript] 015: lista enlazada única***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-015-single-linked-list)
{.links-list}
- [[JavaScript] 015：单链表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-015-single-linked-list)
{.links-list}
- [[JavaScript] 015: 단일 연결 목록***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-015-single-linked-list)
{.links-list}


# JavaScript 015: Single Linked List

Linked lists are a type of data structure that store a collection of data in nodes. Each node in a linked list contains two things: the data itself, and a reference to the next node in the list. Linked lists are often used because they are easy to manipulate and don't require extra memory to store the links between nodes.

There are two types of linked lists: singly-linked lists and doubly-linked lists. In a singly-linked list, each node only has a reference to the next node in the list. In a doubly-linked list, each node has a reference to both the next node and the previous node.

## Creating a Linked List

To create a linked list, we need to create a `Node` class. Each `Node` will have two properties: `data`, which stores the data for that node, and `next`, which stores the reference to the next node in the list.

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

Now that we have a `Node` class, we can create a `LinkedList` class. The `LinkedList` class will have two properties: `head`, which stores the first node in the list, and `tail`, which stores the last node in the list.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }
}
```

## Inserting Data

There are two ways to insert data into a linked list: at the head of the list, or at the tail of the list.

### Inserting at the Head

To insert data at the head of the list, we need to create a new node with the data, and set the `next` property of the new node to the current head of the list. Then, we set the head of the list to the new node.

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

### Inserting at the Tail

To insert data at the tail of the list, we need to create a new node with the data, and set the `next` property of the current tail of the list to the new node. Then, we set the tail of the list to the new node.

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

## Deleting Data

There are two ways to delete data from a linked list: from the head of the list, or from the tail of the list.

### Deleting from the Head

To delete data from the head of the list, we simply set the head of the list to the node after the current head.

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

### Deleting from the Tail

To delete data from the tail of the list, we need to keep track of the node before the tail. Then, we set the `next` property of the node before the tail to `null`, and set the tail of the list to the node before the tail.

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

## Searching for Data

To search for data in a linked list, we need to start at the head of the list and compare the data of each node to the data we are searching for. If the data is found, we return the node. If the data is not found, we return `null`.

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

## Traversing a Linked List

To traverse a linked list, we need to start at the head of the list and visit each node in turn. We can do this using a `while` loop.

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

## Reversing a Linked List

To reverse a linked list, we need to keep track of the previous node, the current node, and the next node. Then, we set the `next` property of the current node to the previous node, and move on to the next node.

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

## Sorting a Linked List

There are many different ways to sort a linked list. One way is to use the [selection sort algorithm](https://en.wikipedia.org/wiki/Selection_sort).

To sort a linked list using selection sort, we need to keep track of the minimum node, the current node, and the next node. Then, we compare the data of the current node to the data of the minimum node. If the data of the current node is less than the data of the minimum node, we set the minimum node to the current node. Once we have looped through the entire list, we swap the data of the minimum node with the data of the head node. Then, we move on to the next node and repeat the process.

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

## Conclusion

Linked lists are a type of data structure that store a collection of data in nodes. Each node in a linked list contains two things: the data itself, and a reference to the next node in the list. Linked lists are often used because they are easy to manipulate and don't require extra memory to store the links between nodes.

There are two types of linked lists: singly-linked lists and doubly-linked lists. In a singly-linked list, each node only has a reference to the next node in the list. In a doubly-linked list, each node has a reference to both the next node and the previous node.

To create a linked list, we need to create a `Node` class. Each `Node` will have two properties: `data`, which stores the data for that node, and `next`, which stores the reference to the next node in the list.

To insert data into a linked list, we can either insert at the head of the list or insert at the tail of the list. To delete data from a linked list, we can either delete from the head of the list or delete from the tail of the list.

To search for data in a linked list, we need to start at the head of the list and compare the data of each node to the data we are searching for. If the data is found, we return the node. If the data is not found, we return `null`.

To traverse a linked list, we need to start at the head of the list and visit each node in turn. To reverse a linked list, we need to keep track of the previous node, the current node, and the next node. Then, we set the `next` property of the current node to the previous node, and move on to the next node.

There are many different ways to sort a linked list. One way is to use the [selection sort algorithm](https://en.wikipedia.org/wiki/Selection_sort). To sort a linked list using selection sort, we need to keep track of the minimum node, the current node, and the next node. Then, we compare the data of the current node to the data of the minimum node. If the data of the current node is less than the data of the minimum node, we set the minimum node to the current node. Once we have looped through the entire list, we swap the data of the minimum node with the data of the head node. Then, we move on to the next node and repeat the process.