---
title: [JavaScript] 015: 단일 연결 목록
description: 
published: true
date: 2023-02-09T17:33:38.553Z
tags: 
editor: markdown
dateCreated: 2023-02-09T17:33:36.919Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 015: Single Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-015-single-linked-list)
{.links-list}


# JavaScript 015: 단일 연결 목록

연결 목록은 데이터 모음을 노드에 저장하는 데이터 구조 유형입니다. 연결된 목록의 각 노드에는 데이터 자체와 목록의 다음 노드에 대한 참조라는 두 가지 항목이 포함됩니다. 연결된 목록은 조작하기 쉽고 노드 간 링크를 저장하기 위해 추가 메모리가 필요하지 않기 때문에 자주 사용됩니다.

연결 목록에는 단일 연결 목록과 이중 연결 목록의 두 가지 유형이 있습니다. 단일 연결 목록에서 각 노드는 목록의 다음 노드에 대한 참조만 가집니다. 이중 연결 리스트에서 각 노드는 다음 노드와 이전 노드 모두에 대한 참조를 가집니다.

## 연결된 목록 만들기

연결 리스트를 만들려면 `Node` 클래스를 만들어야 합니다. 각 `Node`에는 해당 노드에 대한 데이터를 저장하는 `data`와 목록의 다음 노드에 대한 참조를 저장하는 `next`라는 두 가지 속성이 있습니다.

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

이제 `Node` 클래스가 있으므로 `LinkedList` 클래스를 만들 수 있습니다. `LinkedList` 클래스에는 목록의 첫 번째 노드를 저장하는 `head`와 목록의 마지막 노드를 저장하는 `tail`의 두 가지 속성이 있습니다.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }
}
```

## 데이터 삽입

연결 리스트에 데이터를 삽입하는 방법에는 두 가지가 있습니다: 목록의 맨 앞 또는 맨 끝.

### 헤드에 삽입

목록의 헤드에 데이터를 삽입하려면 데이터로 새 노드를 만들고 새 노드의 `next` 속성을 목록의 현재 헤드로 설정해야 합니다. 그런 다음 목록의 헤드를 새 노드로 설정합니다.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  insertAtHead(data) {
    const newNode = new Node(data);
    newNode.next = this.head;
    this.head = newNode;
  }
}
```

### 꼬리에 삽입

목록의 꼬리에 데이터를 삽입하려면 데이터로 새 노드를 만들고 목록의 현재 꼬리의 `next` 속성을 새 노드로 설정해야 합니다. 그런 다음 목록의 꼬리를 새 노드로 설정합니다.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  insertAtTail(data) {
    const newNode = new Node(data);
    if (!this.head) {
      this.head = newNode;
    }
    if (this.tail) {
      this.tail.next = newNode;
    }
    this.tail = newNode;
  }
}
```

## 데이터 삭제

연결된 목록에서 데이터를 삭제하는 방법에는 두 가지가 있습니다: 목록의 머리에서 또는 목록의 꼬리에서.

### 헤드에서 삭제

목록의 헤드에서 데이터를 삭제하려면 목록의 헤드를 현재 헤드 다음 노드로 설정하기만 하면 됩니다.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  deleteFromHead() {
    if (!this.head) {
      return;
    }
    this.head = this.head.next;
  }
}
```

### 테일에서 삭제

목록의 꼬리에서 데이터를 삭제하려면 꼬리 이전의 노드를 추적해야 합니다. 그런 다음 꼬리 앞 노드의 `next` 속성을 `null`로 설정하고 목록의 꼬리를 꼬리 앞 노드로 설정합니다.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  deleteFromTail() {
    if (!this.tail) {
      return;
    }
    if (!this.head) {
      this.head = null;
      this.tail = null;
      return;
    }
    let current = this.head;
    while (current.next !== this.tail) {
      current = current.next;
    }
    current.next = null;
    this.tail = current;
  }
}
```

## 데이터 검색

연결된 목록에서 데이터를 검색하려면 목록의 맨 처음부터 시작하여 각 노드의 데이터와 검색 중인 데이터를 비교해야 합니다. 데이터가 발견되면 노드를 반환합니다. 데이터를 찾을 수 없으면 `null`을 반환합니다.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

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
}
```

## 연결 리스트 순회

