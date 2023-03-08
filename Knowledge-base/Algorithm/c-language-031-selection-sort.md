---
title: [C언어] 031: 선택정렬
description: 
published: true
date: 2023-02-13T11:32:12.533Z
tags: 
editor: markdown
dateCreated: 2023-02-13T11:32:10.894Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 031: Selection Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-031-selection-sort)
{.links-list}


# 031: 선택 정렬

선택 정렬 알고리즘은 정렬되지 않은 부분에서 최소 요소(오름차순 고려)를 반복적으로 찾아 처음에 배치하여 배열을 정렬합니다. 알고리즘은 주어진 배열에서 두 개의 하위 배열을 유지합니다.

1) 이미 정렬된 하위 배열.
2) 정렬되지 않은 나머지 하위 배열.

선택 정렬의 모든 반복에서 정렬되지 않은 하위 배열의 최소 요소(오름차순 고려)가 선택되어 정렬된 하위 배열로 이동됩니다.

## 의사 코드

```
procedure selectionSort( A : array of items )
   n = length(A)
   for i = 0 to n-1 do
      /* find the minimum element in the unsorted array */
       
      /* swap the found minimum element with the first element */
     
   done
```

## 복잡성

### 시간 복잡도

최상의 경우: Ω(n^2)

평균 케이스: Θ(n^2)

최악의 경우: O(n^2)

### 공간 복잡성

최악의 경우: O(1)