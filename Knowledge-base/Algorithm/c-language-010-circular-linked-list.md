---
title: [C언어] 010: 순환 연결 리스트
description: 
published: true
date: 2023-02-10T13:17:44.965Z
tags: 
editor: markdown
dateCreated: 2023-02-10T13:17:38.747Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 010: Circular Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-010-circular-linked-list)
{.links-list}


# 순환 연결 리스트

순환 연결 목록은 목록의 마지막 노드가 다시 첫 번째 노드를 가리키며 루프를 형성하는 연결 목록의 변형입니다. 이 유형의 목록은 게임이나 운영 체제 스케줄러와 같이 목록을 라운드 로빈 방식으로 순회해야 하는 애플리케이션에 유용합니다.

## 개념

순환 연결 목록은 일련의 노드를 포함하는 데이터 구조입니다. 각 노드에는 값과 시퀀스의 다음 노드에 대한 포인터가 포함됩니다. 시퀀스의 마지막 노드는 다시 첫 번째 노드를 가리키며 루프를 형성합니다.

선형 연결 목록에 비해 순환 연결 목록의 장점은 라운드 로빈 방식으로 순회할 수 있다는 것입니다. 따라서 게임 또는 운영 체제 스케줄러와 같은 응용 프로그램에 적합한 데이터 구조가 됩니다.

## 코드 예제

다음은 C 프로그래밍 언어로 된 순환 연결 목록의 예입니다.

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

## 운동

1. 주어진 단일 연결 목록이 순환인지 확인하는 함수를 구현합니다.

2. 주어진 단일 연결 목록의 중간 노드를 찾는 함수를 구현합니다.

3. 주어진 단일 연결 목록의 끝에서 N번째 노드를 찾는 함수를 구현합니다.

4. 주어진 단일 연결 목록이 회문인지 확인하는 함수를 구현합니다.

## 답변

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

삼.

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

## 해설

순환 연결 목록은 목록을 라운드 로빈 방식으로 순회해야 하는 응용 프로그램에 유용한 데이터 구조입니다. 구현하기 쉽고 어레이에 대한 공간 절약형 대안이 될 수 있습니다.