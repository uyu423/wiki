---
title: [JavaScript] 009: Double Linked List
description: 
published: true
date: 2023-02-09T11:32:49.479Z
tags: 
editor: markdown
dateCreated: 2023-02-09T11:32:47.804Z
---

- [[JavaScript] 009: Lista de enlaces dobles***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-009-double-linked-list)
{.links-list}
- [[JavaScript] 009：双链表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-009-double-linked-list)
{.links-list}
- [[JavaScript] 009: 이중 연결 목록***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-009-double-linked-list)
{.links-list}


# JavaScript 009: Double Linked List

## What is a Double Linked List?

A **double linked list** is a data structure that consists of a set of nodes, each pointing to the next and the previous node in the list. This type of linked list is often used when we need to be able to move backwards and forwards through the data.

## The Node Object

In a double linked list, each node has two pointers:
* `next`: pointing to the next node in the list
* `prev`: pointing to the previous node in the list

In addition, each node has a `data` attribute which holds the actual data.

## Creating a Double Linked List

Let's create a simple double linked list with three nodes. We'll start by creating a `Node` class:

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
    this.prev = null;
  }
}
```

Now we can create our `LinkedList` class:

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }
}
```

Our `LinkedList` has two attributes:
* `head`: pointing to the first node in the list
* `tail`: pointing to the last node in the list

## Inserting Nodes

There are two ways to insert nodes into a double linked list:
* at the **head** of the list
* at the **tail** of the list

We'll start with the `insertAtHead` method. This method takes a `data` parameter and creates a new node with that data. The new node is then assigned as the `head` of the list, and the `next` pointer of the new node is set to point to the old head node. Finally, the `prev` pointer of the old head node is set to point to the new node.

```javascript
insertAtHead(data) {
  const newNode = new Node(data);
  newNode.next = this.head;
  this.head.prev = newNode;
  this.head = newNode;
}
```

The `insertAtTail` method is similar, but the new node is assigned as the `tail` of the list, and the `prev` pointer of the new node is set to point to the old tail node. Finally, the `next` pointer of the old tail node is set to point to the new node.

```javascript
insertAtTail(data) {
  const newNode = new Node(data);
  newNode.prev = this.tail;
  this.tail.next = newNode;
  this.tail = newNode;
}
```

## Deleting Nodes

There are also two ways to delete nodes from a double linked list:
* from the **head** of the list
* from the **tail** of the list

We'll start with the `deleteFromHead` method. This method simply assigns the `head` of the list to the node pointed to by the `next` pointer of the current head node. Then, the `prev` pointer of the new head node is set to `null`.

```javascript
deleteFromHead() {
  this.head = this.head.next;
  this.head.prev = null;
}
```

The `deleteFromTail` method is similar, but the `tail` of the list is assigned to the node pointed to by the `prev` pointer of the current tail node. Then, the `next` pointer of the new tail node is set to `null`.

```javascript
deleteFromTail() {
  this.tail = this.tail.prev;
  this.tail.next = null;
}
```

## Searching the List

We can search the list for a particular piece of data using the `search` method. This method takes a `data` parameter and returns the node that contains that data. If the data is not found, the method returns `null`.

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

## Traversing the List

We can traverse the list using the `traverse` method. This method takes a `callback` function which is called on each node in the list.

```javascript
traverse(callback) {
  let current = this.head;

  while (current) {
    callback(current);
    current = current.next;
  }
}
```

## Reversing the List

We can reverse the list using the `reverse` method. This method simply swaps the `next` and `prev` pointers of each node in the list.

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

## Conclusion

In this post, we've seen how to create and use a double linked list. This data structure can be useful when we need to be able to move backwards and forwards through the data.