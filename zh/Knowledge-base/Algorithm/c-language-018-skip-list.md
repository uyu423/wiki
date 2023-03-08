---
title: [C语言]018：跳表
description: 
published: true
date: 2023-02-13T02:32:45.921Z
tags: 
editor: markdown
dateCreated: 2023-02-13T02:32:38.544Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 018: Skip List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-018-skip-list)
{.links-list}


# 跳过列表

跳跃列表是一种数据结构，允许在有序的元素序列中进行有效搜索。跳跃列表于 1990 年由 Pugh 首次描述，人们发现它们在各种应用中非常有用。

跳表是具有额外指针级别的链表。跳过列表的构造使得每个节点都有一个指向同一级别下一个节点的指针以及一个指向下一个级别下一个节点的指针。

选择级别数，以便找到元素的概率很高。选择跳跃列表的高度，以便查找元素的预期步数与列表中的元素数成对数。

以下是具有六个元素的跳跃列表的示例：

![](https://github.com/BryanBo-Chen/Algorithm-Data-Structure-notes/blob/master/assets/skiplist.png)

## 操作

跳过列表支持以下操作：

- 搜索具有给定键的元素。
- 插入具有给定键的元素。
- 删除具有给定键的元素。

这些操作的时间复杂度如下：

- 搜索：O(log n)
- 插入：O(log n)
- 删除：O(log n)

其中 n 是跳过列表中的元素数。

## 执行

跳表可以使用链表来实现。跳跃列表中的每个节点都包含一个键和指向同一级别的下一个节点和下一级的下一个节点的指针。

以下是 C 中跳过列表的示例实现：

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
 
typedef struct node {
    int key;
    struct node *next;
    struct node *down;
} node;
 
node *create_node(int key, node *next, node *down) {
    node *n = malloc(sizeof(node));
    n->key = key;
    n->next = next;
    n->down = down;
    return n;
}
 
node *create_skip_list(int *keys, int n, int h) {
    node *head, *tail, *curr, *down;
    int i, j;
 
    head = create_node(0, NULL, NULL);
    tail = create_node(0, NULL, NULL);
    down = head;
 
    for (i = 0; i < h; i++) {
        curr = create_node(0, tail, down);
        down->next = curr;
        down = tail;
        for (j = 0; j < n; j++) {
            curr->next = create_node(keys[j], tail, NULL);
            curr = curr->next;
        }
    }
 
    return head;
}
 
void print_skip_list(node *head) {
    node *curr;
 
    while (head != NULL) {
        curr = head;
        while (curr->next != NULL) {
            printf("%d -> ", curr->next->key);
            curr = curr->next;
        }
        printf("NULL\n");
        head = head->down;
    }
}
 
node *search(node *head, int key) {
    node *curr;
 
    while (head != NULL) {
        curr = head;
        while (curr->next != NULL && curr->next->key <= key) {
            if (curr->next->key == key) {
                return curr->next;
            }
            curr = curr->next;
        }
        head = head->down;
    }
 
    return NULL;
}
 
node *insert(node *head, int key) {
    node *curr, *down, *new_node;
    int i;
 
    curr = head;
    down = NULL;
 
    while (curr != NULL) {
        while (curr->next != NULL && curr->next->key < key) {
            curr = curr->next;
        }
 
        if (curr->next != NULL && curr->next->key == key) {
            return curr->next;
        }
 
        new_node = create_node(key, curr->next, NULL);
        curr->next = new_node;
 
        if (down != NULL) {
            down->down = new_node;
        }
 
        down = new_node;
        curr = curr->down;
    }
 
    i = 0;
 
    while (rand() % 2 == 0) {
        if (i >= head->key) {
            break;
        }
 
        new_node = create_node(0, NULL, head);
        head->down = new_node;
        head = new_node;
 
        i++;
    }
 
    head->key = i;
 
    return NULL;
}
 
node *delete(node *head, int key) {
    node *curr, *down, *tmp;
 
    curr = head;
    down = NULL;
 
    while (curr != NULL) {
        while (curr->next != NULL && curr->next->key < key) {
            curr = curr->next;
        }
 
        if (curr->next == NULL || curr->next->key > key) {
            down = curr->down;
            curr = down;
            continue;
        }
 
        tmp = curr->next;
        curr->next = curr->next->next;
        free(tmp);
 
        if (down != NULL) {
            down->down = curr;
        }
 
        down = curr;
        curr = curr->down;
    }
 
    while (head->next == NULL) {
        tmp = head;
        head = head->down;
        free(tmp);
    }
 
    return head;
}
 
int main() {
    int keys[] = {1, 2, 3, 4, 5, 6};
    int n = sizeof(keys) / sizeof(keys[0]);
    int h = 3;
 
    node *head = create_skip_list(keys, n, h);
 
    print_skip_list(head);
 
    return 0;
}
```

## 练习

1.实现跳表操作。

2. 修改插入和删除操作，使它们返回跳表的头部。

3. 修改搜索操作，使其返回具有小于或等于给定键的最大键的节点。

4. 修改插入和删除操作，使它们以节点**指针**为参数，并从跳过列表中插入或删除该节点。

5. 使用双向链表实现跳表的操作。