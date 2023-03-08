---
title: TypeScript 애플리케이션에서 캐싱 및 성능 최적화 구현
description: 
published: true
date: 2023-02-17T03:55:59.204Z
tags: 
editor: markdown
dateCreated: 2023-02-17T03:55:57.123Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Implementing Caching and Performance Optimization in TypeScript Applications***English** document is available*](/en/Knowledge-base/TypeScript/implementing-caching-and-performance-optimization-in-typescript-applications)
{.links-list}


# TypeScript 애플리케이션에서 캐싱 및 성능 최적화 구현

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 강력한 구성 요소를 구축하는 데 도움이 되는 클래스, 모듈 및 인터페이스를 제공합니다. TypeScript 애플리케이션을 구축할 때 성능을 염두에 두는 것이 중요합니다. 이 가이드는 TypeScript 애플리케이션의 캐싱 및 성능 최적화를 위한 팁과 요령을 제공합니다.

## 캐싱

캐싱은 자주 액세스하는 데이터를 메모리에 저장하여 빠르게 검색할 수 있도록 하는 기술입니다. 캐싱을 올바르게 사용하면 데이터베이스 또는 디스크로의 이동 횟수를 줄여 애플리케이션의 성능을 향상시킬 수 있습니다.

다양한 유형의 캐시가 있으며 각각 고유한 장점과 단점이 있습니다. 예를 들어 인 메모리 캐시는 빠르지만 휘발성이 있으며 애플리케이션이 다시 시작되면 데이터가 손실될 수 있습니다. 디스크 기반 캐시는 느리지만 다시 시작해도 데이터를 유지할 수 있습니다.

사용할 캐시를 결정할 때 다음 요소를 고려하십시오.

- 캐시되는 데이터의 유형
- 데이터의 크기
- 데이터에 액세스하는 빈도
- 데이터의 수명

캐시를 결정했으면 이를 구현해야 합니다. 다음 섹션에서는 이를 수행하는 방법에 대한 몇 가지 팁을 제공합니다.

### 캐싱 라이브러리 사용

TypeScript에 사용할 수 있는 많은 캐싱 라이브러리가 있습니다. 인기 있는 옵션은 다음과 같습니다.

