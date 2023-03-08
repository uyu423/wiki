---
title: [JavaScript] 032: 병합 정렬
description: 
published: true
date: 2023-02-10T10:32:29.133Z
tags: 
editor: markdown
dateCreated: 2023-02-10T10:32:27.482Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 032: Merge Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-032-merge-sort)
{.links-list}


# JavaScript 032: 병합 정렬

병합 정렬은 분할 정복 전략을 사용하는 정렬 알고리즘입니다. 배열을 더 작은 하위 배열로 나눈 다음 해당 하위 배열을 다시 정렬하고 병합하여 작동하는 재귀 알고리즘입니다.

병합 정렬 알고리즘은 다음과 같이 의사 코드로 작성할 수 있습니다.

```
function mergeSort(array)
  if array.length <= 1
    return array
  end
 
  middle = array.length / 2
  left = array.slice(0, middle)
  right = array.slice(middle)
 
  return merge(
    mergeSort(left),
    mergeSort(right)
  )
end
 
function merge(left, right)
  result = []
 
  while left.length && right.length
    if left[0] <= right[0]
      result.push(left.shift())
    else
      result.push(right.shift())
    end
  end
 
  return result.concat(left, right)
end
```

병합 정렬 알고리즘의 시간 복잡도는 O(n log n)입니다. 이는 배열이 각 단계에서 반으로 나뉘고 O(log n) 단계가 있기 때문입니다. 각 단계에는 시간 복잡도가 O(n)인 병합 작업도 포함됩니다.

병합 정렬 알고리즘의 공간 복잡도는 O(n)입니다. 이는 각 단계에서 정렬된 하위 배열을 저장하기 위해 새 배열이 생성되기 때문입니다.

## 코드 예

다음은 JavaScript로 작성된 병합 정렬 알고리즘의 예입니다.

```javascript
function mergeSort(array) {
  if (array.length <= 1) {
    return array;
  }
 
  const middle = Math.floor(array.length / 2);
  const left = array.slice(0, middle);
  const right = array.slice(middle);
 
  return merge(
    mergeSort(left),
    mergeSort(right)
  );
}
 
function merge(left, right) {
  const result = [];
 
  while (left.length && right.length) {
    if (left[0] <= right[0]) {
      result.push(left.shift());
    } else {
      result.push(right.shift());
    }
  }
 
  return result.concat(left, right);
}
 
const array = [5, 3, 2, 1, 4];
console.log(mergeSort(array)); // [1, 2, 3, 4, 5]
```

## 설명

병합 정렬 알고리즘은 배열을 더 작은 하위 배열로 나눈 다음 해당 하위 배열을 다시 정렬하고 병합하는 방식으로 작동합니다.

알고리즘은 배열이 비어 있는지 또는 요소가 하나만 있는지 확인하는 것으로 시작합니다. 그렇다면 배열을 반환합니다.

그렇지 않으면 배열은 각 단계에서 반으로 나뉘며 O(log n) 단계가 있습니다. 각 단계에는 시간 복잡도가 O(n)인 병합 작업도 포함됩니다.

병합 정렬 알고리즘의 공간 복잡도는 O(n)입니다. 이는 각 단계에서 정렬된 하위 배열을 저장하기 위해 새 배열이 생성되기 때문입니다.

## 복잡성 분석

병합 정렬 알고리즘의 시간 복잡도는 O(n log n)입니다. 이는 배열이 각 단계에서 반으로 나뉘고 O(log n) 단계가 있기 때문입니다. 각 단계에는 시간 복잡도가 O(n)인 병합 작업도 포함됩니다.

병합 정렬 알고리즘의 공간 복잡도는 O(n)입니다. 이는 각 단계에서 정렬된 하위 배열을 저장하기 위해 새 배열이 생성되기 때문입니다.