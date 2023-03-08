---
title: [JavaScript] 008: 연결된 목록
description: 
published: true
date: 2023-02-09T10:32:30.626Z
tags: 
editor: markdown
dateCreated: 2023-02-09T10:32:28.922Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 008: Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-008-linked-list)
{.links-list}


# JavaScript 008: 연결된 목록

연결된 목록은 각 노드가 목록의 다음 노드에 대한 참조를 포함하는 노드 집합으로 구성된 데이터 구조입니다. 이 유형의 목록은 목록을 재정렬할 필요가 없기 때문에 삽입 및 삭제와 같은 작업에 매우 효율적입니다.

연결된 목록에는 두 가지 유형이 있습니다.

- 단일 연결 리스트: 각 노드는 다음 노드에 대한 참조를 가집니다.
- 이중 연결 리스트: 각 노드는 다음 노드와 이전 노드에 대한 참조를 가집니다.

이 게시물에서는 JavaScript에서 단일 연결 목록을 구현합니다.

## 노드 생성

가장 먼저 해야 할 일은 노드 클래스를 만드는 것입니다. 각 노드에는 두 가지 속성이 있습니다.

- `data`: 노드가 보유할 데이터.
- `next`: 목록의 다음 노드에 대한 참조입니다.

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

## 연결된 목록 만들기

이제 노드 클래스가 있으므로 연결 목록 클래스를 만들 수 있습니다. 이 클래스에는 두 가지 속성이 있습니다.

- `head`: 목록의 첫 번째 노드에 대한 참조입니다.
- `tail`: 목록의 마지막 노드에 대한 참조입니다.

연결된 목록 클래스에는 몇 가지 메서드도 있습니다.

- `append(data)`: 주어진 데이터를 가진 새로운 노드를 리스트의 끝에 추가합니다.
- `prepend(data)`: 주어진 데이터가 있는 새 노드를 목록의 시작 부분에 추가합니다.
- `delete(data)`: 주어진 데이터가 있는 첫 번째 노드를 목록에서 삭제합니다.
- `print()`: 목록의 모든 노드를 순서대로 인쇄합니다.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  append(data) {
    // code here
  }

  prepend(data) {
    // code here
  }

  delete(data) {
    // code here
  }

  print() {
    // code here
  }
}
```

## 노드 추가

`append` 메소드는 주어진 데이터가 있는 새 노드를 목록 끝에 추가합니다.

```javascript
append(data) {
  // create a new node with the given data
  const newNode = new Node(data);

  // if the list is empty, set the new node as the head and tail
  if (!this.head) {
    this.head = newNode;
    this.tail = newNode;
  } else {
    // set the current tail's next property to the new node
    this.tail.next = newNode;

    // set the new node as the current tail
    this.tail = newNode;
  }
}
```

## 선행 노드

`prepend` 메소드는 주어진 데이터가 있는 새 노드를 목록의 시작 부분에 추가합니다.

```javascript
prepend(data) {
  // create a new node with the given data
  const newNode = new Node(data);

  // if the list is empty, set the new node as the head and tail
  if (!this.head) {
    this.head = newNode;
    this.tail = newNode;
  } else {
    // set the new node's next property to the current head
    newNode.next = this.head;

    // set the new node as the current head
    this.head = newNode;
  }
}
```

## 노드 삭제

`delete` 메서드는 목록에서 주어진 데이터가 있는 첫 번째 노드를 삭제합니다.

```javascript
delete(data) {
  // if the list is empty, do nothing
  if (!this.head) {
    return;
  }

  // if the head contains the data to be deleted, delete it and set the next node as the new head
  if (this.head.data === data) {
    this.head = this.head.next;
    return;
  }

  // start at the head
  let currentNode = this.head;

  // loop until the tail
  while (currentNode.next) {
    // if the next node contains the data to be deleted, delete it and set the current node's next property to the next node's next property
    if (currentNode.next.data === data) {
      currentNode.next = currentNode.next.next;
      return;
    }

    // if the data is not found, move to the next node
    currentNode = currentNode.next;
  }
}
```

## 목록 인쇄

`print` 메서드는 목록의 모든 노드를 순서대로 인쇄합니다.

```javascript
print() {
  // if the list is empty, do nothing
  if (!this.head) {
    return;
  }

  // start at the head
  let currentNode = this.head;

  // loop until the tail
  while (currentNode) {
    // print the current node's data
    console.log(currentNode.data);

    // move to the next node
    currentNode = currentNode.next;
  }
}
```

## 함께 모아서

연결된 목록 클래스를 구현했으므로 이제 실제로 작동하는 것을 살펴보겠습니다.

```javascript
// create a new linked list
const list = new LinkedList();

// append some nodes
list.append(1);
list.append(2);
list.append(3);

// prepend a node
list.prepend(0);

// delete a node
list.delete(2);

// print the list
list.print();
// 0 -> 1 -> 3
```

그게 전부입니다! 연결된 목록은 다양한 응용 프로그램에서 사용할 수 있는 단순하면서도 강력한 데이터 구조입니다.