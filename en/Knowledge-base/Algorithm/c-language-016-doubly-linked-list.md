---
title: [C Language] 016: Doubly Linked List
description: 
published: true
date: 2023-02-11T21:18:21.399Z
tags: 
editor: markdown
dateCreated: 2023-02-11T21:18:14.576Z
---

- [[Lenguaje C] 016: Lista doblemente enlazada***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-016-doubly-linked-list)
{.links-list}
- [[C语言]016：双向链表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-016-doubly-linked-list)
{.links-list}
- [[C언어] 016: 이중 연결 리스트***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-016-doubly-linked-list)
{.links-list}


# Doubly Linked List

A doubly linked list is a type of linked list in which each node is connected to two other nodes instead of just one. This allows for bidirectional traversal of the list.

## Concept

A doubly linked list is a data structure that consists of a set of nodes that are interconnected by links. Each node contains two fields:

-   A **data** field that stores the information associated with the node.
-   A **next** field that stores a reference to the next node in the list.
-   A **prev** field that stores a reference to the previous node in the list.

The first and last nodes of a doubly linked list are called the **head** and **tail** nodes, respectively. The head node is the first node in the list, and the tail node is the last node in the list.

The **next** field of the tail node contains a reference to the head node, and the **prev** field of the head node contains a reference to the tail node. This allows for bidirectional traversal of the list.

## Code Example

Here is an example of a doubly linked list in the C programming language:

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

## Exercises

1.  Implement a doubly linked list in the C programming language.

2.  Implement the following operations on a doubly linked list:

-   Insert a node at the head of the list.
-   Insert a node at the tail of the list.
-   Delete a node from the list.
-   Search for a node in the list.
-   Reverse the order of the list.

3.  Write a program that uses a doubly linked list to store a list of integers. The program should allow the user to perform the following operations:

-   Insert a new integer at the head of the list.
-   Insert a new integer at the tail of the list.
-   Delete an integer from the list.
-   Search for an integer in the list.
-   Print the contents of the list.

4.  Write a program that uses a doubly linked list to store a list of strings. The program should allow the user to perform the following operations:

-   Insert a new string at the head of the list.
-   Insert a new string at the tail of the list.
-   Delete a string from the list.
-   Search for a string in the list.
-   Print the contents of the list.

## Answers

1.  The following is a C implementation of a doubly linked list:

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

2.  The following is a C implementation of the operations on a doubly linked list:

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

3.  The following is a C implementation of a program that uses a doubly linked list to store a list of integers:

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

4.  The following is a C implementation of a program that uses a doubly linked list to store a list of strings:

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