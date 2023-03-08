---
title: [JavaScript] 033: 빠른 정렬
description: 
published: true
date: 2023-02-10T11:32:29.339Z
tags: 
editor: markdown
dateCreated: 2023-02-10T11:32:27.715Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 033: Quick Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-033-quick-sort)
{.links-list}


# JavaScript 033: 빠른 정렬

빠른 정렬 알고리즘은 배열을 두 개의 하위 배열로 분할한 다음 하위 배열을 재귀적으로 정렬하여 배열을 정렬하는 정렬 알고리즘입니다. 이 알고리즘은 배열을 정렬하는 방식에서 이름을 얻습니다. 배열을 두 개의 하위 배열로 분할한 다음 빠른 정렬 알고리즘을 재귀적으로 적용하여 하위 배열을 "빠르게" 정렬합니다.

빠른 정렬 알고리즘은 일반적으로 재귀를 사용하여 구현됩니다. 재귀의 기본 사례는 정렬할 배열의 길이가 1 또는 0인 경우입니다. 이 경우 배열은 이미 정렬되어 있습니다. 그렇지 않으면 배열이 두 개의 하위 배열로 분할되고 빠른 정렬 알고리즘이 각 하위 배열에 재귀적으로 적용됩니다.

퀵 정렬 알고리즘은 평균적으로 O(n log n)의 시간 복잡도와 O(log n)의 공간 복잡도를 갖는다. 그러나 퀵 정렬 알고리즘의 최악의 경우 시간 복잡도는 O(n^2)입니다.

## 코드 예

다음은 JavaScript에서 빠른 정렬 알고리즘의 코드 예제입니다.

```javascript
function quickSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const pivot = arr[arr.length - 1];
  const left = [];
  const right = [];

  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  return [...quickSort(left), pivot, ...quickSort(right)];
}
```

## 운동

다음은 퀵 정렬 알고리즘에 대한 이해도를 테스트하기 위한 연습입니다.

```javascript
// Write a function that sorts an array using the quick sort algorithm.

function quickSort(arr) {
  // Your code here
}
```

## 응답 코드

다음은 연습의 응답 코드입니다.

```javascript
function quickSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const pivot = arr[arr.length - 1];
  const left = [];
  const right = [];

  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  return [...quickSort(left), pivot, ...quickSort(right)];
}
```

## 해설

퀵 정렬 알고리즘은 평균적으로 시간 복잡도가 O(n log n)인 매우 효율적인 정렬 알고리즘입니다. 그러나 퀵 정렬 알고리즘의 최악의 경우 시간 복잡도는 O(n^2)입니다. 따라서 빠른 정렬 알고리즘은 모든 경우에 사용할 수 있는 최상의 정렬 알고리즘이 아닙니다.