---
title: 【C语言】011：堆栈
description: 
published: true
date: 2023-02-09T09:55:46.138Z
tags: 
editor: markdown
dateCreated: 2023-02-09T09:55:39.782Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 011: Stack***English** document is available*](/en/Knowledge-base/Algorithm/c-language-011-stack)
{.links-list}


# 堆

栈是一种基本的数据结构，在逻辑上可以被认为是一个线性结构，由一个真实的物理栈或堆表示，这是一种对象堆叠在一起的结构。栈的基本原理是栈中最后插入的元素将最先被移除。

堆栈是一种受限的数据结构，因为它具有执行操作的预定义顺序。订单仅限于 LIFO（后进先出）。

有许多真实世界的堆栈示例。几个例子如下：

- 一副纸牌
- 一盘食物
- 一堆书

## 执行

堆栈可以使用数组或链表来实现。在这篇文章中，我们将讨论使用数组实现堆栈。

### 数组实现

栈的数组实现非常简单。我们只需要维护一个变量来跟踪堆栈的顶部元素。栈顶元素是最后加入栈的元素。

可以对栈执行以下操作：

- Push：此操作将一个元素添加到堆栈的顶部。
- Pop：这个操作从栈顶移除一个元素。
- Peek：此操作返回堆栈顶部的元素而不删除它。
- isEmpty：如果堆栈为空，则此操作返回 true，否则返回 false。

下面是C语言中使用数组实现栈的实现：

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

输出：

```
3 popped from stack
Top element is 2
```

在上面的程序中，我们创建了一个大小为 MAXSIZE=10 的堆栈。 top 变量存储栈顶元素的索引。 push 操作将一个元素添加到栈顶，pop 操作从栈顶移除一个元素。 peek 操作返回堆栈顶部的元素而不删除它。如果堆栈为空，则 isEmpty 操作返回 true，否则返回 false。

## 应用

堆栈在计算机科学中有许多应用。栈的一些应用如下：

- 解析：堆栈用于解析。例如，当给出诸如“3 + ((5*9) + 2)”这样的算术表达式时，可以使用堆栈对其进行解析。
- 回溯：堆栈用于回溯。例如，当给定一个迷宫时，我们可以使用堆栈来跟踪路径并在到达死胡同时回溯。
- 文本编辑器中的撤消操作：堆栈用于在文本编辑器中实现撤消操作。例如，当我们键入一个字符时，它会被压入堆栈。当我们按下撤销按钮时，栈顶的字符被弹出。
- 表达式评估和转换：堆栈用于评估中缀表示法中的表达式和转换为后缀表示法。