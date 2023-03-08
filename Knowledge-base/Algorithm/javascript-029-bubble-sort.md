---
title: [JavaScript] 029: 버블 정렬
description: 
published: true
date: 2023-02-10T07:32:37.190Z
tags: 
editor: markdown
dateCreated: 2023-02-10T07:32:30.681Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 029: Bubble Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-029-bubble-sort)
{.links-list}


# 버블 정렬

버블 정렬은 정렬할 목록을 반복적으로 단계별로 실행하고 인접한 항목의 각 쌍을 비교하고 순서가 잘못된 경우 교환하는 간단한 정렬 알고리즘입니다. 목록을 통한 전달은 교체가 필요하지 않을 때까지 반복되며, 이는 목록이 정렬되었음을 나타냅니다. 이 알고리즘은 작거나 큰 요소가 목록의 맨 위로 "버블"하는 방식에서 이름을 얻습니다.

버블 정렬은 일반적으로 가장 간단한 정렬 알고리즘으로 간주됩니다. 그러나 큰 목록에는 상대적으로 비효율적이기도 합니다. 하지만 상대적으로 작은 목록에는 잘 작동합니다.

## 개념

버블 정렬은 목록의 각 요소를 옆에 있는 요소와 비교하고 순서가 잘못된 경우 교환하는 방식으로 작동합니다. 모든 요소가 정렬될 때까지 프로세스가 반복됩니다.

예를 들어 다음과 같은 목록이 있다고 가정해 보겠습니다.

```
[5, 1, 4, 2, 8]
```

먼저 처음 두 요소인 `5`와 `1`을 비교하고 `5`가 `1`보다 크기 때문에 서로 바꿉니다. 그러면 목록이 다음과 같이 표시됩니다.

```
[1, 5, 4, 2, 8]
```

그런 다음 다음 두 요소인 `5`와 `4`를 비교하고 `5`가 `4`보다 크지 않기 때문에 동일한 순서로 둡니다. 그러면 목록이 다음과 같이 표시됩니다.

```
[1, 5, 4, 2, 8]
```

그런 다음 다음 두 요소인 `4`와 `2`를 비교하고 `4`가 `2`보다 크기 때문에 서로 바꿉니다. 그러면 목록이 다음과 같이 표시됩니다.

```
[1, 5, 2, 4, 8]
```

마지막으로 마지막 두 요소인 `4`와 `8`을 비교하고 `4`가 `8`보다 크지 않기 때문에 동일한 순서로 둡니다. 그러면 목록이 다음과 같이 표시됩니다.

```
[1, 5, 2, 4, 8]
```

마지막 패스에서 스왑을 수행할 필요가 없었기 때문에 이제 목록이 정렬되었다고 결론을 내릴 수 있습니다.

## 코드 예

다음은 JavaScript에서 버블 정렬을 간단하게 구현한 것입니다.

```javascript
function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        // swap
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```

## 복잡성

버블 정렬의 시간 복잡도는 최악의 경우 **O(n^2)**이고 최상의 경우 **O(n)**입니다. 목록이 역순으로 정렬된 경우 최악의 경우가 발생하고 목록이 이미 정렬된 경우 최상의 경우가 발생합니다.

버블 정렬의 공간 복잡도는 **O(1)**입니다. 추가 메모리 공간이 하나만 필요하기 때문입니다.

## 버블 정렬을 사용하는 경우

버블 정렬은 상대적으로 작은 목록을 정렬하는 데 적합합니다. 거의 정렬된 목록을 정렬해야 하는 경우에도 좋은 선택입니다.

## 버블 정렬을 사용하지 말아야 할 때

버블 정렬은 그다지 효율적이지 않기 때문에 큰 목록을 정렬하는 데 적합하지 않습니다. 큰 목록을 정렬해야 하는 경우 다른 정렬 알고리즘을 사용해야 합니다.

## 운동

1. 선택한 프로그래밍 언어로 버블 정렬을 구현합니다.

2. 목록과 정수를 인수로 취하고 거품 정렬을 사용하여 목록을 정렬하는 함수를 작성하십시오. 정수는 정렬이 실행되어야 하는 횟수를 지정해야 합니다.

3. 목록을 인수로 사용하고 목록이 정렬된 경우 'true'를 반환하고 정렬되지 않은 경우 'false'를 반환하는 함수를 작성하세요.

4. 리스트와 함수를 인자로 받아 함수를 이용해 리스트를 정렬하는 함수를 작성하세요. 함수는 두 개의 인수를 가져와서 첫 번째 인수가 두 번째 인수보다 작으면 '-1'을, 두 인수가 같으면 '0'을, 첫 번째 인수가 두 번째 인수보다 크면 '1'을 반환해야 합니다.

## 답변

1.

```javascript
function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        // swap
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```

2.

```javascript
function bubbleSortNTimes(arr, n) {
  for (let i = 0; i < n; i++) {
    bubbleSort(arr);
  }
  return arr;
}
```

삼.

```javascript
function isSorted(arr) {
  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] > arr[i + 1]) {
      return false;
    }
  }
  return true;
}
```

4.

```javascript
function bubbleSortWithComparator(arr, comparator) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (comparator(arr[j], arr[j + 1]) === 1) {
        // swap
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```