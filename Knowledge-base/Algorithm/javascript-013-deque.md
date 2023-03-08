---
title: [JavaScript] 013: 그래서
description: 
published: true
date: 2023-02-09T15:32:30.312Z
tags: 
editor: markdown
dateCreated: 2023-02-09T15:32:28.698Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 013: Deque***English** document is available*](/en/Knowledge-base/Algorithm/javascript-013-deque)
{.links-list}


# 데크

양단 큐라고도 하는 양단 큐는 큐의 양쪽 끝에서 요소를 추가하거나 제거할 수 있는 순서가 지정된 항목 모음입니다. 데크는 스택과 큐의 일반화이며 종종 이중 연결 목록으로 구현됩니다.

## 운영

Deques는 다음 작업을 지원합니다.

* ```push(x)```: deque 뒤에 항목 x를 추가합니다.
* ```pop()```: deque 뒤에 있는 항목을 제거하고 반환합니다.
* ```unshift(x)```: 항목 x를 deque 앞에 추가합니다.
* ```shift()```: deque 앞에 있는 항목을 제거하고 반환합니다.

## 구현

JavaScript에서는 배열을 사용하여 deque를 구현할 수 있습니다.

```javascript
function Deque() {
  this.dataStore = [];
  this.push = push;
  this.pop = pop;
  this.unshift = unshift;
  this.shift = shift;
}

function push(element) {
  this.dataStore.push(element);
}

function pop() {
  return this.dataStore.pop();
}

function unshift(element) {
  this.dataStore.unshift(element);
}

function shift() {
  return this.dataStore.shift();
}
```

## 용법

deque를 사용하여 ```unshift()``` 및 ```shift()``` 작업이 사용되는 대기열을 구현할 수 있습니다.

```javascript
function Queue() {
  this.dataStore = [];
  this.enqueue = enqueue;
  this.dequeue = dequeue;
}

function enqueue(element) {
  this.dataStore.unshift(element);
}

function dequeue() {
  return this.dataStore.shift();
}
```

또한 deque를 사용하여 ```push()``` 및 ```pop()`` 연산이 사용되는 스택을 구현할 수 있습니다.

```javascript
function Stack() {
  this.dataStore = [];
  this.push = push;
  this.pop = pop;
}

function push(element) {
  this.dataStore.push(element);
}

function pop() {
  return this.dataStore.pop();
}
```

## 운동

1. deque를 사용하여 대기열을 구현합니다.

2. deque를 사용하여 스택을 구현합니다.

3. deque를 사용하여 회문 검사기를 구현합니다.