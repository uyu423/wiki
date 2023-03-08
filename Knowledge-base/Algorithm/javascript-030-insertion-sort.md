---
title: [JavaScript] 030: 삽입 정렬
description: 
published: true
date: 2023-02-10T08:32:39.338Z
tags: 
editor: markdown
dateCreated: 2023-02-10T08:32:37.748Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 030: Insertion Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-030-insertion-sort)
{.links-list}


# 삽입 정렬

삽입 정렬은 정렬된 배열을 한 번에 한 요소씩 구성하는 정렬 알고리즘입니다. 퀵 정렬, 힙 정렬 또는 병합 정렬과 같은 다른 정렬 알고리즘보다 큰 목록에서 훨씬 덜 효율적입니다. 그러나 삽입 정렬은 다음과 같은 몇 가지 이점을 제공합니다.

간단한 구현: Jon Bentley는 Programming Pearls[2]에서 3줄 C 버전을 보여줍니다.
다른 2차 정렬 알고리즘과 마찬가지로 (상당히) 작은 데이터 세트에 효율적입니다.
선택 정렬이나 버블 정렬보다 효율적입니다.
안정적인; 즉, 동일한 키를 가진 요소의 상대적 순서를 변경하지 않습니다.
제자리; 즉, 추가 메모리 공간의 일정한 양 O(1)만 필요합니다.
온라인; 즉, 목록을 받는 대로 정렬할 수 있습니다.

## 알고리즘

삽입 정렬은 반복될 때마다 하나의 입력 요소를 소비하고 정렬된 출력 목록을 증가시키면서 반복됩니다. 각 반복에서 삽입 정렬은 입력 데이터에서 하나의 요소를 제거하고 정렬된 목록 내에서 해당 요소가 속한 위치를 찾아 거기에 삽입합니다. 입력 요소가 남지 않을 때까지 반복합니다.

정렬은 일반적으로 배열을 반복하고 그 뒤에 정렬된 목록을 확장하여 제자리에서 수행됩니다. 각 배열 위치에서 정렬된 목록의 가장 큰 값(이전 배열 위치에서 옆에 있는 값)과 비교하여 해당 값을 확인합니다. 더 크면 요소를 제자리에 두고 다음으로 이동합니다. 더 작은 경우 정렬된 목록 내에서 올바른 위치를 찾고 더 큰 값을 모두 위로 이동하여 공백을 만들고 올바른 위치에 삽입합니다.

## 복잡성

### 최악의 경우

최악의 경우 입력은 역순으로 정렬된 배열입니다. 크기가 n인 배열을 역순으로 정렬하려면 삽입 정렬이 n^2 비교 및 스왑을 수행해야 합니다. 따라서 최악의 시나리오에 대한 시간 복잡도는 O(n^2)입니다.

### 최고의 사례

최상의 경우 입력은 이미 정렬된 배열입니다. 이 경우 삽입 정렬은 n-1 비교를 수행하지만 스왑은 수행하지 않습니다. 따라서 최상의 시나리오에 대한 시간 복잡도는 O(n)입니다.

## 코드 예제

### 자바스크립트

```javascript
function insertionSort(array) {
  for(let i = 1; i < array.length; i++) {
    let current = array[i];
    let j = i - 1;
    while(j >= 0 && array[j] > current) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = current;
  }
  return array;
}
```

### 파이썬

```python
def insertion_sort(array):
  for i in range(1, len(array)):
    current = array[i]
    j = i - 1
    while j >= 0 and array[j] > current:
      array[j + 1] = array[j]
      j -= 1
    array[j + 1] = current
  return array
```

## 관련 연습

- [ ] 실습 1: 삽입 정렬 구현
- [ ] 연습 2: 삽입 정렬을 사용하여 문자열 배열 정렬

## 답변

- [ ] 답변 1:

```javascript
function insertionSort(array) {
  for(let i = 1; i < array.length; i++) {
    let current = array[i];
    let j = i - 1;
    while(j >= 0 && array[j] > current) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = current;
  }
  return array;
}
```

- [ ] 답변 2:

```javascript
function insertionSort(array) {
  for(let i = 1; i < array.length; i++) {
    let current = array[i];
    let j = i - 1;
    while(j >= 0 && array[j] > current) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = current;
  }
  return array;
}
```