- [memcached](https://www.npmjs.com/package/memcached)
- [redis](https://www.npmjs.com/package/redis)
- [memjs](https://www.npmjs.com/package/memjs)

캐싱 라이브러리를 사용하면 애플리케이션에서 캐싱을 구현하는 프로세스를 단순화할 수 있습니다. 또한 데이터 만료 또는 클러스터 설정과 같은 추가 기능을 제공할 수도 있습니다.

### 캐시에 데이터 저장

캐시를 결정하고 연결을 설정했으면 캐시에 데이터 저장을 시작해야 합니다. 이는 키/값 쌍을 사용하여 수행할 수 있습니다. 키는 데이터를 식별하는 데 사용되며 값은 데이터 자체입니다.

예를 들어 데이터베이스 쿼리 결과를 캐시하려고 한다고 가정해 보겠습니다. 쿼리 결과는 SQL 쿼리를 포함하는 키를 사용하여 캐시에 저장할 수 있습니다. 쿼리가 다시 실행되면 동일한 키를 사용하여 캐시된 결과를 검색할 수 있습니다.

```javascript
var memcache = require('memcache');

var cache = new memcache.Client();
cache.connect();

//Store data in the cache
cache.set('query', 'SELECT * FROM table', function (err) {

  //Data is stored in the cache

});

//Retrieve data from the cache
cache.get('query', function (err, data) {

  //Data is retrieved from the cache

});
```

캐시에 데이터를 저장할 때 좋은 키를 선택하는 것이 중요합니다. 키는 고유하고 설명적이어야 합니다. 또한 생성하기 쉬워야 합니다. 성능에 영향을 미치므로 키 생성에 너무 많은 시간을 소비하고 싶지는 않습니다.

### 데이터 만료

캐시에 데이터를 저장할 때 만료 시간을 설정해야 합니다. 데이터가 자동으로 삭제되기 전에 캐시에 저장되는 시간입니다.

만료 시간은 데이터 액세스 빈도와 데이터 변경 빈도에 따라 선택해야 합니다. 예를 들어 액세스 빈도가 높고 자주 변경되지 않는 데이터는 액세스 빈도가 낮거나 자주 변경되는 데이터보다 만료 시간이 더 길 수 있습니다.

한 번도 액세스하지 않은 데이터에는 짧은 만료 시간이 지정되거나 만료 시간이 전혀 지정되지 않을 수 있습니다. 이렇게 하면 데이터가 불필요하게 캐시 공간을 차지하는 것을 방지할 수 있습니다.

```javascript
var memcache = require('memcache');

var cache = new memcache.Client();
cache.connect();

//Store data in the cache with an expiration time of 60 seconds
cache.set('query', 'SELECT * FROM table', 60, function (err) {

  //Data is stored in the cache

});
```

## 성능 최적화

캐싱 외에도 TypeScript 애플리케이션의 성능을 개선하는 데 사용할 수 있는 다른 기술이 있습니다.

### 올바른 데이터 구조 사용

데이터로 작업할 때 올바른 데이터 구조를 선택하는 것이 중요합니다. 선택한 데이터 구조는 애플리케이션의 성능에 영향을 미칩니다.

예를 들어 많은 양의 데이터로 작업하는 경우 배열을 사용하는 것이 최선의 선택이 아닐 수 있습니다. 어레이가 크면 어레이의 데이터에 액세스하는 속도가 느리기 때문입니다. 이 경우 연결 목록을 대신 사용할 수 있습니다.

```javascript
//Slow when the array is large
var data = [1, 2, 3, 4, 5];

console.log(data[0]); //1
console.log(data[1]); //2

//Faster when the array is large
var data = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five'};

console.log(data[1]); //one
console.log(data[2]); //two
```

### 올바른 알고리즘 사용

코드를 작성할 때 올바른 알고리즘을 선택하는 것이 중요합니다. 선택한 알고리즘은 애플리케이션의 성능에 영향을 미칩니다.

예를 들어 많은 양의 데이터를 정렬해야 하는 경우 거품 정렬 알고리즘을 사용하는 것이 최선의 선택이 아닐 수 있습니다. 데이터가 크면 버블 정렬이 느리기 때문입니다. 이 경우 대신 퀵 정렬 알고리즘을 사용할 수 있습니다.

```javascript
//Slow when the data is large
function bubbleSort(data) {
  for (var i = 0; i < data.length; i++) {
    for (var j = 0; j < data.length - 1; j++) {
      if (data[j] > data[j + 1]) {
        var temp = data[j];
        data[j] = data[j + 1];
        data[j + 1] = temp;
      }
    }
  }
}

//Faster when the data is large
function quickSort(data) {
  if (data.length <= 1) {
    return data;
  }

  var pivot = data[0];
  var left = [];
  var right = [];

  for (var i = 1; i < data.length; i++) {
    if (data[i] <= pivot) {
      left.push(data[i]);
    } else {
      right.push(data[i]);
    }
  }

  return quickSort(left).concat(pivot, quickSort(right));
}
```

### 올바른 도구 사용

TypeScript 애플리케이션을 구축할 때 올바른 도구를 선택하는 것이 중요합니다. 선택한 도구는 애플리케이션의 성능에 영향을 미칩니다.

예를 들어 많은 양의 데이터로 작업하는 경우 TypeScript를 사용하는 것이 최선의 선택이 아닐 수 있습니다. 데이터가 클 때 TypeScript가 느리기 때문입니다. 이 경우 Scala와 같은 대규모 데이터 세트용으로 설계된 언어를 사용할 수 있습니다.

```javascript
//Slow when the data is large
var data = [1, 2, 3, 4, 5];

var sum = 0;

for (var i = 0; i < data.length; i++) {
  sum += data[i];
}

console.log(sum); //15

//Faster when the data is large
val data = Array(1, 2, 3, 4, 5)

var sum = data.reduce(_ + _)

println(sum) //15
```

## 결론

TypeScript는 강력한 애플리케이션을 구축하는 데 사용할 수 있는 강력한 언어입니다. TypeScript 애플리케이션을 구축할 때 성능을 염두에 두는 것이 중요합니다. 이 가이드는 TypeScript 애플리케이션의 캐싱 및 성능 최적화를 위한 팁과 요령을 제공합니다.