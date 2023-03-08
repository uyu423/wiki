---
title: [JavaScript] 016: Doubly Linked List
description: 
published: true
date: 2023-02-09T18:32:36.483Z
tags: 
editor: markdown
dateCreated: 2023-02-09T18:32:30.294Z
---

- [[JavaScript] 016: Lista doblemente enlazada***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-016-doubly-linked-list)
{.links-list}
- [[JavaScript] 016：双向链表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-016-doubly-linked-list)
{.links-list}
- [[JavaScript] 016: 이중 연결 목록***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-016-doubly-linked-list)
{.links-list}


# JavaScript 016: Doubly Linked List

A doubly linked list is a data structure that consists of a set of sequential nodes linked together in a manner where each node contains a reference to the previous node as well as the next node. This type of linked list is advantageous over a singly linked list because it allows for traversal in both directions.

A typical doubly linked list node contains three fields:

- **prev**: A reference to the previous node in the list
- **next**: A reference to the next node in the list
- **data**: The data stored in the node

The first node in a doubly linked list is typically referred to as the **head** node, and the last node is typically referred to as the **tail** node. The head node and tail node have special properties in that the head node's prev field is null, and the tail node's next field is null.

Here is an illustration of a doubly linked list with four nodes:

![Doubly Linked List](https://i.imgur.com/eLzWqlN.png)

And here is the code for a basic doubly linked list node in JavaScript:

```javascript
function Node(data) {
  this.prev = null;
  this.next = null;
  this.data = data;
}
```

To insert a new node into a doubly linked list, we first need to find the node that we want to insert the new node after. Once we have found that node, we can set the new node's next field to point to the node that we found, and we can set the found node's prev field to point to the new node. Finally, we can set the new node's prev field to point to the found node.

Here is an illustration of what this insertion process looks like:

![Insertion into a Doubly Linked List](https://i.imgur.com/TGiukgD.png)

And here is the code for this insertion process:

```javascript
function insertAfter(node, newNode) {
  newNode.next = node.next;
  node.next = newNode;
  newNode.prev = node;
}
```

To delete a node from a doubly linked list, we first need to find the node that we want to delete. Once we have found the node, we can set the prev field of the node's next field to point to the node's prev field, and we can set the next field of the node's prev field to point to the node's next field. Finally, we can set the node's prev field and next field to null.

Here is an illustration of what this deletion process looks like:

![Deletion from a Doubly Linked List](https://i.imgur.com/FgxLbNv.png)

And here is the code for this deletion process:

```javascript
function deleteNode(node) {
  node.prev.next = node.next;
  node.next.prev = node.prev;
  node.prev = null;
  node.next = null;
}
```

That's all there is to it! A doubly linked list is a simple yet powerful data structure that can be used in a variety of applications.