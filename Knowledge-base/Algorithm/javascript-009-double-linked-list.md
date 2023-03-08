---
title: [JavaScript] 009: 이중 연결 목록
description: 
published: true
date: 2023-02-09T11:32:54.013Z
tags: 
editor: markdown
dateCreated: 2023-02-09T11:32:47.800Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 009: Double Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-009-double-linked-list)
{.links-list}


# JavaScript 009: 이중 연결 목록

## 이중 연결 목록이란 무엇입니까?

**이중 연결 목록**은 각각 목록의 다음 노드와 이전 노드를 가리키는 일련의 노드로 구성된 데이터 구조입니다. 이 유형의 연결 목록은 데이터를 앞뒤로 이동할 수 있어야 할 때 자주 사용됩니다.

## 노드 객체

이중 연결 목록에서 각 노드에는 두 개의 포인터가 있습니다.
* `next`: 목록의 다음 노드를 가리킴
* `prev`: 목록에서 이전 노드를 가리킴

또한 각 노드에는 실제 데이터를 보유하는 'data' 속성이 있습니다.

## 이중 연결 리스트 만들기

세 개의 노드가 있는 간단한 이중 연결 목록을 만들어 봅시다. `Node` 클래스를 만드는 것으로 시작하겠습니다.

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
    this.prev = null;
  }
}
```

이제 `LinkedList` 클래스를 만들 수 있습니다.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }
}
```

우리의 `LinkedList`에는 두 가지 속성이 있습니다.
* `head`: 목록의 첫 번째 노드를 가리킴
* `tail`: 목록의 마지막 노드를 가리킴

## 노드 삽입

이중 연결 리스트에 노드를 삽입하는 방법에는 두 가지가 있습니다.
* 목록의 **헤드**에
* 목록의 **꼬리**

`insertAtHead` 메소드부터 시작하겠습니다. 이 메서드는 `data` 매개변수를 사용하고 해당 데이터로 새 노드를 만듭니다. 그런 다음 새 노드가 목록의 'head'로 할당되고 새 노드의 'next' 포인터가 이전 헤드 노드를 가리키도록 설정됩니다. 마지막으로 이전 헤드 노드의 `prev` 포인터가 새 노드를 가리키도록 설정됩니다.

```javascript
insertAtHead(data) {
  const newNode = new Node(data);
  newNode.next = this.head;
  this.head.prev = newNode;
  this.head = newNode;
}
```

`insertAtTail` 메서드도 비슷하지만 새 노드가 목록의 `tail`로 할당되고 새 노드의 `prev` 포인터가 이전 꼬리 노드를 가리키도록 설정됩니다. 마지막으로 이전 테일 노드의 `next` 포인터가 새 노드를 가리키도록 설정됩니다.

```javascript
insertAtTail(data) {
  const newNode = new Node(data);
  newNode.prev = this.tail;
  this.tail.next = newNode;
  this.tail = newNode;
}
```

## 노드 삭제

이중 연결 목록에서 노드를 삭제하는 두 가지 방법도 있습니다.
* 목록의 **head**에서
* 목록의 **꼬리**에서

`deleteFromHead` 메서드부터 시작하겠습니다. 이 메서드는 단순히 현재 헤드 노드의 'next' 포인터가 가리키는 노드에 목록의 'head'를 할당합니다. 그러면 새 헤드 노드의 `prev` 포인터가 `null`로 설정됩니다.

```javascript
deleteFromHead() {
  this.head = this.head.next;
  this.head.prev = null;
}
```

`deleteFromTail` 메소드도 비슷하지만 목록의 `tail`은 현재 테일 노드의 `prev` 포인터가 가리키는 노드에 할당됩니다. 그러면 새로운 꼬리 노드의 `next` 포인터가 `null`로 설정됩니다.

```javascript
deleteFromTail() {
  this.tail = this.tail.prev;
  this.tail.next = null;
}
```

## 목록 검색

'검색' 방법을 사용하여 특정 데이터 조각에 대한 목록을 검색할 수 있습니다. 이 메서드는 `data` 매개변수를 사용하고 해당 데이터가 포함된 노드를 반환합니다. 데이터를 찾을 수 없으면 메서드는 `null`을 반환합니다.

```javascript
search(data) {
  let current = this.head;

  while (current) {
    if (current.data === data) {
      return current;
    }
    current = current.next;
  }

  return null;
}
```

## 목록 순회

`traverse` 메서드를 사용하여 목록을 순회할 수 있습니다. 이 메서드는 목록의 각 노드에서 호출되는 `콜백` 함수를 사용합니다.

```javascript
traverse(callback) {
  let current = this.head;

  while (current) {
    callback(current);
    current = current.next;
  }
}
```

## 목록 뒤집기

'reverse' 메서드를 사용하여 목록을 뒤집을 수 있습니다. 이 메서드는 단순히 목록에 있는 각 노드의 `next` 및 `prev` 포인터를 교체합니다.

```javascript
reverse() {
  let current = this.head;

  while (current) {
    const temp = current.next;
    current.next = current.prev;
    current.prev = temp;
    current = current.next;
  }

  const temp = this.head;
  this.head = this.tail;
  this.tail = temp;
}
```

## 결론

이번 포스팅에서는 이중 연결 리스트를 생성하고 사용하는 방법에 대해 알아보았습니다. 이 데이터 구조는 데이터를 앞뒤로 이동할 수 있어야 할 때 유용할 수 있습니다.