연결된 목록을 순회하려면 목록의 맨 위에서 시작하여 각 노드를 차례로 방문해야 합니다. 우리는 `while` 루프를 사용하여 이것을 할 수 있습니다.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  traverse() {
    let current = this.head;
    while (current) {
      console.log(current.data);
      current = current.next;
    }
  }
}
```

## 연결된 목록 뒤집기

연결 리스트를 되돌리려면 이전 노드, 현재 노드, 다음 노드를 추적해야 합니다. 그런 다음 현재 노드의 `next` 속성을 이전 노드로 설정하고 다음 노드로 이동합니다.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  reverse() {
    let current = this.head;
    let previous = null;
    let next = null;
    while (current) {
      next = current.next;
      current.next = previous;
      previous = current;
      current = next;
    }
    this.head = previous;
  }
}
```

## 연결 리스트 정렬

연결 리스트를 정렬하는 방법에는 여러 가지가 있습니다. 한 가지 방법은 [선택 정렬 알고리즘](https://en.wikipedia.org/wiki/Selection_sort)을 사용하는 것입니다.

선택 정렬을 사용하여 연결 목록을 정렬하려면 최소 노드, 현재 노드 및 다음 노드를 추적해야 합니다. 그런 다음 현재 노드의 데이터와 최소 노드의 데이터를 비교합니다. 현재 노드의 데이터가 최소 노드의 데이터보다 작으면 최소 노드를 현재 노드로 설정합니다. 전체 목록을 반복한 후에는 최소 노드의 데이터를 헤드 노드의 데이터와 교환합니다. 그런 다음 다음 노드로 이동하여 프로세스를 반복합니다.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  sort() {
    let current = this.head;
    let minimum = null;
    let next = null;
    while (current) {
      minimum = current;
      next = current.next;
      while (next) {
        if (next.data < minimum.data) {
          minimum = next;
        }
        next = next.next;
      }
      if (minimum !== current) {
        const temp = current.data;
        current.data = minimum.data;
        minimum.data = temp;
      }
      current = current.next;
    }
  }
}
```

## 결론

연결 목록은 데이터 모음을 노드에 저장하는 데이터 구조 유형입니다. 연결된 목록의 각 노드에는 데이터 자체와 목록의 다음 노드에 대한 참조라는 두 가지 항목이 포함됩니다. 연결된 목록은 조작하기 쉽고 노드 간 링크를 저장하기 위해 추가 메모리가 필요하지 않기 때문에 자주 사용됩니다.

연결 목록에는 단일 연결 목록과 이중 연결 목록의 두 가지 유형이 있습니다. 단일 연결 목록에서 각 노드는 목록의 다음 노드에 대한 참조만 가집니다. 이중 연결 리스트에서 각 노드는 다음 노드와 이전 노드 모두에 대한 참조를 가집니다.

연결 리스트를 만들려면 `Node` 클래스를 만들어야 합니다. 각 `Node`에는 해당 노드에 대한 데이터를 저장하는 `data`와 목록의 다음 노드에 대한 참조를 저장하는 `next`라는 두 가지 속성이 있습니다.

연결된 목록에 데이터를 삽입하려면 목록의 맨 앞에 삽입하거나 목록의 맨 뒤에 삽입할 수 있습니다. 연결된 목록에서 데이터를 삭제하려면 목록의 헤드에서 삭제하거나 목록의 테일에서 삭제할 수 있습니다.

연결된 목록에서 데이터를 검색하려면 목록의 맨 처음부터 시작하여 각 노드의 데이터와 검색 중인 데이터를 비교해야 합니다. 데이터가 발견되면 노드를 반환합니다. 데이터를 찾을 수 없으면 `null`을 반환합니다.

연결된 목록을 순회하려면 목록의 맨 위에서 시작하여 각 노드를 차례로 방문해야 합니다. 연결 리스트를 되돌리려면 이전 노드, 현재 노드, 다음 노드를 추적해야 합니다. 그런 다음 현재 노드의 `next` 속성을 이전 노드로 설정하고 다음 노드로 이동합니다.

연결 리스트를 정렬하는 방법에는 여러 가지가 있습니다. 한 가지 방법은 [선택 정렬 알고리즘](https://en.wikipedia.org/wiki/Selection_sort)을 사용하는 것입니다. 선택 정렬을 사용하여 연결 목록을 정렬하려면 최소 노드, 현재 노드 및 다음 노드를 추적해야 합니다. 그런 다음 현재 노드의 데이터와 최소 노드의 데이터를 비교합니다. 현재 노드의 데이터가 최소 노드의 데이터보다 작으면 최소 노드를 현재 노드로 설정합니다. 전체 목록을 반복한 후에는 최소 노드의 데이터를 헤드 노드의 데이터와 교환합니다. 그런 다음 다음 노드로 이동하여 프로세스를 반복합니다.