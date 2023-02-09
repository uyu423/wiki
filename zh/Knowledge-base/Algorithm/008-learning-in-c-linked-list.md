---
title: 008：学习C语言：链表
description: 
published: true
date: 2023-02-09T03:26:06.881Z
tags: 
editor: markdown
dateCreated: 2023-02-09T03:26:06.881Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [008: Learning in C: Linked List***English** document is available*](/en/Knowledge-base/Algorithm/008-learning-in-c-linked-list)
{.links-list}


# 008：学习 C：链表

欢迎来到我关于学习算法和数据结构的博客系列！在这篇文章中，我们将介绍 C 编程语言中的链表。

链表是一种存储元素序列的数据结构。链表中的每个元素称为节点。

节点通过链接连接在一起。链表中的第一个节点称为头节点。链表中的最后一个节点称为尾节点。

下面是一个有四个节点的链表的例子：

![具有四个节点的链表的图像](https://i.imgur.com/fTXdiLN.png)

链表中的每个节点都有两部分：

- 数据部分存储实际数据。
- 链接部分存储到列表中下一个节点的链接。

第一个节点（头节点）具有到第二个节点的链接。第二个节点有到第三个节点的链接。第三个节点有到第四个节点的链接。第四个节点（尾节点）有一个指向 NULL 的链接。

NULL 是一个特殊值，表示列表的结尾。

以下是如何创建链表的示例：

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *link;
};

int main() {
    struct node *head;
    struct node *second;
    struct node *third;
    
    head = (struct node*)malloc(sizeof(struct node)); 
    second = (struct node*)malloc(sizeof(struct node));
    third = (struct node*)malloc(sizeof(struct node));
    
    head->data = 1; 
    head->link = second; 
    
    second->data = 2; 
    second->link = third; 
    
    third->data = 3; 
    third->link = NULL;
    
    return 0;
}
```

在上面的例子中，我们创建了三个节点。我们已经将第二个节点的地址存储在头节点的链接部分。我们在第二个节点的链接部分存储了第三个节点的地址。我们在第三个节点的链接部分存储了 NULL，因为第三个节点是列表中的最后一个节点。

我们还在每个节点的数据部分存储了数据。数据部分可以存储任何类型的数据（整数、浮点数、字符等）。

要访问链表中的数据，我们需要遍历链表。遍历链表意味着访问列表中的每个节点。

我们可以使用循环遍历链表。循环将继续，直到当前节点为 NULL。

下面是一个如何遍历链表的例子：

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *link;
};

int main() {
    struct node *head;
    struct node *second;
    struct node *third;
    
    head = (struct node*)malloc(sizeof(struct node)); 
    second = (struct node*)malloc(sizeof(struct node));
    third = (struct node*)malloc(sizeof(struct node));
    
    head->data = 1; 
    head->link = second; 
    
    second->data = 2; 
    second->link = third; 
    
    third->data = 3; 
    third->link = NULL;
    
    struct node *current;
    current = head;
    
    while (current != NULL) {
        printf("%d\n", current->data);
        current = current->link;
    }
    
    return 0;
}
```

在上面的示例中，我们创建了一个包含三个节点的链表。我们已将头节点的地址存储在名为 current 的结构节点指针中。

我们已经创建了一个 while 循环，它将一直持续到当前节点为 NULL。在 while 循环中，我们正在打印当前节点的数据部分。然后，我们将下一个节点的地址分配给当前节点。

这将导致循环访问列表中的每个节点并打印每个节点的数据部分。

输出：

```
1
2
3
```

要在链表中插入新节点，我们需要找到要插入新节点的位置。

假设我们想在列表的开头插入一个新节点。为此，我们需要更改头指针以指向新节点。

以下是如何在链表开头插入新节点的示例：

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *link;
};

int main() {
    struct node *head;
    struct node *second;
    struct node *third;
    
    head = (struct node*)malloc(sizeof(struct node)); 
    second = (struct node*)malloc(sizeof(struct node));
    third = (struct node*)malloc(sizeof(struct node));
    
    head->data = 1; 
    head->link = second; 
    
    second->data = 2; 
    second->link = third; 
    
    third->data = 3; 
    third->link = NULL;
    
    struct node *new_node;
    new_node = (struct node*)malloc(sizeof(struct node));
    
    new_node->data = 0;
    new_node->link = head;
    
    head = new_node;
    
    struct node *current;
    current = head;
    
    while (current != NULL) {
        printf("%d\n", current->data);
        current = current->link;
    }
    
    return 0;
}
```

在上面的示例中，我们创建了一个包含三个节点的链表。我们还创建了一个新节点。我们已将新节点的地址存储在头指针中。

输出：

```
0
1
2
3
```

假设我们想在列表的末尾插入一个新节点。为此，我们需要将尾节点的链接部分更改为指向新节点。

以下是如何在链表末尾插入新节点的示例：

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *link;
};

int main() {
    struct node *head;
    struct node *second;
    struct node *third;
    
    head = (struct node*)malloc(sizeof(struct node)); 
    second = (struct node*)malloc(sizeof(struct node));
    third = (struct node*)malloc(sizeof(struct node));
    
    head->data = 1; 
    head->link = second; 
    
    second->data = 2; 
    second->link = third; 
    
    third->data = 3; 
    third->link = NULL;
    
    struct node *new_node;
    new_node = (struct node*)malloc(sizeof(struct node));
    
    new_node->data = 4;
    new_node->link = NULL;
    
    third->link = new_node;
    
    struct node *current;
    current = head;
    
    while (current != NULL) {
        printf("%d\n", current->data);
        current = current->link;
    }
    
    return 0;
}
```

