---
title: [JavaScript] 012: Queue
description: 
published: true
date: 2023-02-09T14:32:53.560Z
tags: 
editor: markdown
dateCreated: 2023-02-09T14:32:47.402Z
---

- [[JavaScript] 012: Cola***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-012-queue)
{.links-list}
- [[JavaScript] 012：队列***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-012-queue)
{.links-list}
- [[JavaScript] 012: 대기열***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-012-queue)
{.links-list}


# JavaScript 012: Queue

A queue is a data structure that stores items in a First-In-First-Out (FIFO) manner. That is, the first item added to the queue will be the first item removed from the queue. A queue is sometimes called a First-In-First-Out (FIFO) list.

A common analogy to a queue is a line at a bank. The first person in line is the first person to be served and the last person in line is the last person to be served.

A queue has two main operations: enqueue and dequeue. Enqueue adds an item to the back of the queue and dequeue removes an item from the front of the queue.

## Implementation

There are many ways to implement a queue. The most common way is to use an array.

### Array Implementation

The simplest way to implement a queue is to use an array. The first element in the array is the front of the queue and the last element in the array is the back of the queue.

#### Enqueue

To enqueue an item, we add the item to the end of the array.

```javascript
function enqueue(item) {
  queue.push(item);
}
```

#### Dequeue

To dequeue an item, we remove the first item in the array.

```javascript
function dequeue() {
  return queue.shift();
}
```

### Linked List Implementation

A more efficient way to implement a queue is to use a linked list. With a linked list, we can avoid the expensive operation of shifting all of the elements in the array when we dequeue an item.

#### Enqueue

To enqueue an item, we add the item to the end of the linked list.

```javascript
function enqueue(item) {
  var node = {
    data: item,
    next: null
  };

  if (queue.length === 0) {
    queue.head = node;
  } else {
    queue.tail.next = node;
  }

  queue.tail = node;
}
```

#### Dequeue

To dequeue an item, we remove the first item in the linked list.

```javascript
function dequeue() {
  var node = queue.head;

  if (queue.length === 1) {
    queue.tail = null;
  }

  queue.head = node.next;
  queue.length--;

  return node.data;
}
```

## Time Complexity

The time complexity of both the array and linked list implementations of a queue is O(1). That is, both enqueue and dequeue are constant time operations.

## Examples

Here are some examples of using a queue.

### Example 1: Queue of Numbers

In this example, we'll create a queue of numbers. We'll enqueue the numbers 0 through 9 in order. Then we'll dequeue and print each number until the queue is empty.

```javascript
var queue = [];

for (var i = 0; i < 10; i++) {
  enqueue(i);
}

while (queue.length > 0) {
  console.log(dequeue());
}
```

Running the above code will print the numbers 0 through 9 in order.

### Example 2: Simulating a Printer Queue

In this example, we'll simulate a printer queue. We'll have a queue of print jobs and each job will have a priority. The job with the highest priority will be dequeued first.

```javascript
var queue = [];

function enqueue(item, priority) {
  var node = {
    data: item,
    priority: priority,
    next: null
  };

  if (queue.length === 0) {
    queue.head = node;
  } else {
    var current = queue.head;
    var previous;

    while (current && current.priority >= node.priority) {
      previous = current;
      current = current.next;
    }

    if (!previous) {
      node.next = queue.head;
      queue.head = node;
    } else {
      node.next = current;
      previous.next = node;
    }
  }

  queue.length++;
}

function dequeue() {
  var node = queue.head;
  queue.head = node.next;
  queue.length--;
  return node.data;
}

enqueue('A', 1);
enqueue('B', 2);
enqueue('C', 3);
enqueue('D', 4);
enqueue('E', 5);

console.log(dequeue()); // A
console.log(dequeue()); // B
console.log(dequeue()); // C
console.log(dequeue()); // D
console.log(dequeue()); // E
```

Running the above code will print the letters A through E in order.