---
title: [JavaScript] 036: 해시 테이블
description: 
published: true
date: 2023-02-10T14:33:06.707Z
tags: 
editor: markdown
dateCreated: 2023-02-10T14:33:04.731Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 036: Hash Table***English** document is available*](/en/Knowledge-base/Algorithm/javascript-036-hash-table)
{.links-list}


# JavaScript 036: 해시 테이블

이 게시물에서는 키-값 쌍을 저장하는 데 사용되는 데이터 구조인 해시 테이블에 대해 설명합니다. 해시 테이블의 개념과 이론을 다루고 몇 가지 코드 예제를 살펴보고 몇 가지 관련 연습으로 마무리합니다.

## 해시 테이블이란?

해시 테이블은 키-값 쌍을 저장하는 데이터 구조입니다. 배열과 비슷하지만 숫자 인덱스 대신 키를 사용하여 값의 위치를 인덱싱합니다.

해시 테이블은 맵과 세트를 구현하는 데 사용됩니다. 또한 캐싱, 빠른 조회 등과 같은 다른 많은 응용 프로그램에서도 사용됩니다.

## 해시 테이블은 어떻게 작동합니까?

해시 테이블은 해시 함수를 사용하여 키를 값에 매핑합니다. 해시 함수는 키를 가져와 해시 테이블의 위치에 매핑하는 함수입니다.

위치를 버킷이라고 합니다. 버킷은 단순히 배열 인덱스입니다.

해시 함수는 주어진 키에 대한 버킷을 계산하는 데 사용됩니다. 이 함수는 키를 가져와 키를 기반으로 배열 인덱스를 계산합니다. 이 인덱스는 배열에 값을 저장하는 데 사용됩니다.

## 해시 테이블을 사용하는 이유는 무엇입니까?

해시 테이블은 빠릅니다. 일정한 시간 삽입 및 조회 기능이 있습니다. 즉, 값을 삽입하거나 조회하는 데 걸리는 시간은 해시 테이블의 크기와 무관합니다.

해시 테이블도 유연합니다. 맵, 세트 등과 같은 다양한 데이터 구조를 구현하는 데 사용할 수 있습니다.

## 코드 예제

다음은 JavaScript에서 간단한 해시 테이블 구현입니다.


```javascript
function HashTable(size) {
  this.buckets = new Array(size);
  this.numBuckets = this.buckets.length;
}

function HashNode(key, value, next) {
  this.key = key;
  this.value = value;
  this.next = next || null;
}

HashTable.prototype.hash = function(key) {
  var total = 0;
  for (var i = 0; i < key.length; i++) {
    total += key.charCodeAt(i);
  }
  var bucket = total % this.numBuckets;
  return bucket;
};

HashTable.prototype.insert = function(key, value) {
  var bucket = this.hash(key);
  if (!this.buckets[bucket]) {
    this.buckets[bucket] = new HashNode(key, value);
  }
  else if (this.buckets[bucket].key === key) {
    this.buckets[bucket].value = value;
  }
  else {
    var currentNode = this.buckets[bucket];
    while (currentNode.next) {
      if (currentNode.next.key === key) {
        currentNode.next.value = value;
        return;
      }
      currentNode = currentNode.next;
    }
    currentNode.next = new HashNode(key, value);
  }
};

HashTable.prototype.get = function(key) {
  var bucket = this.hash(key);
  if (!this.buckets[bucket]) {
    return null;
  }
  else {
    var currentNode = this.buckets[bucket];
    while (currentNode) {
      if (currentNode.key === key) {
        return currentNode.value;
      }
      currentNode = currentNode.next;
    }
    return null;
  }
};

HashTable.prototype.retrieveAll = function() {
  var allValues = [];
  for (var i = 0; i < this.numBuckets; i++) {
    var currentNode = this.buckets[i];
    while (currentNode) {
      allValues.push(currentNode.value);
      currentNode = currentNode.next;
    }
  }
  return allValues;
};

var myHT = new HashTable(30);

myHT.insert('dean', 'dean@gmail.com');
myHT.insert('megan', 'megan@gmail.com');
myHT.insert('dave', 'dave@gmail.com');
myHT.insert('jane', 'jane@gmail.com');
myHT.insert('mike', 'mike@gmail.com');
myHT.insert('sarah', 'sarah@gmail.com');
myHT.insert('john', 'john@gmail.com');

console.log(myHT.retrieveAll());
// ['dean@gmail.com', 'megan@gmail.com', 'dave@gmail.com', 'jane@gmail.com', 'mike@gmail.com', 'sarah@gmail.com', 'john@gmail.com']
```

위의 코드 예제에서는 HashTable 클래스와 HashNode 클래스를 만들었습니다. HashTable 클래스에는 배열을 초기화하는 데 사용되는 크기 속성이 있습니다. 또한 배열 크기를 저장하는 데 사용되는 numBuckets 속성도 있습니다.

HashNode 클래스에는 키, 값 및 다음 속성이 있습니다. 키는 노드의 키를 저장하는 데 사용되고 값은 노드의 값을 저장하는 데 사용되며 next 속성은 연결 목록의 다음 노드를 저장하는 데 사용됩니다.

HashTable 클래스에는 키를 가져와 배열의 위치에 매핑하는 해시 함수가 있습니다. 위치를 버킷이라고 합니다. 버킷은 단순히 배열 인덱스입니다.

HashTable 클래스에는 키와 값을 받는 삽입 함수도 있습니다. 해시 함수를 사용하여 주어진 키에 대한 버킷을 계산합니다. 버킷이 비어 있으면 새 HashNode를 생성하여 버킷에 저장합니다. 버킷이 비어 있지 않으면 키가 이미 있는지 확인합니다. 키가 있으면 값을 업데이트합니다. 키가 없으면 연결된 목록의 끝에 새 HashNode를 추가합니다.

HashTable 클래스에는 키를 가져와서 주어진 키에 대한 값을 반환하는 get 함수도 있습니다. 키가 없으면 null을 반환합니다.

HashTable 클래스에는 해시 테이블의 모든 값 배열을 반환하는 retrieveAll 함수도 있습니다.

## 운동

1. 좋아하는 프로그래밍 언어로 해시 테이블을 구현합니다.

2. 키와 값을 가져와 해시 테이블에 삽입하는 함수를 작성합니다.

3. 키를 받아서 주어진 키에 대한 값을 반환하는 함수를 작성합니다.

4. 해시 테이블에 있는 모든 값의 배열을 반환하는 함수를 작성합니다.