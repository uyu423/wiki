---
title: [JavaScript] 031: 선택 정렬
description: 
published: true
date: 2023-02-10T09:32:32.096Z
tags: 
editor: markdown
dateCreated: 2023-02-10T09:32:30.417Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 031: Selection Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-031-selection-sort)
{.links-list}


# JavaScript 031: 선택 정렬

선택 정렬은 정렬 알고리즘, 특히 내부 비교 정렬입니다. O(n2) 시간 복잡도를 가지므로 큰 목록에서 비효율적이며 일반적으로 비슷한 삽입 정렬보다 성능이 떨어집니다. 선택 정렬은 단순함으로 유명하며 특정 상황, 특히 보조 메모리가 제한된 경우 더 복잡한 알고리즘보다 성능 이점이 있습니다.

알고리즘은 입력 목록을 두 부분으로 나눕니다. 목록의 앞(왼쪽)에서 왼쪽에서 오른쪽으로 이미 정렬된 항목의 하위 목록과 나머지를 차지하는 정렬할 항목의 하위 목록입니다. 목록. 처음에 정렬된 하위 목록은 비어 있고 정렬되지 않은 하위 목록은 전체 입력 목록입니다. 알고리즘은 정렬되지 않은 하위 목록에서 가장 작은(또는 정렬 순서에 따라 가장 큰) 요소를 찾아 가장 왼쪽의 정렬되지 않은 요소와 교환(교환)하고(정렬된 순서로 배치) 하위 목록 경계를 오른쪽으로 한 요소 이동하여 진행합니다. .

## 코드 예제

```javascript
function selectionSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    let min = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[min]) {
        min = j;
      }
    }
    if (i !== min) {
      [arr[i], arr[min]] = [arr[min], arr[i]];
    }
  }
  return arr;
}
```

## 선택 정렬 의사 코드

```
procedure selectionSort( A : list of sortable items )
   n = length(A)
   for i = 1 to n - 1
   /* set current element as minimum*/
      minIndex = i    
   /* check the element to be minimum */
 
      for j = i+1 to n      
         if A[j] < A[minIndex]   
            minIndex = j;
      end if
   end for
   /* swap the minimum element with the current element*/
   if indexMin != i  then
      swap A[minIndex] with A[i]
   end if
   end for
end procedure
```

## 선택 정렬 시각화

![선택 정렬 시각화](https://upload.wikimedia.org/wikipedia/commons/9/94/Selection-Sort-Animation.gif)

## 선택 정렬 복잡도

선택 정렬의 시간 복잡도는 O(n2)입니다. 즉, 최악의 시나리오에서 알고리즘은 n개의 요소 목록을 정렬하기 위해 n2단계를 수행합니다.

## 관련 연습

- [연습 1](https://repl.it/@ezekielelin/Selection-Sort# index.js) : 자바스크립트로 선택 정렬 구현하기
- [연습 2](https://repl.it/@ezikielelin/Selection-Sort-Optimized# index.js): 거의 정렬된 데이터에 대한 선택 정렬 최적화

## 답변

- [답변 1](https://repl.it/@ezekiellin/Selection-Sort-Answer# index.js)
- [답변 2](https://repl.it/@ezekiellin/Selection-Sort-Optimized-Answer# index.js)