---
title: [C언어] 015: 단일 연결 리스트
description: 
published: true
date: 2023-02-13T00:32:29.225Z
tags: 
editor: markdown
dateCreated: 2023-02-13T00:32:27.251Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 015: Single Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-015-single-linked-list)
{.links-list}


# 015: 단일 연결 목록

단일 연결 목록은 일련의 노드를 포함하는 데이터 구조입니다. 각 노드에는 두 개의 필드가 있습니다.

- `data`: 노드에 대한 데이터를 포함합니다.
- `next`: 목록의 다음 노드에 대한 포인터를 포함합니다.

목록의 첫 번째 노드를 `head` 노드라고 하고 목록의 마지막 노드를 `tail` 노드라고 합니다.

![단일 연결 리스트](https://i.imgur.com/kTGiukN.png)

## 단일 연결 목록 만들기

단일 연결 리스트를 생성하려면 `head` 노드와 `tail` 노드를 생성해야 합니다. `head` 노드는 목록의 첫 번째 노드를 가리키고 `tail` 노드는 목록의 마지막 노드를 가리킵니다.

다음과 같이 C++에서 단일 연결 목록을 만들 수 있습니다.

```c++
// Create a head node.
Node* head = new Node();
 
// Create a tail node.
Node* tail = new Node();
 
// Set the head node's "next" field to point to the tail node.
head->next = tail;
```

## 단일 연결 목록에 노드 추가

단일 연결 목록에 노드를 추가하려면 다음 두 가지 작업을 수행해야 합니다.

- 새 노드를 만듭니다.
- 목록에서 마지막 노드의 `next` 필드가 새 노드를 가리키도록 설정합니다.

다음과 같이 C++에서 단일 연결 목록에 노드를 추가할 수 있습니다.

```c++
// Create a new node.
Node* newNode = new Node();
 
// Set the "next" field of the last node in the list to point to the new node.
tail->next = newNode;
 
// Set the new node as the new tail node.
tail = newNode;
```

## 단일 연결 목록에서 노드 삭제

단일 연결 목록에서 노드를 삭제하려면 다음 두 가지 작업을 수행해야 합니다.

- 삭제할 노드 앞 노드의 `next` 필드가 삭제할 노드 뒤 노드를 가리키도록 설정합니다.
- 노드를 삭제합니다.

다음과 같이 C++의 단일 연결 목록에서 노드를 삭제할 수 있습니다.

```c++
// Set the "next" field of the node before the node to be deleted to point to the node after the node to be deleted.
nodeBefore->next = nodeToDelete->next;
 
// Delete the node.
delete nodeToDelete;
```

## 단일 연결 목록 순회

단일 연결 리스트를 순회하려면 `head` 노드에서 시작하여 `tail` 노드에 도달할 때까지 `next` 포인터를 따라야 합니다.

다음과 같이 C++에서 단일 연결 목록을 순회할 수 있습니다.

```c++
// Start at the head node.
Node* currentNode = head;
 
// Follow the "next" pointers until we reach the tail node.
while (currentNode != tail)
{
    // Do something with the data in the node.
 
    // Move to the next node.
    currentNode = currentNode->next;
}
```

## 관련 연습

- [015: 단일 연결 목록](https://github.com/egis/data-structures/tree/master/015-single-linked-list)
- [016: 이중 연결 리스트](https://github.com/egis/data-structures/tree/master/016-double-linked-list)
- [017: 순환 연결 목록](https://github.com/egis/data-structures/tree/master/017-circular-linked-list)