在上面的示例中，我们创建了一个包含三个节点的链表。我们还创建了一个新节点。我们在第三个节点的链接部分存储了新节点的地址。

输出：

```
1
2
3
4
```

假设我们要在第二个节点之后插入一个新节点。为此，我们需要将第二个节点的链接部分更改为指向新节点。我们还需要将新节点的链接部分更改为指向第三个节点。

以下是如何在第二个节点之后插入新节点的示例：

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *link;
};

int main() {
    struct node *head;
    struct node *second;
    struct node *third;
    
    head = (struct node*)malloc(sizeof(struct node)); 
    second = (struct node*)malloc(sizeof(struct node));
    third = (struct node*)malloc(sizeof(struct node));
    
    head->data = 1; 
    head->link = second; 
    
    second->data = 2; 
    second->link = third; 
    
    third->data = 3; 
    third->link = NULL;
    
    struct node *new_node;
    new_node = (struct node*)malloc(sizeof(struct node));
    
    new_node->data = 4;
    new_node->link = third;
    
    second->link = new_node;
    
    struct node *current;
    current = head;
    
    while (current != NULL) {
        printf("%d\n", current->data);
        current = current->link;
    }
    
    return 0;
}
```

在上面的示例中，我们创建了一个包含三个节点的链表。我们还创建了一个新节点。我们已经将新节点的地址存储在第二个节点的链接部分。我们还在新节点的链接部分存储了第三个节点的地址。

输出：

```
1
2
4
3
```

要从链表中删除节点，我们需要找到要删除的节点的位置。

假设我们要从列表中删除第一个节点（头节点）。为此，我们需要将头指针更改为指向第二个节点。

以下是如何从链表中删除第一个节点的示例：

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *link;
};

int main() {
    struct node *head;
    struct node *second;
    struct node *third;
    
    head = (struct node*)malloc(sizeof(struct node)); 
    second = (struct node*)malloc(sizeof(struct node));
    third = (struct node*)malloc(sizeof(struct node));
    
    head->data = 1; 
    head->link = second; 
    
    second->data = 2; 
    second->link = third; 
    
    third->data = 3; 
    third->link = NULL;
    
    head = head->link;
    
    struct node *current;
    current = head;
    
    while (current != NULL) {
        printf("%d\n", current->data);
        current = current->link;
    }
    
    return 0;
}
```

在上面的示例中，我们创建了一个包含三个节点的链表。我们还从列表中删除了第一个节点。我们通过将头指针更改为指向第二个节点来完成此操作。

输出：

```
2
3
```

假设我们要从列表中删除最后一个节点。为此，我们需要找到最后一个节点之前的节点地址。我们还需要将最后一个节点之前的节点的链接部分更改为指向NULL。

以下是如何从链表中删除最后一个节点的示例：

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *link;
};

int main() {
    struct node *head;
    struct node *second;
    struct node *third;
    
    head = (struct node*)malloc(sizeof(struct node)); 
    second = (struct node*)malloc(sizeof(struct node));
    third = (struct node*)malloc(sizeof(struct node));
    
    head->data = 1; 
    head->link = second; 
    
    second->data = 2; 
    second->link = third; 
    
    third->data = 3; 
    third->link = NULL;
    
    second->link = NULL;
    
    struct node *current;
    current = head;
    
    while (current != NULL) {
        printf("%d\n", current->data);
        current = current->link;
    }
    
    return 0;
}
```

在上面的示例中，我们创建了一个包含三个节点的链表。我们还从列表中删除了最后一个节点。我们通过将第二个节点的链接部分更改为 NULL 来完成此操作。

输出：

```
1
2
```

假设我们要删除第一个节点之后的节点。为此，我们需要找到第一个节点之后的节点地址。我们还需要将第一个节点的链接部分更改为指向第一个节点之后的节点之后的节点。

以下是如何删除第一个节点之后的节点的示例：

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *link;
};

int main() {
    struct node *head;
    struct node *second;
    struct node *third;
    
    head = (struct node*)malloc(sizeof(struct node)); 
    second = (struct node*)malloc(sizeof(struct node));
    third = (struct node*)malloc(sizeof(struct node));
    
    head->data = 1; 
    head->link = second; 
    
    second->data = 2; 
    second->link = third; 
    
    third->data = 3; 
    third->link = NULL;
    
    head->link = third;
    
    struct node *current;
    current = head;
    
    while (current != NULL) {
        printf("%d\n", current->data);
        current = current->link;
    }
    
    return 0;
}
```

在上面的示例中，我们创建了一个包含三个节点的链表。我们还删除了第一个节点之后的节点。我们通过将第一个节点的链接部分更改为指向第三个节点来完成此操作。

输出：

```
1
3
```

这就是这篇文章的全部内容！我希望你发现它有帮助。在下一篇文章中，我们将介绍 C 编程语言中的堆栈。