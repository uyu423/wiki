---
title: [C언어] 017: 순환 연결 리스트
description: 
published: true
date: 2023-02-13T01:32:59.507Z
tags: 
editor: markdown
dateCreated: 2023-02-13T01:32:57.858Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 017: Circular Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-017-circular-linked-list)
{.links-list}


# 순환 연결 리스트

순환 연결 목록은 마지막 노드가 null을 가리키는 대신 다시 첫 번째 노드(또는 헤드 노드)를 가리키는 연결 목록의 변형입니다. 즉, 꼬리 노드가 머리 노드를 가리키는 연결 목록입니다.

## 개념

순환 연결 목록은 일련의 노드를 포함하는 데이터 구조입니다. 각 노드에는 두 개의 필드가 있습니다.

- 데이터를 저장하는 **data** 필드
- 목록의 다음 노드에 대한 포인터를 포함하는 **next** 필드

순환 연결 목록의 마지막 노드는 다시 첫 번째 노드(또는 헤드 노드)를 가리킵니다. 이렇게 하면 순환 연결 목록이 **순환** 데이터 구조가 됩니다.

![순환 연결 리스트](https://i.imgur.com/zgNU6UQ.png)

위 다이어그램에서 볼 수 있듯이 마지막 노드(노드 4)는 다시 첫 번째 노드(노드 1)를 가리킵니다.

## 운영

순환 연결 목록은 다음 작업을 지원합니다.

- **삽입**: 목록의 처음, 끝 또는 중간에 새 노드를 삽입할 수 있습니다.
- **삭제**: 목록의 시작, 끝 또는 중간 어디에서나 노드를 삭제할 수 있습니다.
- **검색**: 목록에서 특정 노드를 검색할 수 있습니다.
- **순회**: 목록을 순회하여 각 노드에 저장된 데이터를 출력할 수 있습니다.

## 장점

순환 연결 목록은 다른 데이터 구조에 비해 다음과 같은 이점이 있습니다.

- **빠른 삽입 및 삭제**: 순환 연결 목록의 모든 위치에서 노드를 삽입하고 삭제할 수 있습니다. 배열에서는 불가능합니다.
- **유연한 크기**: 원형 연결 목록의 크기는 언제든지 늘리거나 줄일 수 있습니다. 배열에서는 불가능합니다.
- **효율적인 메모리 활용**: 단일 포인터를 사용하여 순환 연결 목록을 구현할 수 있습니다. 배열에서는 불가능합니다.

## 단점

순환 연결 목록에는 다음과 같은 단점이 있습니다.

- **뒤집기 어려움**: 순환 연결 목록을 뒤집기가 어렵습니다.
- **No random access**: 순환 연결 목록의 노드에 임의로 접근할 수 없습니다. 헤드 노드에서 시작하여 찾고 있는 노드를 찾을 때까지 목록을 순회해야 합니다.

## 코드 예제

### 삽입

목록의 처음, 끝 또는 중간에 새 노드를 삽입할 수 있습니다.

**처음에 삽입:**

```c
void insertAtBeginning(int data) {
  // Create a new node
  struct Node* newNode = (struct Node*) malloc(sizeof(struct Node));
  newNode->data = data;
 
  // Set the next field of the new node to point to the head node
  newNode->next = head;
 
  // Set the next field of the last node to point to the new node
  if(head != NULL) {
    struct Node* temp = head;
    while(temp->next != head) {
      temp = temp->next;
    }
    temp->next = newNode;
  } else {
    // If the list is empty, set the new node as the head node
    newNode->next = newNode;
  }
 
  // Set the new node as the head node
  head = newNode;
}
```

**마지막에 삽입:**

```c
void insertAtEnd(int data) {
  // Create a new node
  struct Node* newNode = (struct Node*) malloc(sizeof(struct Node));
  newNode->data = data;
 
  // Set the next field of the new node to point to the head node
  newNode->next = head;
 
  // If the list is empty, set the new node as the head node
  if(head == NULL) {
    head = newNode;
  } else {
    // Set the next field of the last node to point to the new node
    struct Node* temp = head;
    while(temp->next != head) {
      temp = temp->next;
    }
    temp->next = newNode;
  }
}
```

**가운데 삽입:**

```c
void insertInMiddle(int data, int position) {
  // Create a new node
  struct Node* newNode = (struct Node*) malloc(sizeof(struct Node));
  newNode->data = data;
 
  // Set the next field of the new node to point to the head node
  newNode->next = head;
 
  // If the list is empty, set the new node as the head node
  if(head == NULL) {
    head = newNode;
  } else {
    // Find the node at the given position
    struct Node* temp = head;
    int i;
    for(i=0; i<position-1; i++) {
      temp = temp->next;
    }
 
    // Set the next field of the new node to point to the node at the given position
    newNode->next = temp->next;
 
    // Set the next field of the node at the given position to point to the new node
    temp->next = newNode;
  }
}
```

### 삭제

시작, 끝 또는 목록 중간에서 노드를 삭제할 수 있습니다.

**처음부터 삭제:**

```c
void deleteFromBeginning() {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Find the last node
  struct Node* temp = head;
  while(temp->next != head) {
    temp = temp->next;
  }
 
  // Set the next field of the last node to point to the head node
  temp->next = head->next;
 
  // Free the memory occupied by the head node
  free(head);
 
  // Set the head node to the node at the given position
  head = temp->next;
}
```

**끝부터 삭제:**

```c
void deleteFromEnd() {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Find the last node
  struct Node* temp = head;
  while(temp->next != head) {
    temp = temp->next;
  }
 
  // Set the next field of the last node to point to the head node
  temp->next = head;
 
  // Free the memory occupied by the last node
  free(temp);
}
```

**중간부터 삭제:**

```c
void deleteFromMiddle(int position) {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Find the node at the given position
  struct Node* temp = head;
  int i;
  for(i=0; i<position-1; i++) {
    temp = temp->next;
  }
 
  // Set the next field of the node at the given position to point to the node at the given position
  struct Node* toBeDeleted = temp->next;
 
  // Set the next field of the node at the given position to point to the node at the given position
  temp->next = toBeDeleted->next;
 
  // Free the memory occupied by the node at the given position
  free(toBeDeleted);
}
```

### 찾다

목록에서 특정 노드를 검색할 수 있습니다.

```c
void search(int data) {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Find the node with the given data
  struct Node* temp = head;
  int position = 1;
  while(temp->next != head) {
    if(temp->data == data) {
      break;
    }
    temp = temp->next;
    position++;
  }
 
  // If the data is not found, return
  if(temp->data != data) {
    return;
  }
 
  // Print the data
  printf("%d", temp->data);
}
```

### 순회

목록을 순회하여 각 노드에 저장된 데이터를 인쇄할 수 있습니다.

```c
void traverse() {
  // If the list is empty, return
  if(head == NULL) {
    return;
  }
 
  // Print the data in each node
  struct Node* temp = head;
  do {
    printf("%d ", temp->data);
    temp = temp->next;
  } while(temp != head);
}
```

## 운동

1. 순환 연결 리스트를 만들고 리스트의 시작, 끝, 중간에 노드를 삽입하는 프로그램을 작성하세요.

2. 목록의 시작, 끝, 중간에서 노드를 삭제하는 프로그램을 작성하십시오.

3. 목록에서 특정 노드를 검색하는 프로그램을 작성하십시오.

4. 목록을 순회하고 각 노드에 저장된 데이터를 인쇄하는 프로그램을 작성하십시오.