---
title: [C언어] 034: 힙정렬
description: 
published: true
date: 2023-02-13T14:33:07.379Z
tags: 
editor: markdown
dateCreated: 2023-02-13T14:33:05.783Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 034: Heap Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-034-heap-sort)
{.links-list}


# 034: 힙 정렬

힙 정렬은 비교 기반 정렬 알고리즘입니다. 힙 정렬은 개선된 선택 정렬로 생각할 수 있습니다. 해당 알고리즘과 마찬가지로 입력을 정렬된 영역과 정렬되지 않은 영역으로 나누고 가장 큰 요소를 추출하여 정렬된 영역으로 이동하여 정렬되지 않은 영역을 반복적으로 축소합니다. 개선 사항은 최대값을 찾기 위해 선형 시간 검색이 아닌 힙 데이터 구조를 사용하는 것입니다.

Heapsort는 J. W. J. Williams가 1964년에 발명했습니다.[1] Heapsort는 제자리 알고리즘이지만 안정적인 정렬은 아닙니다.

## 알고리즘

이진 힙은 이진 트리 형식을 취하는 힙 데이터 구조입니다. 이진 힙은 우선 순위 대기열을 구현하는 일반적인 방법입니다.

이진 힙은 두 가지 추가 제약 조건이 있는 이진 트리로 정의됩니다.

* 모양 속성: 트리는 완전한 이진 트리입니다. 즉, 마지막 레벨(가장 깊은)을 제외하고 트리의 모든 레벨이 완전히 채워지고, 트리의 마지막 레벨이 완료되지 않은 경우 해당 레벨의 노드가 왼쪽에서 오른쪽으로 채워집니다.
* 힙 속성: 각 노드는 힙에 대해 정의된 비교 조건자에 따라 각 자식보다 크거나 같습니다.

힙 속성을 사용하면 루트 노드에 빠르게 액세스할 수 있습니다. 트리에서 가장 큰(또는 가장 작은) 요소임이 보장됩니다.

알고리즘에는 힙 구성과 정렬의 두 단계가 있습니다.

### 힙 건설

힙 구성 단계는 정렬되지 않은 숫자 배열로 시작하여 이진 힙으로 변환합니다. 배열은 이진 트리로 나타낼 수 있으며 각 노드는 배열의 요소에 해당하고 각 노드의 자식은 노드의 요소보다 큰(또는 작은) 배열의 요소입니다.

첫 번째 단계는 어레이에서 힙을 만드는 것입니다. 힙 구성 알고리즘은 다음과 같습니다.

1. 빈 힙에서 시작합니다.

2. 배열의 각 요소를 임의의 순서로 힙에 삽입합니다.

3. 힙이 비어 있지 않은 동안:

    ㅏ. 힙의 맨 위 요소를 제거하십시오.

    비. 정렬된 배열에 요소를 삽입합니다.

4. 정렬된 배열을 반환합니다.

힙 구성 단계의 시간 복잡도는 O(n)이며 여기서 n은 배열의 요소 수입니다.

### 정렬

정렬 단계는 이진 힙에서 시작하여 정렬된 배열로 변환합니다. 정렬 알고리즘은 다음과 같습니다.

1. 힙이 비어 있지 않은 동안:

    ㅏ. 힙의 맨 위 요소를 제거하십시오.

    비. 정렬된 배열에 요소를 삽입합니다.

2. 정렬된 배열을 반환합니다.

정렬 단계의 시간 복잡도는 O(nlog(n))입니다. 여기서 n은 배열의 요소 수입니다. 이는 while 루프가 반복될 때마다 힙의 맨 위 요소가 제거되고 heapify 작업이 수행되기 때문입니다. heapify 작업은 O(log(n)) 시간이 걸리고 while 루프가 n회 반복되므로 총 시간 복잡도는 O(nlog(n))입니다.

## 코드 예시

다음은 C 프로그래밍 언어로 구현된 힙 정렬입니다.

```c
#include <stdio.h>
#include <stdlib.h>

void heapify(int* array, int size, int i)
{
    int largest = i;
    int left = 2*i + 1;
    int right = 2*i + 2;

    if (left < size && array[left] > array[largest])
        largest = left;

    if (right < size && array[right] > array[largest])
        largest = right;

    if (largest != i)
    {
        int temp = array[i];
        array[i] = array[largest];
        array[largest] = temp;

        heapify(array, size, largest);
    }
}

void heap_sort(int* array, int size)
{
    for (int i = size / 2 - 1; i >= 0; i--)
        heapify(array, size, i);

    for (int i = size - 1; i >= 0; i--)
    {
        int temp = array[0];
        array[0] = array[i];
        array[i] = temp;

        heapify(array, i, 0);
    }
}

int main()
{
    int array[] = {3, 2, 1, 5, 4};
    int size = sizeof(array) / sizeof(array[0]);

    heap_sort(array, size);

    for (int i = 0; i < size; i++)
        printf("%d ", array[i]);
    printf("\n");

    return 0;
}
```

## 운동

1. 힙 정렬 알고리즘에서 heapify 작업을 구현합니다.

2. 힙 정렬 알고리즘을 구현합니다.

3. 힙 정렬 알고리즘과 선택 정렬 알고리즘의 실행 시간을 비교하십시오.

## 답변

1. heapify 작업은 다음과 같이 구현할 수 있습니다.

```c
void heapify(int* array, int size, int i)
{
    int largest = i;
    int left = 2*i + 1;
    int right = 2*i + 2;

    if (left < size && array[left] > array[largest])
        largest = left;

    if (right < size && array[right] > array[largest])
        largest = right;

    if (largest != i)
    {
        int temp = array[i];
        array[i] = array[largest];
        array[largest] = temp;

        heapify(array, size, largest);
    }
}
```

2. 힙 정렬 알고리즘은 다음과 같이 구현할 수 있습니다.

```c
void heap_sort(int* array, int size)
{
    for (int i = size / 2 - 1; i >= 0; i--)
        heapify(array, size, i);

    for (int i = size - 1; i >= 0; i--)
    {
        int temp = array[0];
        array[0] = array[i];
        array[i] = temp;

        heapify(array, i, 0);
    }
}
```

3. 힙 정렬 알고리즘의 실행 시간은 O(nlog(n))이고 선택 정렬 알고리즘의 실행 시간은 O(n^2)입니다.