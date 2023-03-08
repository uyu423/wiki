---
title: [C Language] 018: Skip List
description: 
published: true
date: 2023-02-13T02:32:40.273Z
tags: 
editor: markdown
dateCreated: 2023-02-13T02:32:38.549Z
---

- [[Idioma C] 018: Lista de omisión***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-018-skip-list)
{.links-list}
- [[C语言]018：跳表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-018-skip-list)
{.links-list}
- [[C언어] 018: 건너뛰기 목록***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-018-skip-list)
{.links-list}


# Skip List

A skip list is a data structure that allows for efficient search within an ordered sequence of elements. Skip lists were first described by Pugh in 1990, and they have been found to be very useful in a variety of applications.

A skip list is a linked list with an additional level of pointers. The skip list is constructed such that each node has a pointer to the next node at the same level as well as a pointer to the next node at the level below. 

The number of levels is chosen so that the probability of finding an element is high. The height of the skip list is chosen so that the expected number of steps to find an element is logarithmic in the number of elements in the list.

The following is an example of a skip list with six elements:

![](https://github.com/BryanBo-Chen/Algorithm-Data-Structure-notes/blob/master/assets/skiplist.png)

## Operations

The skip list supports the following operations:

- Search for an element with a given key.
- Insert an element with a given key.
- Delete an element with a given key.

The time complexity of these operations is as follows:

- Search: O(log n)
- Insert: O(log n)
- Delete: O(log n)

where n is the number of elements in the skip list.

## Implementation

A skip list can be implemented using a linked list. Each node in the skip list contains a key and pointers to the next node at the same level and the next node at the level below. 

The following is an example implementation of a skip list in C:

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

## Exercises

1. Implement the operations of a skip list.

2. Modify the insert and delete operations so that they return the head of the skip list.

3. Modify the search operation so that it returns the node with the largest key less than or equal to the given key.

4. Modify the insert and delete operations so that they take a node **pointer** as an argument and insert or delete the node from the skip list.

5. Implement the operations of a skip list using a doubly linked list.