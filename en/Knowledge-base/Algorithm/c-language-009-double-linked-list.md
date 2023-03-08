---
title: [C Language] 009: Double Linked List
description: 
published: true
date: 2023-02-12T20:33:41.703Z
tags: 
editor: markdown
dateCreated: 2023-02-12T20:33:39.909Z
---

- [[Lenguaje C] 009: Lista de enlaces dobles***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-009-double-linked-list)
{.links-list}
- [[C语言]009：双链表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-009-double-linked-list)
{.links-list}
- [[C언어] 009: 이중 연결 리스트***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-009-double-linked-list)
{.links-list}


#C Language 009: Double Linked List

A double linked list is a data structure that consists of a set of nodes connected together in a linear fashion. Each node contains two fields, called links, that point to the previous and next nodes in the list. The first node, called the head, points to the last node, called the tail.

A double linked list can be traversed in both directions, from head to tail and from tail to head. It is also possible to insert and delete nodes at any point in the list.

The following code example shows how to create a double linked list in C:

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head; // global variable - pointer to the head node.

// Create a new node and return its address.
struct node* getnode() {
    struct node* newnode = (struct node*)malloc(sizeof(struct node));
    newnode->data = 0;
    newnode->next = NULL;
    newnode->prev = NULL;
    return newnode;
}

// Insert a new node at the head of the list.
void insert_at_head(int x) {
    struct node* newnode = getnode();
    newnode->data = x;
    newnode->next = head;
    if(head != NULL)
        head->prev = newnode;
    head = newnode;
}

// Insert a new node at the tail of the list.
void insert_at_tail(int x) {
    struct node* newnode = getnode();
    newnode->data = x;
    newnode->next = NULL;
    if(head == NULL) {
        newnode->prev = NULL;
        head = newnode;
        return;
    }
    struct node* temp = head;
    while(temp->next != NULL)
        temp = temp->next;
    temp->next = newnode;
    newnode->prev = temp;
}

