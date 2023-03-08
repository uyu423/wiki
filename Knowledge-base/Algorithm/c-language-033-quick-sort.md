---
title: [C언어] 033: 퀵소트
description: 
published: true
date: 2023-02-13T13:32:35.843Z
tags: 
editor: markdown
dateCreated: 2023-02-13T13:32:34.306Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 033: Quick Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-033-quick-sort)
{.links-list}


# 033: 퀵 정렬

빠른 정렬은 배열을 두 개의 하위 배열로 분할한 다음 하위 배열을 재귀적으로 정렬하여 배열을 정렬하는 정렬 알고리즘입니다.

이 알고리즘은 배열에서 피벗 요소를 선택한 다음 피벗보다 작은 모든 요소가 앞에 있고 피벗보다 큰 모든 요소가 뒤에 있도록 피벗을 중심으로 배열을 분할하여 작동합니다. 그런 다음 두 개의 하위 배열이 재귀적으로 정렬됩니다.

퀵 정렬은 분할 정복 알고리즘입니다. 즉, 문제를 더 작은 하위 문제로 나눈 다음 재귀적으로 해결합니다.

퀵 정렬의 시간 복잡도는 구현에 따라 다르지만 최악의 경우는 O(n^2)이고 최상의 경우는 O(n log n)입니다.

## 코드 예

다음은 C로 구현된 빠른 정렬 알고리즘입니다.

```C
void quick_sort(int *arr, int left, int right)
{
    int i, j, pivot, tmp;

    if (left < right) {
        pivot = left;
        i = left;
        j = right;

        while (i < j) {
            while (arr[i] <= arr[pivot] && i <= right) {
                i++;
            }
            while (arr[j] > arr[pivot]) {
                j--;
            }
            if (i <= j) {
                tmp = arr[i];
                arr[i] = arr[j];
                arr[j] = tmp;
                i++;
                j--;
            }
        }

        tmp = arr[pivot];
        arr[pivot] = arr[j];
        arr[j] = tmp;

        quick_sort(arr, left, j - 1);
        quick_sort(arr, j + 1, right);
    }
}
```

## 설명

빠른 정렬 알고리즘은 배열에서 피벗 요소를 선택한 다음 피벗보다 작은 모든 요소가 앞에 있고 피벗보다 큰 모든 요소가 뒤에 있도록 피벗을 중심으로 배열을 분할하여 작동합니다. 그런 다음 두 개의 하위 배열이 재귀적으로 정렬됩니다.

퀵 정렬의 시간 복잡도는 구현에 따라 다르지만 최악의 경우는 O(n^2)이고 최상의 경우는 O(n log n)입니다.

## 관련 연습

1. 좋아하는 프로그래밍 언어로 빠른 정렬을 구현합니다.

2. 다양한 입력에 대한 퀵 정렬과 병합 정렬의 실행 시간을 비교합니다.