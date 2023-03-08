---
title: [C语言]010：循环链表
description: 
published: true
date: 2023-02-10T13:17:44.965Z
tags: 
editor: markdown
dateCreated: 2023-02-10T13:17:38.738Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 010: Circular Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-010-circular-linked-list)
{.links-list}


# 循环链表

循环链表是链表的变体，其中链表的最后一个节点指向第一个节点，形成一个循环。这种类型的列表对于需要以循环方式遍历列表的应用程序很有用，例如在游戏或操作系统调度程序中。

## 概念

循环链表是一种包含节点序列的数据结构。每个节点包含一个值和一个指向序列中下一个节点的指针。序列中的最后一个节点指向第一个节点，形成一个循环。

循环链表相对于线性链表的优势在于它可以以循环方式遍历。这使它成为游戏或操作系统调度程序等应用程序的合适数据结构。

## 代码示例

下面是 C 编程语言中循环链表的示例：

```c
struct node {
   int data;
   struct node *next;
};

struct node *head = NULL;

void insert_node(int data) {
   struct node *new_node = malloc(sizeof(struct node));
   new_node->data = data;
   new_node->next = head;
   if (head != NULL) {
      struct node *temp = head;
      while (temp->next != head) {
         temp = temp->next;
      }
      temp->next = new_node;
   } else {
      new_node->next = new_node;
   }
   head = new_node;
}

void delete_node(int data) {
   if (head == NULL) {
      return;
   }
   if (head->next == head && head->data == data) {
      free(head);
      head = NULL;
      return;
   }
   struct node *temp = head;
   while (temp->next != head && temp->next->data != data) {
      temp = temp->next;
   }
   if (temp->next->data == data) {
      struct node *to_be_deleted = temp->next;
      if (to_be_deleted == head) {
         head = to_be_deleted->next;
      }
      temp->next = to_be_deleted->next;
      free(to_be_deleted);
   }
}

void print_list() {
   if (head == NULL) {
      printf("List is empty\n");
      return;
   }
   struct node *temp = head;
   printf("List: ");
   do {
      printf("%d ", temp->data);
      temp = temp->next;
   } while (temp != head);
   printf("\n");
}

int main() {
   insert_node(1);
   insert_node(2);
   insert_node(3);
   insert_node(4);
   print_list();
   delete_node(2);
   print_list();
   delete_node(1);
   print_list();
   delete_node(4);
   print_list();
   delete_node(3);
   print_list();
   return 0;
}
```

## 练习

1. 实现一个函数来检查给定的单链表是否是循环的。

2. 实现一个函数来查找给定单向链表的中间节点。

3. 实现一个函数，从给定的单向链表的末尾找到第 N 个节点。

4. 实现一个函数来检查给定的单向链表是否为回文。

## 答案

1.

```c
bool is_circular(struct node *head) {
   if (head == NULL) {
      return true;
   }
   struct node *temp = head;
   while (temp->next != head) {
      temp = temp->next;
   }
   return (temp == head);
}
```

2.

```c
struct node *find_middle(struct node *head) {
   if (head == NULL) {
      return NULL;
   }
   struct node *slow_ptr = head;
   struct node *fast_ptr = head;
   while (fast_ptr->next != head && fast_ptr->next->next != head) {
      slow_ptr = slow_ptr->next;
      fast_ptr = fast_ptr->next->next;
   }
   return slow_ptr;
}
```

3.

```c
struct node *find_nth_from_end(struct node *head, int n) {
   if (head == NULL || n <= 0) {
      return NULL;
   }
   struct node *slow_ptr = head;
   struct node *fast_ptr = head;
   int i;
   for (i = 0; i < n; i++) {
      if (fast_ptr->next == head) {
         return NULL;
      }
      fast_ptr = fast_ptr->next;
   }
   while (fast_ptr != head) {
      slow_ptr = slow_ptr->next;
      fast_ptr = fast_ptr->next;
   }
   return slow_ptr;
}
```

4.

```c
bool is_palindrome(struct node *head) {
   if (head == NULL) {
      return true;
   }
   struct node *slow_ptr = head;
   struct node *fast_ptr = head;
   struct node *prev_slow_ptr = head;
   struct node *mid_node = NULL;
   bool is_even = true;
   while (fast_ptr->next != head && fast_ptr->next->next != head) {
      fast_ptr = fast_ptr->next->next;
      prev_slow_ptr = slow_ptr;
      slow_ptr = slow_ptr->next;
   }
   if (fast_ptr->next->next == head) {
      is_even = false;
   }
   if (is_even) {
      mid_node = slow_ptr;
      slow_ptr = slow_ptr->next;
   }
   struct node *second_half = slow_ptr;
   prev_slow_ptr->next = head;
   struct node *prev_of_curr = second_half;
   struct node *curr = second_half->next;
   while (curr != head) {
      struct node *next = curr->next;
      curr->next = prev_of_curr;
      prev_of_curr = curr;
      curr = next;
   }
   second_half->next = prev_of_curr;
   bool is_palindrome = true;
   struct node *first_ptr = head;
   struct node *second_ptr = second_half;
   while (first_ptr != second_half) {
      if (first_ptr->data != second_ptr->data) {
         is_palindrome = false;
         break;
      }
      first_ptr = first_ptr->next;
      second_ptr = second_ptr->next;
   }
   prev_of_curr = second_half->next;
   curr = prev_of_curr->next;
   while (curr != second_half) {
      struct node *next = curr->next;
      curr->next = prev_of_curr;
      prev_of_curr = curr;
      curr = next;
   }
   if (is_even) {
      mid_node->next = second_half;
   } else {
      head->next = second_half;
   }
   return is_palindrome;
}
```

## 评论

对于需要以循环方式遍历列表的应用程序，循环链表是一种有用的数据结构。它们易于实施，并且可以作为阵列的一种节省空间的替代方案。