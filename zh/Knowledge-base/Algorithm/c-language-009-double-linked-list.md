---
title: [C语言]009：双链表
description: 
published: true
date: 2023-02-12T20:33:46.901Z
tags: 
editor: markdown
dateCreated: 2023-02-12T20:33:39.904Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 009: Double Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-009-double-linked-list)
{.links-list}


# C语言009：双向链表

双链表是一种数据结构，由一组以线性方式连接在一起的节点组成。每个节点包含两个字段，称为链接，指向列表中的前一个和下一个节点。第一个节点，称为头，指向最后一个节点，称为尾。

双链表可以双向遍历，从头到尾和从尾到头。也可以在列表中的任意点插入和删除节点。

下面的代码示例显示了如何在 C 中创建双向链表：

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

上述程序的输出是：

```
Printing from head:
1 2 3 4 

Printing from tail:
4 3 2 1 

Printing from head:
2 3 
```

如您所见，双链表允许我们在列表中的任意点插入和删除节点。我们也可以双向遍历列表。

双链表有很多应用。例如，它们可用于实现队列和堆栈。

## 练习

1. 实现一个函数，删除双链表中给定位置的节点。

2. 实现一个双向链表反转的函数。

3. 实现一个函数来检查给定的单向链表是否为回文。

4. 实现一个函数，从排序的双链表中删除所有重复的节点。

5. 实现一个函数，从一个未排序的双链表中删除所有重复的节点。

6. 实现一个查找双链表中间节点的函数。

7. 实现一个函数来计算给定整数在双向链表中出现的次数。

8. 实现一个函数，将节点插入到已排序的双链表中。

9. 实现一个函数，从双链表中删除所有出现的给定 int。

10. 实现一个将双向链表分成两半的函数。

## 答案

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