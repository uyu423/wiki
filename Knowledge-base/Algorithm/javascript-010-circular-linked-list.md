---
title: [JavaScript] 010: 순환 연결 목록
description: 
published: true
date: 2023-02-09T12:32:50.712Z
tags: 
editor: markdown
dateCreated: 2023-02-09T12:32:49.026Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 010: Circular Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-010-circular-linked-list)
{.links-list}


# JavaScript 010: 순환 연결 목록

연결된 목록은 목록의 다음 노드를 가리키는 노드로 구성된 선형 데이터 구조입니다. 순환 연결 목록은 마지막 노드가 다시 첫 번째 노드를 가리키며 루프를 만드는 연결 목록입니다.

## 개념

연결된 목록은 목록의 다음 노드를 가리키는 노드로 구성된 선형 데이터 구조입니다. 순환 연결 목록은 마지막 노드가 다시 첫 번째 노드를 가리키며 루프를 만드는 연결 목록입니다.

순환 연결 리스트는 각 노드가 다음 노드에 대한 참조만 갖는 단일 연결 리스트이거나 각 노드가 다음 노드와 이전 노드에 대한 참조를 갖는 이중 연결 리스트일 수 있습니다.

순환 연결 목록은 항목 목록을 저장하는 데 사용할 수 있는 데이터 구조입니다. 목록의 마지막 노드가 다시 첫 번째 노드를 가리키는 점을 제외하면 단일 연결 목록과 유사합니다. 이렇게 하면 루프가 생성되어 목록을 끝없이 살펴볼 수 있습니다.

단일 연결 목록보다 순환 연결 목록을 사용하면 몇 가지 이점이 있습니다. 첫째, 목록의 끝을 추적할 필요가 없기 때문에 구현하기가 더 쉽습니다. 둘째, 목록의 어느 지점에서나 시작할 수 있고 처음부터 다시 시작할 필요 없이 전체 목록을 순회할 수 있기 때문에 더 효율적입니다. 마지막으로 목록의 어느 지점에서나 항목을 삽입하고 삭제할 수 있기 때문에 더 유연합니다.

## 코드 예제

다음은 JavaScript에서 순환 연결 목록을 간단하게 구현한 것입니다.

```javascript
function Node(data) {
  this.data = data;
  this.next = null;
}

function CircularLinkedList() {
  this.head = null;
  this.tail = null;
  this.length = 0;
}

CircularLinkedList.prototype.add = function(data) {
  var node = new Node(data);

  if (this.length === 0) {
    this.head = node;
  } else {
    this.tail.next = node;
  }

  node.next = this.head;
  this.tail = node;
  this.length++;
};

CircularLinkedList.prototype.remove = function(data) {
  var current = this.head;
  var previous = null;
  var index = 0;

  if (this.length === 0) {
    return null;
  }

  if (this.length === 1) {
    this.head = null;
    this.tail = null;
    this.length--;
    return current.data;
  }

  while (current) {
    if (current.data === data) {
      previous.next = current.next;
      this.length--;
      return current.data;
    }

    previous = current;
    current = current.next;
    index++;
  }

  return null;
};

CircularLinkedList.prototype.get = function(index) {
  var current = this.head;
  var count = 0;

  while (count < index) {
    current = current.next;
    count++;
  }

  return current.data;
};

CircularLinkedList.prototype.contains = function(data) {
  var current = this.head;

  while (current) {
    if (current.data === data) {
      return true;
    }

    current = current.next;
  }

  return false;
};

CircularLinkedList.prototype.size = function() {
  return this.length;
};

CircularLinkedList.prototype.toString = function() {
  var current = this.head;
  var string = '';

  while (current) {
    string += current.data + ' ';
    current = current.next;
  }

  return string.trim();
};

var list = new CircularLinkedList();
list.add('a');
list.add('b');
list.add('c');
list.add('d');
console.log(list.toString()); // a b c d
list.remove('c');
console.log(list.toString()); // a b d
console.log(list.contains('a')); // true
console.log(list.contains('b')); // true
console.log(list.contains('c')); // false
console.log(list.contains('d')); // true
console.log(list.get(0)); // a
console.log(list.get(1)); // b
console.log(list.get(2)); // d
console.log(list.size()); // 3
```

## 운동

1. 목록의 특정 인덱스에 항목을 삽입하는 메서드를 구현합니다.

2. 목록을 뒤집는 방법을 구현합니다.

## 답변

1.

```javascript
CircularLinkedList.prototype.insert = function(index, data) {
  if (index < 0 || index > this.length) {
    return null;
  }

  var node = new Node(data);
  var current = this.head;
  var previous = null;
  var count = 0;

  if (index === 0) {
    if (this.head) {
      node.next = this.head;
    }

    this.head = node;
  } else {
    while (count < index) {
      previous = current;
      current = current.next;
      count++;
    }

    node.next = current;
    previous.next = node;
  }

  this.length++;
  return node.data;
};
```

2.

```javascript
CircularLinkedList.prototype.reverse = function() {
  var current = this.head;
  var previous = null;
  var next = null;

  while (current) {
    next = current.next;
    current.next = previous;
    previous = current;
    current = next;
  }

  this.tail = this.head;
  this.head = previous;
};
```