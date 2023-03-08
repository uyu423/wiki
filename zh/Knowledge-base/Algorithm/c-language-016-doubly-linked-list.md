---
title: [C语言]016：双向链表
description: 
published: true
date: 2023-02-11T21:18:16.205Z
tags: 
editor: markdown
dateCreated: 2023-02-11T21:18:14.571Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 016: Doubly Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-016-doubly-linked-list)
{.links-list}


# 双向链表

双向链表是一种链表，其中每个节点都连接到另外两个节点，而不仅仅是一个。这允许双向遍历列表。

## 概念

双向链表是一种数据结构，由一组通过链接互连的节点组成。每个节点包含两个字段：

- 一个 **data** 字段，用于存储与节点关联的信息。
- 一个 **next** 字段，用于存储对列表中下一个节点的引用。
- 一个 **prev** 字段，存储对列表中前一个节点的引用。

双向链表的第一个和最后一个节点分别称为**头**和**尾**节点。头节点是列表中的第一个节点，尾节点是列表中的最后一个节点。

尾节点的**next**字段包含对头节点的引用，头节点的**prev**字段包含对尾节点的引用。这允许双向遍历列表。

## 代码示例

这是 C 编程语言中双向链表的示例：

```c
struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(int data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(int data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(curr_node->data == data) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%d ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

int main() {
    insert_node(1);
    insert_node(2);
    insert_node(3);
    insert_node(4);
    insert_node(5);

    print_list();

    delete_node(3);

    print_list();

    return 0;
}
```

## 练习

1、用C语言实现一个双向链表。

2. 对双向链表执行如下操作：

- 在列表的头部插入一个节点。
- 在列表的尾部插入一个节点。
- 从列表中删除一个节点。
- 在列表中搜索节点。
- 反转列表的顺序。

3. 编写一个使用双向链表存储整数列表的程序。该程序应允许用户执行以下操作：

- 在列表的头部插入一个新的整数。
- 在列表的尾部插入一个新的整数。
- 从列表中删除一个整数。
- 在列表中搜索一个整数。
- 打印列表的内容。

4. 编写一个使用双向链表存储字符串列表的程序。该程序应允许用户执行以下操作：

- 在列表的头部插入一个新字符串。
- 在列表的尾部插入一个新字符串。
- 从列表中删除一个字符串。
- 在列表中搜索字符串。
- 打印列表的内容。

## 答案

1. 下面是一个双向链表的C实现：

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(int data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(int data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(curr_node->data == data) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%d ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

int main() {
    insert_node(1);
    insert_node(2);
    insert_node(3);
    insert_node(4);
    insert_node(5);

    print_list();

    delete_node(3);

    print_list();

    return 0;
}
```

2. 下面是双向链表操作的C实现：

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(int data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(int data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(curr_node->data == data) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%d ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

void reverse_list() {
    struct node* curr_node = head;
    struct node* temp_node = NULL;

    while(curr_node != NULL) {
        temp_node = curr_node->prev;
        curr_node->prev = curr_node->next;
        curr_node->next = temp_node;

        curr_node = curr_node->prev;
    }

    if(temp_node != NULL) {
        head = temp_node->prev;
    }
}

int main() {
    insert_node(1);
    insert_node(2);
    insert_node(3);
    insert_node(4);
    insert_node(5);

    print_list();

    delete_node(3);

    print_list();

    reverse_list();

    print_list();

    return 0;
}
```

3. 以下是使用双向链表存储整数列表的程序的 C 实现：

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(int data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(int data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(curr_node->data == data) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%d ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

int main() {
    int data;

    while(1) {
        printf("Enter an integer (Enter -1 to exit): ");
        scanf("%d", &data);

        if(data == -1) {
            break;
        }

        insert_node(data);
    }

    print_list();

    while(1) {
        printf("Enter an integer to delete (Enter -1 to exit): ");
        scanf("%d", &data);

        if(data == -1) {
            break;
        }

        delete_node(data);
    }

    print_list();

    return 0;
}
```

4. 以下是使用双向链表存储字符串列表的程序的 C 实现：

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct node {
    char data[100];
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(char* data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    strcpy(new_node->data, data);
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(char* data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(strcmp(curr_node->data, data) == 0) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%s ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

int main() {
    char data[100];

    while(1) {
        printf("Enter a string (Enter -1 to exit): ");
        scanf("%s", data);

        if(strcmp(data, "-1") == 0) {
            break;
        }

        insert_node(data);
    }

    print_list();

    while(1) {
        printf("Enter a string to delete (Enter -1 to exit): ");
        scanf("%s", data);

        if(strcmp(data, "-1") == 0) {
            break;
        }

        delete_node(data);
    }

    print_list();

    return 0;
}
```