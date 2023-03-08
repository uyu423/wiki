---
title: [C언어] 032: 병합 정렬
description: 
published: true
date: 2023-02-13T12:34:00.279Z
tags: 
editor: markdown
dateCreated: 2023-02-13T12:33:58.549Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 032: Merge Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-032-merge-sort)
{.links-list}


# 032: 병합 정렬

병합 정렬은 분할 정복 전략을 사용하는 정렬 알고리즘입니다. 시간 복잡도가 O(n log n)인 가장 효율적인 정렬 알고리즘 중 하나입니다.

병합 정렬 알고리즘은 배열을 두 개의 절반으로 나누고 각 절반을 정렬한 다음 두 절반을 함께 병합하는 방식으로 작동합니다. 병합 단계는 병합 정렬 알고리즘에서 가장 중요한 부분입니다.

## 병합 단계는 어떻게 작동합니까?

병합 단계는 두 개의 정렬된 배열을 가져와 단일 정렬된 배열로 병합하는 방식으로 작동합니다. 병합 단계는 병합 정렬 알고리즘에서 가장 중요한 부분입니다.

두 개의 정렬된 배열을 병합하려면 병합 알고리즘이라는 간단한 알고리즘을 사용할 수 있습니다. 병합 알고리즘은 두 개의 정렬된 배열을 가져와서 하나의 정렬된 배열로 병합하는 방식으로 작동합니다.

병합 알고리즘은 각 배열의 첫 번째 요소를 비교하여 작동합니다. 그런 다음 두 요소 중 더 작은 요소가 병합된 배열에 추가됩니다. 그런 다음 병합 알고리즘은 어레이 중 하나가 비워질 때까지 이 프로세스를 반복합니다. 그런 다음 다른 배열의 나머지 요소가 병합된 배열에 추가됩니다.

## 코드 예시

다음은 C에서 병합 정렬 알고리즘을 간단하게 구현한 것입니다.

```c
#include <stdio.h>
#include <stdlib.h>
 
void merge(int *array, int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
 
    int L[n1], R[n2];
 
    for (i = 0; i < n1; i++)
        L[i] = array[l + i];
    for (j = 0; j < n2; j++)
        R[j] = array[m + 1+ j];
 
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            array[k] = L[i];
            i++;
        }
        else
        {
            array[k] = R[j];
            j++;
        }
        k++;
    }
 
    while (i < n1)
    {
        array[k] = L[i];
        i++;
        k++;
    }
 
    while (j < n2)
    {
        array[k] = R[j];
        j++;
        k++;
    }
}
 
void mergeSort(int *array, int l, int r)
{
    if (l < r)
    {
        int m = l+(r-l)/2;
 
        mergeSort(array, l, m);
        mergeSort(array, m+1, r);
 
        merge(array, l, m, r);
    }
}
 
int main()
{
    int array[] = {12, 11, 13, 5, 6, 7};
    int array_size = sizeof(array)/sizeof(array[0]);
 
    printf("Given array is \n");
    printArray(array, array_size);
 
    mergeSort(array, 0, array_size - 1);
 
    printf("\nSorted array is \n");
    printArray(array, array_size);
    return 0;
}
```

## 운동

1. 좋아하는 프로그래밍 언어로 병합 정렬 알고리즘을 구현합니다.

2. 병합 정렬 알고리즘을 사용하여 정수 배열을 오름차순으로 정렬합니다.

3. 병합 정렬 알고리즘을 사용하여 문자열 배열을 사전순으로 정렬합니다.

## 답변

1.

```c
#include <stdio.h>
#include <stdlib.h>
 
void merge(int *array, int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
 
    int L[n1], R[n2];
 
    for (i = 0; i < n1; i++)
        L[i] = array[l + i];
    for (j = 0; j < n2; j++)
        R[j] = array[m + 1+ j];
 
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            array[k] = L[i];
            i++;
        }
        else
        {
            array[k] = R[j];
            j++;
        }
        k++;
    }
 
    while (i < n1)
    {
        array[k] = L[i];
        i++;
        k++;
    }
 
    while (j < n2)
    {
        array[k] = R[j];
        j++;
        k++;
    }
}
 
void mergeSort(int *array, int l, int r)
{
    if (l < r)
    {
        int m = l+(r-l)/2;
 
        mergeSort(array, l, m);
        mergeSort(array, m+1, r);
 
        merge(array, l, m, r);
    }
}
 
int main()
{
    int array[] = {12, 11, 13, 5, 6, 7};
    int array_size = sizeof(array)/sizeof(array[0]);
 
    printf("Given array is \n");
    printArray(array, array_size);
 
    mergeSort(array, 0, array_size - 1);
 
    printf("\nSorted array is \n");
    printArray(array, array_size);
    return 0;
}
```

2.

```c
#include <stdio.h>
#include <stdlib.h>
 
void merge(int *array, int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
 
    int L[n1], R[n2];
 
    for (i = 0; i < n1; i++)
        L[i] = array[l + i];
    for (j = 0; j < n2; j++)
        R[j] = array[m + 1+ j];
 
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            array[k] = L[i];
            i++;
        }
        else
        {
            array[k] = R[j];
            j++;
        }
        k++;
    }
 
    while (i < n1)
    {
        array[k] = L[i];
        i++;
        k++;
    }
 
    while (j < n2)
    {
        array[k] = R[j];
        j++;
        k++;
    }
}
 
void mergeSort(int *array, int l, int r)
{
    if (l < r)
    {
        int m = l+(r-l)/2;
 
        mergeSort(array, l, m);
        mergeSort(array, m+1, r);
 
        merge(array, l, m, r);
    }
}
 
int main()
{
    int array[] = {12, 11, 13, 5, 6, 7};
    int array_size = sizeof(array)/sizeof(array[0]);
 
    printf("Given array is \n");
    printArray(array, array_size);
 
    mergeSort(array, 0, array_size - 1);
 
    printf("\nSorted array is \n");
    printArray(array, array_size);
    return 0;
}
```

삼.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
 
void merge(char **array, int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
 
    char **L = malloc(sizeof(char*)*n1);
    char **R = malloc(sizeof(char*)*n2);
 
    for (i = 0; i < n1; i++)
        L[i] = array[l + i];
    for (j = 0; j < n2; j++)
        R[j] = array[m + 1+ j];
 
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (strcmp(L[i], R[j]) <= 0)
        {
            array[k] = L[i];
            i++;
        }
        else
        {
            array[k] = R[j];
            j++;
        }
        k++;
    }
 
    while (i < n1)
    {
        array[k] = L[i];
        i++;
        k++;
    }
 
    while (j < n2)
    {
        array[k] = R[j];
        j++;
        k++;
    }
 
    free(L);
    free(R);
}
 
void mergeSort(char **array, int l, int r)
{
    if (l < r)
    {
        int m = l+(r-l)/2;
 
        mergeSort(array, l, m);
        mergeSort(array, m+1, r);
 
        merge(array, l, m, r);
    }
}
 
int main()
{
    char *array[] = {"c", "a", "e", "b", "d"};
    int array_size = sizeof(array)/sizeof(array[0]);
 
    printf("Given array is \n");
    printArray(array, array_size);
 
    mergeSort(array, 0, array_size - 1);
 
    printf("\nSorted array is \n");
    printArray(array, array_size);
    return 0;
}
```