// Traverse the list from head to tail and print the data of each node.
void print_from_head() {
    struct node* temp = head;
    printf("\nPrinting from head:\n");
    while(temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}

// Traverse the list from tail to head and print the data of each node.
void print_from_tail() {
    struct node* temp = head;
    if(temp == NULL) return; // empty list
    // go to the last node
    while(temp->next != NULL)
        temp = temp->next;
    // print from tail
    printf("\nPrinting from tail:\n");
    while(temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->prev;
    }
    printf("\n");
}

// Delete the first node of the list.
void delete_at_head() {
    if(head == NULL) return; // empty list
    struct node* temp = head;
    head = head->next; // head now points to the second node
    if(head != NULL)
        head->prev = NULL;
    free(temp); // free the memory of the first node
}

// Delete the last node of the list.
void delete_at_tail() {
    if(head == NULL) return; // empty list
    struct node* temp = head;
    if(temp->next == NULL) { // only one node in the list
        free(temp);
        head = NULL;
        return;
    }
    // go to the last node
    while(temp->next != NULL)
        temp = temp->next;
    // the second last node now points to NULL
    temp->prev->next = NULL;
    free(temp); // free the memory of the last node
}

int main() {
    head = NULL; // empty list
    insert_at_head(2);
    insert_at_head(1);
    insert_at_tail(3);
    insert_at_tail(4);
    print_from_head();
    print_from_tail();
    delete_at_head();
    delete_at_tail();
    print_from_head();
    return 0;
}
```

The output of the above program is:

```
Printing from head:
1 2 3 4 

Printing from tail:
4 3 2 1 

Printing from head:
2 3 
```

As you can see, the double linked list allows us to insert and delete nodes at any point in the list. We can also traverse the list in both directions.

There are many applications of double linked lists. For example, they can be used to implement queues and stacks.

## Exercises

1. Implement a function to delete a node at a given position in a double linked list.

2. Implement a function to reverse a double linked list.

3. Implement a function to check if a given singly linked list is a palindrome or not.

4. Implement a function to delete all duplicate nodes from a sorted double linked list.

5. Implement a function to delete all duplicate nodes from an unsorted double linked list.

6. Implement a function to find the middle node of a double linked list.

7. Implement a function to count the number of times a given int occurs in a double linked list.

8. Implement a function to insert a node into a sorted double linked list.

9. Implement a function to remove all occurrences of a given int from a double linked list.

10. Implement a function to split a doubly linked list into two halves.

## Answers

1. 

```c
void delete_at_position(int position) {
    if(head == NULL) return; // empty list
    if(position == 1) { // first node
        delete_at_head();
        return;
    }
    int i;
    struct node* temp = head;
    for(i=1; i<position-1 && temp!=NULL; i++)
        temp = temp->next;
    if(temp == NULL || temp->next == NULL) return; // position does not exist
    // temp->next is the node to be deleted
    struct node* next = temp->next->next;
    free(temp->next); // free the memory of the node to be deleted
    temp->next = next;
    if(next != NULL)
        next->prev = temp;
}
```

2. 

```c
void reverse() {
    if(head == NULL) return; // empty list
    struct node* temp = head;
    struct node* next;
    while(temp != NULL) {
        next = temp->next;
        temp->next = temp->prev;
        temp->prev = next;
        head = temp;
        temp = next;
    }
}
```

3. 

```c
// Return 1 if the list is a palindrome, 0 otherwise.
int is_palindrome(struct node* head) {
    if(head == NULL) return 1; // empty list is a palindrome
    struct node* slow = head;
    struct node* fast = head;
    // use slow and fast pointers to find the middle of the list
    while(fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }
    // slow is now pointing to the middle node
    // reverse the second half of the list
    struct node* second_half = NULL;
    struct node* temp = NULL;
    while(slow != NULL) {
        temp = slow->next;
        slow->next = second_half;
        second_half = slow;
        slow = temp;
    }
    // head and second_half now point to the first and second halves of the list
    // compare the two halves for equality
    while(second_half != NULL) {
        if(head->data != second_half->data)
            return 0; // not a palindrome
        head = head->next;
        second_half = second_half->next;
    }
    return 1; // list is a palindrome
}
```

4. 

```c
// Delete all duplicate nodes from a sorted list.
void delete_duplicates(struct node* head) {
    if(head == NULL) return; // empty list
    struct node* temp = head;
    // compare each node with its next node
    while(temp->next != NULL) {
        if(temp->data == temp->next->data) {
            // duplicate node found, delete it
            struct node* next = temp->next->next;
            free(temp->next); // free the memory of the duplicate node
            temp->next = next;
            if(next != NULL)
                next->prev = temp;
        }
        else {
            temp = temp->next;
        }
    }
}
```

5. 

```c
// Delete all duplicate nodes from an unsorted list.
void delete_duplicates(struct node* head) {
    if(head == NULL) return; // empty list
    struct node* temp1 = head;
    // compare each node with every other node in the list
    while(temp1->next != NULL) {
        struct node* temp2 = temp1->next;
        while(temp2 != NULL) {
            if(temp1->data == temp2->data) {
                // duplicate node found, delete it
                struct node* next = temp2->next;
                free(temp2); // free the memory of the duplicate node
                temp2 = next;
                if(next != NULL)
                    next->prev = temp1;
            }
            else {
                temp2 = temp2->next;
            }
        }
        temp1 = temp1->next;
    }
}
```

6. 

```c
// Return the address of the middle node of the list.
struct node* find_middle() {
    if(head == NULL) return NULL; // empty list
    struct node* slow = head;
    struct node* fast = head;
    // use slow and fast pointers to find the middle of the list
    while(fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }
    // slow is now pointing to the middle node
    return slow;
}
```

7. 

```c
// Return the number of times x occurs in the list.
int count(int x) {
    if(head == NULL) return 0; // empty list
    int count = 0;
    struct node* temp = head;
    while(temp != NULL) {
        if(temp->data == x)
            count++;
        temp = temp->next;
    }
    return count;
}
```

8. 

```c
// Insert a new node with data x in a sorted list.
void insert(int x) {
    if(head == NULL) { // empty list
        insert_at_head(x);
        return;
    }
    struct node* temp = head;
    struct node* prev = NULL;
    // find the position to insert the new node
    while(temp != NULL && temp->data < x) {
        prev = temp;
        temp = temp->next;
    }
    // temp is now pointing to the node after the insertion position
    // prev is pointing to the node before the insertion position
    if(prev == NULL) { // insert at the head
        insert_at_head(x);
    }
    else {
        // insert the new node between prev and temp
        struct node* newnode = getnode();
        newnode->data = x;
        newnode->next = temp;
        newnode->prev = prev;
        prev->next = newnode;
        if(temp != NULL)
            temp->prev = newnode;
    }
}
```

9. 

```c
// Remove all occurrences of x from the list.
void remove(int x) {
    if(head == NULL) return; // empty list
    struct node* temp = head;
    // compare each node with x
    while(temp != NULL) {
        if(temp->data == x) {
            // node to be removed
            if(temp == head) { // head node
                delete_at_head();
            }
            else {
                struct node* prev = temp->prev;
                struct node* next = temp->next;
                prev->next = next;
                if(next != NULL)
                    next->prev = prev;
                free(temp); // free the memory of the node to be removed
            }
        }
        temp = temp->next;
    }
}
```

10. 

```c
// Split the list into two halves.
// Return the address of the second half of the list.
struct node* split() {
    if(head == NULL) return NULL; // empty list
    struct node* slow = head;
    struct node* fast = head;
    // use slow and fast pointers to find the middle of the list
    while(fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }
    // slow is now pointing to the middle node
    // the second half of the list starts from slow->next
    struct node* second_half = slow->next;
    if(second_half != NULL)
        second_half->prev = NULL;
    slow->next = NULL; // first half of the list ends at slow
    return second_half;
}
```