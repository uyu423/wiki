---
title: [JavaScript] 017: 순환 연결 목록
description: 
published: true
date: 2023-02-09T19:33:10.653Z
tags: 
editor: markdown
dateCreated: 2023-02-09T19:33:08.923Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 017: Circular Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-017-circular-linked-list)
{.links-list}


# JavaScript 017: 순환 연결 목록

이번 포스팅에서는 순환 연결 리스트에 대해 알아보겠습니다. 그것들이 무엇인지, 일반 연결 목록과 어떻게 다른지, 어떻게 구현하는지에 대해 이야기할 것입니다. 또한 순환 연결 목록을 사용할 때의 장단점에 대해서도 살펴보겠습니다.

## 순환 연결 목록이란 무엇입니까?

순환 연결 리스트는 목록의 마지막 노드가 목록의 첫 번째 노드를 가리키는 연결 목록 유형입니다. 이렇게 하면 목록을 끝없이 탐색할 수 있는 순환이 목록에 생성됩니다.

다음은 순환 연결 목록의 예입니다.

![순환 연결 리스트](https://i.imgur.com/kzgW4vD.png)

보시다시피 목록의 마지막 노드(노드 4)는 목록의 첫 번째 노드(노드 1)를 가리킵니다. 이렇게 하면 목록에 주기가 생성됩니다.

## 원형 연결 목록과 일반 연결 목록의 차이점

순환 연결 목록과 일반 연결 목록의 주요 차이점은 일반 연결 목록에는 목록 끝에 도달했음을 나타내는 null 포인터가 있다는 것입니다. 반면 순환 연결 목록에는 목록의 첫 번째 노드를 다시 가리키는 포인터가 있습니다.

다음은 일반 연결 목록의 예입니다.

![일반 연결 리스트](https://i.imgur.com/FgwJKwB.png)

보시다시피 목록의 마지막 노드(노드 4)에는 널 포인터가 있습니다. 이는 목록의 끝에 도달했음을 나타냅니다.

## 순환 연결 목록을 구현하는 방법

순환 연결 목록을 구현하는 두 가지 방법이 있습니다.

**1. 배열 사용**

순환 연결 목록을 구현하는 첫 번째 방법은 배열을 사용하는 것입니다. 배열 사용의 장점은 구현하기 쉽고 목록을 순회하기 쉽다는 것입니다. 배열 사용의 단점은 그다지 유연하지 않다는 것입니다. 예를 들어 목록 중간에 새 노드를 삽입하려는 경우 새 노드를 위한 공간을 만들기 위해 배열의 모든 요소를 이동해야 합니다.

다음은 배열을 사용하여 순환 연결 목록을 구현하는 방법의 예입니다.

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class CircularLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  // add a new node to the end of the list
  append(data) {
    // create a new node
    let node = new Node(data);

    // if the list is empty, set the head and tail to the new node
    if (this.size === 0) {
      this.head = node;
      this.tail = node;
    } else {
      // otherwise, set the current tail's next pointer to the new node
      this.tail.next = node;
      // and set the new node as the current tail
      this.tail = node;
    }

    // set the new node's next pointer to the head
    node.next = this.head;

    // increment the size
    this.size++;
  }

  // remove the node at the given index
  removeAt(index) {
    // if the index is out of bounds, return null
    if (index < 0 || index >= this.size) {
      return null;
    }

    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // if the index is the same as the size of the list,
    // it means we want to remove the tail
    if (index === this.size - 1) {
      // so set the current tail's next pointer to the head
      this.tail.next = this.head;
      // and set the head as the current tail
      this.tail = this.tail.next;
    } else {
      // otherwise, we need to find the node at the given index
      // so set a pointer to the head
      let pointer = this.head;
      // and set a counter to keep track of our position
      let counter = 0;

      // loop through the list until we find the node at the given index
      while (counter < index) {
        pointer = pointer.next;
        counter++;
      }

      // set the next pointer of the node before the one we want to remove
      // to the node after the one we want to remove
      pointer.next = pointer.next.next;
    }

    // decrement the size
    this.size--;
  }

  // return the node at the given index
  get(index) {
    // if the index is out of bounds, return null
    if (index < 0 || index >= this.size) {
      return null;
    }

    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // set a pointer to the head
    let pointer = this.head;

    // loop through the list until we find the node at the given index
    for (let i = 0; i < index; i++) {
      pointer = pointer.next;
    }

    // return the node at the given index
    return pointer;
  }

  // return the size of the list
  getSize() {
    return this.size;
  }

  // return the head of the list
  getHead() {
    return this.head;
  }

  // return the tail of the list
  getTail() {
    return this.tail;
  }

  // return true if the list is empty, false otherwise
  isEmpty() {
    return this.size === 0;
  }

  // print the list
  print() {
    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // set a pointer to the head
    let pointer = this.head;

    // loop through the list until we reach the tail
    while (pointer.next !== this.tail) {
      // print the data of the current node
      console.log(pointer.data);
      // and set the pointer to the next node
      pointer = pointer.next;
    }

    // print the data of the tail
    console.log(pointer.data);
  }
}

// create a new linked list
let list = new CircularLinkedList();

// append some nodes
list.append(1);
list.append(2);
list.append(3);
list.append(4);

// print the list
list.print(); // 1 2 3 4

// remove a node
list.removeAt(2);

// print the list
list.print(); // 1 2 4

// get the node at the given index
let node = list.get(1);

// print the data of the node
console.log(node.data); // 2

// get the size of the list
let size = list.getSize();

// print the size of the list
console.log(size); // 3

// get the head of the list
let head = list.getHead();

// print the data of the head
console.log(head.data); // 1

// get the tail of the list
let tail = list.getTail();

// print the data of the tail
console.log(tail.data); // 4

// check if the list is empty
let isEmpty = list.isEmpty();

// print true if the list is empty, false otherwise
console.log(isEmpty); // false
```

**2. 연결된 목록 사용**

순환 연결 목록을 구현하는 두 번째 방법은 연결 목록을 사용하는 것입니다. 연결된 목록을 사용하는 이점은 배열보다 유연하다는 것입니다. 예를 들어 목록 중간에 새 노드를 삽입하려는 경우 새 노드 주변의 노드 포인터가 새 노드를 가리키도록 변경하면 됩니다. 연결 리스트 사용의 단점은 리스트를 순회하기가 더 어렵다는 것입니다.

다음은 연결 목록을 사용하여 순환 연결 목록을 구현하는 방법의 예입니다.

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class CircularLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.size = 0;
  }

  // add a new node to the end of the list
  append(data) {
    // create a new node
    let node = new Node(data);

    // if the list is empty, set the head and tail to the new node
    if (this.size === 0) {
      this.head = node;
      this.tail = node;
    } else {
      // otherwise, set the current tail's next pointer to the new node
      this.tail.next = node;
      // and set the new node as the current tail
      this.tail = node;
    }

    // set the new node's next pointer to the head
    node.next = this.head;

    // increment the size
    this.size++;
  }

  // remove the node at the given index
  removeAt(index) {
    // if the index is out of bounds, return null
    if (index < 0 || index >= this.size) {
      return null;
    }

    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // if the index is the same as the size of the list,
    // it means we want to remove the tail
    if (index === this.size - 1) {
      // so set the current tail's next pointer to the head
      this.tail.next = this.head;
      // and set the head as the current tail
      this.tail = this.tail.next;
    } else {
      // otherwise, we need to find the node at the given index
      // so set a pointer to the head
      let pointer = this.head;
      // and set a counter to keep track of our position
      let counter = 0;

      // loop through the list until we find the node before the one we want to remove
      while (counter < index - 1) {
        pointer = pointer.next;
        counter++;
      }

      // set the next pointer of the node before the one we want to remove
      // to the node after the one we want to remove
      pointer.next = pointer.next.next;
    }

    // decrement the size
    this.size--;
  }

  // return the node at the given index
  get(index) {
    // if the index is out of bounds, return null
    if (index < 0 || index >= this.size) {
      return null;
    }

    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // set a pointer to the head
    let pointer = this.head;

    // loop through the list until we find the node at the given index
    for (let i = 0; i < index; i++) {
      pointer = pointer.next;
    }

    // return the node at the given index
    return pointer;
  }

  // return the size of the list
  getSize() {
    return this.size;
  }

  // return the head of the list
  getHead() {
    return this.head;
  }

  // return the tail of the list
  getTail() {
    return this.tail;
  }

  // return true if the list is empty, false otherwise
  isEmpty() {
    return this.size === 0;
  }

  // print the list
  print() {
    // if the list is empty, return null
    if (this.size === 0) {
      return null;
    }

    // set a pointer to the head
    let pointer = this.head;

    // loop through the list until we reach the tail
    while (pointer.next !== this.tail) {
      // print the data of the current node
      console.log(pointer.data);
      // and set the pointer to the next node
      pointer = pointer.next;
    }

    // print the data of the tail
    console.log(pointer.data);
  }
}

// create a new linked list
let list = new CircularLinkedList();

// append some nodes
list.append(1);
list.append(2);
list.append(3);
list.append(4);

// print the list
list.print(); // 1 2 3 4

// remove a node
list.removeAt(2);

// print the list
list.print(); // 1 2 4

// get the node at the given index
let node = list.get(1);

// print the data of the node
console.log(node.data); // 2

// get the size of the list
let size = list.getSize();

// print the size of the list
console.log(size); // 3

// get the head of the list
let head = list.getHead();

// print the data of the head
console.log(head.data); // 1

// get the tail of the list
let tail = list.getTail();

// print the data of the tail
console.log(tail.data); // 4

// check if the list is empty
let isEmpty = list.isEmpty();

// print true if the list is empty, false otherwise
console.log(isEmpty); // false
```

## 순환 연결 목록의 장단점

순환 연결 목록을 사용하면 장점과 단점이 모두 있습니다.

**장점:**

- **큐를 구현하는 데 사용할 수 있습니다.** 큐는 목록의 뒤에 요소를 삽입하고 목록의 앞에 있는 요소를 제거할 수 있는 데이터 구조입니다. 이를 FIFO(First In First Out) 데이터 구조라고 합니다. 순환 연결 목록을 사용하면 FIFO 방식으로 목록에서 요소를 삽입하고 제거할 수 있으므로 대기열을 구현하는 데 사용할 수 있습니다.

- **스택을 구현하는 데 사용할 수 있습니다.** 스택은 목록 맨 위에 요소를 삽입하고 목록 맨 위에서 요소를 제거할 수 있는 데이터 구조입니다. 이를 LIFO(Last In First Out) 데이터 구조라고 합니다. 순환 연결 목록을 사용하면 LIFO 방식으로 목록에서 요소를 삽입하고 제거할 수 있으므로 스택을 구현하는 데 사용할 수 있습니다.

- **deque를 구현하는 데 사용할 수 있습니다.** deque는 목록의 앞과 뒤에 요소를 삽입하고 제거할 수 있는 데이터 구조입니다. 순환 연결 목록을 사용하면 앞과 뒤 모두에서 목록의 요소를 삽입하고 제거할 수 있으므로 deque를 구현하는 데 사용할 수 있습니다.

- **순환 버퍼를 구현하는 데 사용할 수 있습니다.** 순환 버퍼는 목록의 마지막 요소가 목록의 첫 번째 요소에 연결되는 대기열 유형입니다. 이렇게 하면 대기열이 이미 사용된 요소를 둘러싸서 재사용할 수 있습니다. 순환 연결 목록을 사용하면 대기열이 이미 사용된 요소를 둘러싸서 재사용할 수 있기 때문에 순환 버퍼를 구현하는 데 사용할 수 있습니다.

- **우선순위 큐를 구현하는 데 사용할 수 있습니다.** 우선순위 큐는 요소가 우선순위에 따라 큐에 삽입되는 큐 유형입니다. 즉, 우선 순위가 가장 높은 요소는 대기열의 앞에 있고 우선 순위가 가장 낮은 요소는 대기열의 뒤에 있습니다. 순환 연결 목록을 사용하면 FIFO 방식으로 목록에서 요소를 삽입하고 제거할 수 있으므로 우선순위 대기열을 구현하는 데 사용할 수 있습니다.

**단점:**

-