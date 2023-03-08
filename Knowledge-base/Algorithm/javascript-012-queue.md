---
title: [JavaScript] 012: 대기열
description: 
published: true
date: 2023-02-09T14:32:48.967Z
tags: 
editor: markdown
dateCreated: 2023-02-09T14:32:47.394Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 012: Queue***English** document is available*](/en/Knowledge-base/Algorithm/javascript-012-queue)
{.links-list}


# JavaScript 012: 대기열

큐는 FIFO(First-In-First-Out) 방식으로 항목을 저장하는 데이터 구조입니다. 즉, 대기열에 추가된 첫 번째 항목이 대기열에서 제거된 첫 번째 항목이 됩니다. 대기열을 FIFO(First-In-First-Out) 목록이라고도 합니다.

대기열에 대한 일반적인 비유는 은행의 라인입니다. 줄의 첫 번째 사람이 가장 먼저 서비스를 받는 사람이고 마지막 사람이 마지막 서비스를 받는 사람입니다.

대기열에는 대기열에 넣기와 대기열에서 빼기라는 두 가지 주요 작업이 있습니다. Enqueue는 큐의 뒤에 항목을 추가하고 dequeue는 큐의 앞에서 항목을 제거합니다.

## 구현

대기열을 구현하는 방법에는 여러 가지가 있습니다. 가장 일반적인 방법은 배열을 사용하는 것입니다.

### 어레이 구현

대기열을 구현하는 가장 간단한 방법은 배열을 사용하는 것입니다. 배열의 첫 번째 요소는 대기열의 앞쪽이고 배열의 마지막 요소는 대기열의 뒤쪽입니다.

#### 대기열에 넣기

항목을 대기열에 추가하려면 항목을 배열 끝에 추가합니다.

```javascript
function enqueue(item) {
  queue.push(item);
}
```

#### 대기열에서 빼기

항목을 대기열에서 빼기 위해 배열의 첫 번째 항목을 제거합니다.

```javascript
function dequeue() {
  return queue.shift();
}
```

### 연결 리스트 구현

대기열을 구현하는 보다 효율적인 방법은 연결 목록을 사용하는 것입니다. 연결된 목록을 사용하면 항목을 대기열에서 제거할 때 배열의 모든 요소를 이동하는 비용이 많이 드는 작업을 피할 수 있습니다.

#### 대기열에 넣기

항목을 대기열에 추가하려면 연결 목록 끝에 항목을 추가합니다.

```javascript
function enqueue(item) {
  var node = {
    data: item,
    next: null
  };

  if (queue.length === 0) {
    queue.head = node;
  } else {
    queue.tail.next = node;
  }

  queue.tail = node;
}
```

#### 대기열에서 빼기

항목을 대기열에서 빼기 위해 연결 목록에서 첫 번째 항목을 제거합니다.

```javascript
function dequeue() {
  var node = queue.head;

  if (queue.length === 1) {
    queue.tail = null;
  }

  queue.head = node.next;
  queue.length--;

  return node.data;
}
```

## 시간 복잡도

대기열의 배열 및 연결 목록 구현의 시간 복잡도는 모두 O(1)입니다. 즉, 대기열에 넣기와 대기열에서 빼기는 둘 다 일정한 시간 작업입니다.

## 예

다음은 대기열을 사용하는 몇 가지 예입니다.

### 예 1: 숫자 대기열

이 예에서는 숫자 대기열을 만듭니다. 0부터 9까지의 숫자를 순서대로 대기열에 넣습니다. 그런 다음 대기열이 비워질 때까지 각 번호를 대기열에서 빼서 인쇄합니다.

```javascript
var queue = [];

for (var i = 0; i < 10; i++) {
  enqueue(i);
}

while (queue.length > 0) {
  console.log(dequeue());
}
```

위의 코드를 실행하면 0부터 9까지의 숫자가 순서대로 출력됩니다.

### 예 2: 프린터 대기열 시뮬레이션

이 예에서는 프린터 대기열을 시뮬레이트합니다. 인쇄 작업 대기열이 있고 각 작업에는 우선 순위가 있습니다. 우선 순위가 가장 높은 작업이 먼저 대기열에서 제거됩니다.

```javascript
var queue = [];

function enqueue(item, priority) {
  var node = {
    data: item,
    priority: priority,
    next: null
  };

  if (queue.length === 0) {
    queue.head = node;
  } else {
    var current = queue.head;
    var previous;

    while (current && current.priority >= node.priority) {
      previous = current;
      current = current.next;
    }

    if (!previous) {
      node.next = queue.head;
      queue.head = node;
    } else {
      node.next = current;
      previous.next = node;
    }
  }

  queue.length++;
}

function dequeue() {
  var node = queue.head;
  queue.head = node.next;
  queue.length--;
  return node.data;
}

enqueue('A', 1);
enqueue('B', 2);
enqueue('C', 3);
enqueue('D', 4);
enqueue('E', 5);

console.log(dequeue()); // A
console.log(dequeue()); // B
console.log(dequeue()); // C
console.log(dequeue()); // D
console.log(dequeue()); // E
```

위의 코드를 실행하면 문자 A부터 E까지 순서대로 인쇄됩니다.