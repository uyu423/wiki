---
title: [JavaScript] 011：堆栈
description: 
published: true
date: 2023-02-09T13:32:30.645Z
tags: 
editor: markdown
dateCreated: 2023-02-09T13:32:29.052Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 011: Stack***English** document is available*](/en/Knowledge-base/Algorithm/javascript-011-stack)
{.links-list}


# JavaScript 011：堆栈

堆栈是一种数据结构，可让您以有序的方式存储数据。你可以把它想象成一堆书，你只能从书堆的顶部添加或删除书。

堆栈通常用于计算机编程以按特定顺序存储数据。例如，当您编写需要跟踪最后调用的函数的程序时，您将使用堆栈。

可以在堆栈上执行两个主要操作：

- **Push**：这会将一个元素添加到堆栈的顶部。
- **Pop**：从栈顶移除元素。

让我们看一个例子来了解这些操作是如何工作的。

假设我们有一堆整数。我们可以按顺序将数字 1、2 和 3 压入堆栈。堆栈现在看起来像这样：

3个
2个
1个

如果我们然后弹出堆栈，则 3 将从顶部移除，堆栈现在看起来像这样：

2个
1个

如果我们将 4 压入堆栈，它看起来像这样：

4个
2个
1个

如果我们再次弹出堆栈，4 将被删除，堆栈将如下所示：

2个
1个

如您所见，堆栈始终以特定顺序保存数据。最后添加的元素总是第一个被删除的。

堆栈有很多应用。一个例子是当您为一种编程语言编写编译器时。编译器需要跟踪调用了哪个函数，以便生成正确的代码。为此，它使用堆栈。

另一个例子是当你正在编写一个网络浏览器时。当您单击链接时，浏览器需要跟踪您所在的页面，以便在您单击后退按钮时可以返回到该页面。为此，它使用堆栈。

栈也用在很多算法中，例如深度优先搜索。

## 执行

有很多方法可以实现堆栈。一种方法是使用数组。

我们可以通过将元素添加到数组末尾来将其压入堆栈。我们可以通过从数组末尾删除元素来从堆栈中弹出一个元素。

下面是一些使用数组实现堆栈的代码：

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

另一种实现堆栈的方法是使用链表。

我们可以通过将元素添加到链表的头部来将其压入堆栈。我们可以通过从链表头部移除元素来从堆栈中弹出一个元素。

下面是一些使用链表实现堆栈的代码：

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

## 时间复杂度

push 和 pop 操作的时间复杂度是 O(1)。

## 空间复杂度

push 和 pop 操作的空间复杂度是 O(1)。