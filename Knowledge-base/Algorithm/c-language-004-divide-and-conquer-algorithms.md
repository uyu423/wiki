---
title: [C언어] 004: 분할정복 알고리즘
description: 
published: true
date: 2023-02-12T15:32:19.056Z
tags: 
editor: markdown
dateCreated: 2023-02-12T15:32:17.491Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 004: Divide and Conquer Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/c-language-004-divide-and-conquer-algorithms)
{.links-list}


# C언어] 004: 분할정복 알고리즘

분할 정복 알고리즘은 문제 해결을 위한 강력한 도구입니다. 문제를 더 작은 하위 문제로 나누면 문제를 보다 효율적으로 해결할 수 있습니다.

많은 분할 정복 알고리즘이 있지만 가장 인기 있는 두 가지인 병합 정렬과 빠른 정렬에 중점을 둘 것입니다.

## 병합 정렬

병합 정렬은 문제를 더 작은 하위 문제로 나눈 다음 이러한 하위 문제에 대한 솔루션을 결합하여 작동하는 재귀 알고리즘입니다.

병합 정렬은 배열을 반으로 나누고 각 반을 정렬한 다음 두 반쪽을 병합하는 방식으로 작동합니다. 병합 단계는 병합 정렬의 핵심입니다. 두 반쪽을 병합하려면 각 반쪽의 요소를 비교한 다음 올바른 순서로 배치해야 합니다.

병합 정렬의 의사 코드 구현은 다음과 같습니다.

```
def merge_sort(array):
    if len(array) <= 1:
        return array
    
    # split the array in half
    mid = len(array) // 2
    left = array[:mid]
    right = array[mid:]
    
    # sort each half
    left = merge_sort(left)
    right = merge_sort(right)
    
    # merge the halves together
    return merge(left, right)
    
def merge(left, right):
    result = []
    
    while len(left) > 0 and len(right) > 0:
        if left[0] <= right[0]:
            result.append(left[0])
            left = left[1:]
        else:
            result.append(right[0])
            right = right[1:]
            
    # either left or right may have elements left
    while len(left) > 0:
        result.append(left[0])
        left = left[1:]
        
    while len(right) > 0:
        result.append(right[0])
        right = right[1:]
        
    return result
```

병합 정렬은 시간 복잡도가 O(n log n)인 강력한 정렬 알고리즘입니다. 그러나 가장 빠른 정렬 알고리즘은 아닙니다.

## 퀵 정렬

퀵 정렬은 널리 사용되는 또 다른 분할 정복 알고리즘입니다. 빠른 정렬은 피벗 요소를 선택한 다음 피벗을 중심으로 배열을 분할하여 작동합니다. 피벗보다 작은 요소는 하나의 배열에 배치되고 피벗보다 큰 요소는 다른 배열에 배치됩니다. 그런 다음 빠른 정렬은 두 배열을 재귀적으로 정렬합니다.

다음은 빠른 정렬의 의사 코드 구현입니다.

```
def quick_sort(array):
    if len(array) <= 1:
        return array
    
    # select a pivot element
    pivot = array[len(array) // 2]
    
    # partition the array around the pivot
    left = []
    right = []
    
    for element in array:
        if element < pivot:
            left.append(element)
        elif element > pivot:
            right.append(element)
        else:
            # element is equal to the pivot, so we can leave it in the array
            pass
    
    # sort the left and right arrays
    left = quick_sort(left)
    right = quick_sort(right)
    
    # merge the arrays back together
    return left + [pivot] + right
```

퀵 정렬은 시간 복잡도가 O(n log n)인 빠른 정렬 알고리즘입니다.

## 결론

분할 정복 알고리즘은 문제 해결을 위한 강력한 도구입니다. 병합 정렬과 빠른 정렬은 가장 널리 사용되는 분할 정복 알고리즘 중 두 가지입니다.