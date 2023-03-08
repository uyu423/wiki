---
title: [JavaScript] 034: 힙 정렬
description: 
published: true
date: 2023-02-10T12:32:35.020Z
tags: 
editor: markdown
dateCreated: 2023-02-10T12:32:33.484Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 034: Heap Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-034-heap-sort)
{.links-list}


# 힙 정렬

힙 정렬은 비교 기반 정렬 알고리즘입니다. 힙 정렬은 개선된 선택 정렬로 생각할 수 있습니다. 선택 정렬과 마찬가지로 힙 정렬은 입력을 정렬된 영역과 정렬되지 않은 영역으로 나누고 가장 큰 요소를 추출하여 정렬된 영역에 삽입하여 정렬되지 않은 영역을 반복적으로 축소합니다. 개선 사항은 최대값을 찾기 위해 선형 시간 검색이 아닌 힙 데이터 구조를 사용하는 것입니다.

Heapsort는 제자리 알고리즘이지만 안정적인 정렬은 아닙니다.

## 알고리즘

힙은 자식 노드가 부모 노드에 대한 정렬 순서를 갖는 트리와 같은 데이터 구조입니다. 힙에는 최소 힙과 최대 힙의 두 가지 유형이 있습니다. 최소 힙에서 루트 노드의 값은 자식 노드의 값보다 작거나 같습니다. 최대 힙에서 루트 노드의 값은 자식 노드의 값보다 크거나 같습니다.

힙 정렬 알고리즘은 두 부분으로 나눌 수 있습니다.

1. 첫 번째 부분은 입력 배열에서 힙을 구축하는 것과 관련됩니다. 이 단계는 heapify라고도 합니다.
2. 두 번째 부분은 힙에서 요소를 하나씩 추출하여 정렬된 배열에 삽입하는 것입니다.

첫 번째 부분은 최소 힙 또는 최대 힙을 사용하여 수행할 수 있습니다. 이 문서에서는 최대 힙을 사용합니다.

heapify 알고리즘은 루트 노드에서 시작하여 트리 아래로 이동하여 현재 노드의 값을 자식 노드의 값과 비교합니다. 현재 노드의 값이 자식 노드의 값보다 작으면 두 노드를 교환합니다. 이 프로세스는 현재 노드가 두 자식 노드보다 크거나 같을 때까지(또는 트리의 맨 아래에 도달할 때까지) 반복됩니다.

알고리즘의 두 번째 부분은 반복적으로 힙에서 최대 요소를 추출하여 정렬된 배열에 삽입하는 것입니다. 이는 힙의 루트 노드를 배열의 마지막 요소로 교체한 다음 트리를 힙화하여 수행됩니다. 이 프로세스는 힙이 비워질 때까지 반복됩니다.

## 복잡성

heapify의 시간 복잡도는 O(log n)이고 전체 힙 정렬 알고리즘의 시간 복잡도는 O(n log n)입니다.

## 코드 예

다음은 힙 정렬 알고리즘의 C++ 구현입니다.

```C++
#include <iostream>
#include <vector>

using namespace std;

void heapify(vector<int>& A, int n, int i)
{
    int largest = i;
    int l = 2*i + 1;
    int r = 2*i + 2;

    if (l < n && A[l] > A[largest])
        largest = l;

    if (r < n && A[r] > A[largest])
        largest = r;

    if (largest != i)
    {
        swap(A[i], A[largest]);
        heapify(A, n, largest);
    }
}

void heapSort(vector<int>& A, int n)
{
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(A, n, i);

    for (int i=n-1; i>=0; i--)
    {
        swap(A[0], A[i]);
        heapify(A, i, 0);
    }
}

int main()
{
    vector<int> A = {4, 10, 3, 5, 1};
    int n = A.size();

    heapSort(A, n);

    for (int i=0; i<n; ++i)
        cout << A[i] << " ";

    return 0;
}
```

## 운동

1. 선택한 프로그래밍 언어로 heapify 및 heapSort 알고리즘을 구현합니다.

2. heapify 알고리즘을 사용하여 다음 배열에서 최대 힙을 만듭니다.

```
[4, 10, 3, 5, 1]
```

3. heapSort 알고리즘을 사용하여 다음 배열을 정렬합니다.

```
[4, 10, 3, 5, 1]
```

4. heapify 및 heapSort 알고리즘의 시간 복잡도는 얼마입니까?

5. heapify 및 heapSort 알고리즘의 공간 복잡성은 무엇입니까?