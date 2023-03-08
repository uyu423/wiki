---
title: [C Language] 011: Stack
description: 
published: true
date: 2023-02-09T09:55:41.462Z
tags: 
editor: markdown
dateCreated: 2023-02-09T09:55:39.785Z
---

- [[Lenguaje C] 011: Pila***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-011-stack)
{.links-list}
- [【C语言】011：堆栈***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-011-stack)
{.links-list}
- [[C언어] 011: 스택***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-011-stack)
{.links-list}


# Stack

A stack is a basic data structure that can be logically thought of as a linear structure represented by a real physical stack or pile, which is a structure where the objects are piled one on top of the other. The basic principle of a stack is that the element which is inserted last in the stack will be the first one to be removed.

A stack is a restricted data structure because it has a predefined order in which the operations can be performed. The order is restricted to LIFO (Last In First Out).

There are many real world examples of stacks. A few examples are as follows:

- A deck of cards
- A plate of food
- A pile of books

## Implementation

A stack can be implemented using an array or a linked list. In this post, we will discuss the implementation of a stack using an array.

### Array Implementation

The array implementation of a stack is very simple. We just need to maintain a variable that keeps track of the top element of the stack. The top element is the element that was added to the stack last.

The following operations can be performed on a stack:

- Push: This operation adds an element to the top of the stack.
- Pop: This operation removes an element from the top of the stack.
- Peek: This operation returns the element at the top of the stack without removing it.
- isEmpty: This operation returns true if the stack is empty, false otherwise.

The following is the implementation of a stack using an array in the C programming language:

```c
#include <stdio.h>
#include <stdlib.h>
 
#define MAXSIZE 10
 
struct stack
{
    int top;
    int items[MAXSIZE];
};
 
struct stack* createStack()
{
    struct stack* s = (struct stack*) malloc(sizeof(struct stack));
    s->top = -1;
    return s;
}
 
int isEmpty(struct stack* s)
{
    return (s->top == -1);
}
 
int peek(struct stack* s)
{
    if (!isEmpty(s))
        return s->items[s->top];
    return -1;
}
 
void push(struct stack* s, int x)
{
    if (s->top == MAXSIZE-1)
    {
        printf("Stack overflow\n");
        return;
    }
    s->items[++s->top] = x;
}
 
int pop(struct stack* s)
{
    if (isEmpty(s))
    {
        printf("Stack underflow\n");
        return -1;
    }
    return s->items[s->top--];
}
 
int main()
{
    struct stack* s = createStack();
    push(s, 1);
    push(s, 2);
    push(s, 3);
    printf("%d popped from stack\n", pop(s));
    printf("Top element is %d\n", peek(s));
    return 0;
}
```

Output:

```
3 popped from stack
Top element is 2
```

In the above program, we have created a stack of size MAXSIZE=10. The top variable stores the index of the top element of the stack. The push operation adds an element to the top of the stack and the pop operation removes an element from the top of the stack. The peek operation returns the element at the top of the stack without removing it. The isEmpty operation returns true if the stack is empty, false otherwise.

## Applications

Stacks have many applications in computer science. Some of the applications of stacks are as follows:

- Parsing: Stacks are used in parsing. For example, when an arithmetic expression such as "3 + ((5*9) + 2)" is given, it can be parsed using a stack.
- Backtracking: Stacks are used in backtracking. For example, when a maze is given, we can use a stack to keep track of the path and backtrack when we reach a dead end.
- Undo operations in text editors: Stacks are used to implement undo operations in text editors. For example, when we type a character, it is pushed onto a stack. When we press the undo button, the top character is popped from the stack.
- Expression evaluation and conversion: Stacks are used in the evaluation of expressions in infix notation and conversion to postfix notation.