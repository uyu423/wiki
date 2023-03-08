---
title: [C Language] 010: Circular Linked List
description: 
published: true
date: 2023-02-10T13:17:40.426Z
tags: 
editor: markdown
dateCreated: 2023-02-10T13:17:38.760Z
---

- [[Lenguaje C] 010: Lista enlazada circular***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-010-circular-linked-list)
{.links-list}
- [[C语言]010：循环链表***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-010-circular-linked-list)
{.links-list}
- [[C언어] 010: 순환 연결 리스트***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-010-circular-linked-list)
{.links-list}


# Circular Linked List

A circular linked list is a variation of a linked list in which the last node of the list points back to the first node, forming a loop. This type of list is useful for applications where the list needs to be traversed in a round-robin fashion, such as in a game or operating system scheduler.

## Concept

A circular linked list is a data structure that contains a sequence of nodes. Each node contains a value and a pointer to the next node in the sequence. The last node in the sequence points back to the first node, forming a loop.

The advantage of a circular linked list over a linear linked list is that it can be traversed in a round-robin fashion. This makes it a suitable data structure for applications such as game or operating system schedulers.

## Code Examples

Here is an example of a circular linked list in the C programming language:

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

## Exercises

1. Implement a function to check if a given singly linked list is circular.

2. Implement a function to find the middle node of a given singly linked list.

3. Implement a function to find the Nth node from the end of a given singly linked list.

4. Implement a function to check if a given singly linked list is palindrome.

## Answers

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

## Commentary

Circular linked lists are a useful data structure for applications where the list needs to be traversed in a round-robin fashion. They are easy to implement and can be a space-saving alternative to arrays.