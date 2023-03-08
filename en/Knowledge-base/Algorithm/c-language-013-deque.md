---
title: [C Language] 013: Deque
description: 
published: true
date: 2023-02-12T22:32:37.782Z
tags: 
editor: markdown
dateCreated: 2023-02-12T22:32:36.060Z
---

- [[Lenguaje C] 013: Deque***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-013-deque)
{.links-list}
- [【C语言】013：双端队列***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-013-deque)
{.links-list}
- [[C언어] 013: 데크***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-013-deque)
{.links-list}


# Deque

A deque, also known as a double-ended queue, is an ordered collection of items similar to a stack or a queue. Deques are a generalization of stacks and queues (the name is pronounced "deck" and is short for "double-ended queue").

Deques support adding and removing items from either end of the data structure in constant time. In contrast, queues and stacks require linear time to add or remove items.

## Implementation

A deque can be implemented as a dynamic array or a linked list.

### Dynamic Array

A dynamic array is a good choice for a deque if the maximum number of items is known in advance. The array can be resized as needed.

To implement a deque with a dynamic array, we can use a circular array. This allows us to avoid the need to shift elements when items are added or removed from the deque.

![Circular Array](https://i.imgur.com/zk0Fgdq.png)

The front and rear indices can be kept track of with two variables. The front index represents the index of the first element in the deque and the rear index represents the index of the last element in the deque.

To add an element to the front of the deque, we decrement the front index and insert the element at that index. If the front index is less than 0, we wrap around to the end of the array.

To add an element to the rear of the deque, we increment the rear index and insert the element at that index. If the rear index is equal to the size of the array, we wrap around to the beginning of the array.

To remove an element from the front of the deque, we simply remove the element at the front index. To remove an element from the rear of the deque, we remove the element at the rear index.

### Linked List

A linked list is a good choice for a deque if the maximum number of items is not known in advance.

To implement a deque with a linked list, we can use a doubly-linked list. This allows us to add and remove items from either end of the deque in constant time.

![Doubly-Linked List](https://i.imgur.com/7W5rNcu.png)

The front and rear pointers can be kept track of with two variables. The front pointer represents the first node in the deque and the rear pointer represents the last node in the deque.

To add an element to the front of the deque, we simply insert the element at the front of the list. To add an element to the rear of the deque, we insert the element at the rear of the list.

To remove an element from the front of the deque, we simply remove the element at the front of the list. To remove an element from the rear of the deque, we remove the element at the rear of the list.

## Applications

Deques have many applications. Some of the more common applications are described below.

### Queue

A queue is a data structure that allows items to be added at one end and removed from the other end. A queue is often called a first-in, first-out (FIFO) data structure.

A queue can be implemented with a deque. To add an item to the queue, we add it to the rear of the deque. To remove an item from the queue, we remove it from the front of the deque.

### Stack

A stack is a data structure that allows items to be added and removed from only one end. A stack is often called a last-in, first-out (LIFO) data structure.

A stack can be implemented with a deque. To add an item to the stack, we add it to the front of the deque. To remove an item from the stack, we remove it from the front of the deque.

### Palindrome

A palindrome is a word, phrase, or number that is the same forwards and backwards. For example, "racecar" and "1001" are palindromes.

To check if a word is a palindrome, we can use a deque. We add each character of the word to the rear of the deque. We then remove each character from the deque and compare it to the corresponding character from the front of the deque. If all of the characters match, then the word is a palindrome.

## Complexity Analysis

Deques have the following time complexities:

- Access: O(1)
- Search: O(n)
- Insertion: O(1)
- Deletion: O(1)

where n is the number of items in the deque.

Deques have the following space complexities:

- Static Array: O(n)
- Dynamic Array: O(n)
- Linked List: O(n)

where n is the maximum number of items that can be stored in the deque.