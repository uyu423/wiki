---
title: [JavaScript] 011: Stack
description: 
published: true
date: 2023-02-09T13:32:35.505Z
tags: 
editor: markdown
dateCreated: 2023-02-09T13:32:29.060Z
---

- [[JavaScript] 011: Pila***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-011-stack)
{.links-list}
- [[JavaScript] 011：堆栈***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-011-stack)
{.links-list}
- [[JavaScript] 011: 스택***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-011-stack)
{.links-list}


# JavaScript 011: Stack

A stack is a data structure that allows you to store data in an ordered way. You can think of it like a stack of books, where you can only add or remove books from the top of the stack.

Stacks are often used in computer programming to store data in a particular order. For example, when you are writing a program that needs to keep track of what function was called last, you would use a stack.

There are two main operations that can be performed on a stack:

- **Push**: This adds an element to the top of the stack.
- **Pop**: This removes the element from the top of the stack.

Let's look at an example to see how these operations work.

Suppose we have a stack of integers. We can push the numbers 1, 2, and 3 onto the stack in that order. The stack would now look like this:

3
2
1

If we then pop the stack, the 3 would be removed from the top, and the stack would now look like this:

2
1

If we push 4 onto the stack, it would look like this:

4
2
1

And if we pop the stack again, the 4 would be removed and the stack would look like this:

2
1

As you can see, the stack always keeps the data in a particular order. The element that is added last is always the first one to be removed.

There are many applications of stacks. One example is when you are writing a compiler for a programming language. The compiler needs to keep track of which function is being called so that it can generate the correct code. To do this, it uses a stack.

Another example is when you are writing a web browser. When you click on a link, the browser needs to keep track of which page you were on so that it can go back to it when you click the back button. To do this, it uses a stack.

Stacks are also used in many algorithms, such as depth-first search.

## Implementation

There are many ways to implement a stack. One way is to use an array.

We can push an element onto the stack by adding it to the end of the array. We can pop an element from the stack by removing the element from the end of the array.

Here is some code that implements a stack using an array:

```javascript
class Stack {
  constructor() {
    this.data = [];
  }

  push(element) {
    this.data.push(element);
  }

  pop() {
    return this.data.pop();
  }
}
```

Another way to implement a stack is to use a linked list.

We can push an element onto the stack by adding it to the head of the linked list. We can pop an element from the stack by removing the element from the head of the linked list.

Here is some code that implements a stack using a linked list:

```javascript
class Stack {
  constructor() {
    this.head = null;
  }

  push(element) {
    const node = {
      data: element,
      next: this.head
    };
    this.head = node;
  }

  pop() {
    const node = this.head;
    this.head = node.next;
    return node.data;
  }
}
```

## Time Complexity

The time complexity of the push and pop operations is O(1).

## Space Complexity

The space complexity of the push and pop operations is O(1).