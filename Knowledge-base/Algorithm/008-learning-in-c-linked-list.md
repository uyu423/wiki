---
title: 008: C로 배우기: 연결 목록
description: 
published: true
date: 2023-02-09T03:19:04.392Z
tags: 
editor: markdown
dateCreated: 2023-02-09T03:19:04.392Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [008: Learning in C: Linked List***English** document is available*](/en/Knowledge-base/Algorithm/008-learning-in-c-linked-list)
{.links-list}


# 008: C로 배우기: 연결 목록

연결된 목록은 노드라고 하는 데이터 항목 모음을 선형 순서로 저장하는 데이터 구조입니다. 각 노드에는 데이터 필드와 링크 필드라는 두 개의 필드가 있습니다. 데이터 필드는 실제 데이터 항목을 저장하고 링크 필드는 목록의 다음 노드 주소를 저장합니다.

연결 리스트의 첫 번째 노드를 헤드 노드라고 하고 마지막 노드를 테일 노드라고 합니다. 헤드 노드는 목록에서 링크 필드가 없는 유일한 노드이고 꼬리 노드는 목록에서 데이터 필드가 없는 유일한 노드입니다.

다음 그림은 4개의 노드가 있는 연결 목록을 보여줍니다. 머리 노드는 왼쪽에 있고 꼬리 노드는 오른쪽에 있습니다.

![링크된 목록](https://i.imgur.com/lkz5vj7.png)

연결된 목록에 새 노드를 추가하려면 새 노드를 가리키도록 꼬리 노드의 링크 필드를 설정하기만 하면 됩니다.

![새 노드 추가](https://i.imgur.com/q7OM4y4.png)

연결 리스트에서 노드를 제거하려면 제거할 노드 앞에 있는 노드의 링크 필드가 제거할 노드 뒤에 오는 노드를 가리키도록 설정하기만 하면 됩니다.

![노드 제거하기](https://i.imgur.com/tUw4KDV.png)

연결 리스트의 가장 일반적인 유형은 각 노드가 단일 링크 필드를 포함하는 단일 연결 리스트입니다. 다음 그림은 4개의 노드가 있는 단일 연결 목록을 보여줍니다.

![단독 연결 리스트](https://i.imgur.com/Fgsepq7.png)

연결된 목록에서 수행할 수 있는 두 가지 주요 작업은 순회 및 삽입입니다.

순회는 연결된 목록의 각 노드를 순서대로 방문하는 과정입니다. 연결 리스트를 순회하는 가장 일반적인 방법은 헤드 노드에서 시작하여 테일 노드에 도달할 때까지 링크 필드를 따라가는 것입니다.

![연결된 목록 탐색](https://i.imgur.com/TGiukcN.png)

삽입은 연결된 목록에 새 노드를 추가하는 프로세스입니다. 연결 리스트에 새 노드를 삽입하는 가장 일반적인 방법은 리스트의 헤드에 삽입하는 것입니다.

![새 노드 삽입](https://i.imgur.com/C4FgWLI.png)

삭제, 연결 및 반전과 같은 연결 목록에서 수행할 수 있는 몇 가지 다른 작업이 있습니다. 그러나 이러한 작업은 이 문서의 범위를 벗어납니다.

이제 연결 목록의 기본 사항을 다루었으므로 C 프로그래밍 언어에서 연결 목록을 구현하는 방법을 살펴보겠습니다.

가장 먼저 해야 할 일은 노드 구조를 정의하는 것입니다. 노드 구조는 일반적으로 데이터 필드와 링크 필드라는 두 개의 필드를 포함합니다. 데이터 필드는 실제 데이터 항목을 저장하는 데 사용되고 링크 필드는 목록에서 다음 노드의 주소를 저장하는 데 사용됩니다.

```c
struct node {
  int data;
  struct node *link;
};
```

이제 헤드 노드를 만들고 링크 필드가 목록의 첫 번째 노드를 가리키도록 설정하여 연결된 목록을 만들 수 있습니다.

```c
struct node *head;
head = malloc(sizeof(struct node));
head->link = NULL;
```

꼬리 노드의 링크 필드가 새 노드를 가리키도록 설정하여 연결 목록에 새 노드를 추가할 수 있습니다.

```c
struct node *tail;
tail = head;
while (tail->link != NULL) {
  tail = tail->link;
}
tail->link = malloc(sizeof(struct node));
tail->link->data = 5;
tail->link->link = NULL;
```

제거할 노드 앞에 있는 노드의 링크 필드가 제거할 노드 뒤에 오는 노드를 가리키도록 설정하여 연결 목록에서 노드를 제거할 수 있습니다.

```c
struct node *prev;
struct node *curr;
curr = head;
while (curr->data != 5) {
  prev = curr;
  curr = curr->link;
}
prev->link = curr->link;
free(curr);
```

연결 리스트의 가장 일반적인 유형은 각 노드가 단일 링크 필드를 포함하는 단일 연결 리스트입니다. 다음 코드는 C에서 단일 연결 목록을 만드는 방법을 보여줍니다.

```c
struct node *head;
head = malloc(sizeof(struct node));
head->data = 1;
head->link = malloc(sizeof(struct node));
head->link->data = 2;
head->link->link = malloc(sizeof(struct node));
head->link->link->data = 3;
head->link->link->link = NULL;
```

헤드 노드에서 시작하여 테일 노드에 도달할 때까지 링크 필드를 따라 단일 연결 리스트를 순회할 수 있습니다.

```c
struct node *curr;
curr = head;
while (curr != NULL) {
  printf("%d\n", curr->data);
  curr = curr->link;
}
```

새 노드의 링크 필드가 헤드 노드를 가리키도록 설정한 다음 헤드 노드가 새 노드를 가리키도록 설정하여 단일 연결 리스트에 새 노드를 삽입할 수 있습니다.

```c
struct node *new_node;
new_node = malloc(sizeof(struct node));
new_node->data = 4;
new_node->link = head;
head = new_node;
```

이것이 연결 목록의 전부입니다! 다음 기사에서는 또 다른 데이터 구조인 스택에 대해 살펴보겠습니다.