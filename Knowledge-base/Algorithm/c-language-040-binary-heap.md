---
title: [C언어] 040: 바이너리 힙
description: 
published: true
date: 2023-02-13T20:32:18.790Z
tags: 
editor: markdown
dateCreated: 2023-02-13T20:32:17.147Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 040: Binary Heap***English** document is available*](/en/Knowledge-base/Algorithm/c-language-040-binary-heap)
{.links-list}


# 040: 바이너리 힙

이진 힙은 이진 트리 형식을 취하는 힙 데이터 구조입니다. 이진 힙은 두 가지 특수 속성이 있는 이진 트리로 정의됩니다.

1. 트리가 완성되었습니다. 즉, 왼쪽에서 오른쪽으로 채워지는 마지막 수준을 제외하고 트리의 모든 수준이 완전히 채워집니다.
2. 트리가 힙 속성을 충족합니다. 즉, 각 노드는 자식 값보다 크거나 같습니다.

바이너리 힙은 종종 우선 순위 큐를 구현하는 데 사용됩니다. 우선순위 큐는 주어진 우선순위를 가진 요소를 삽입하고 가장 높은 우선순위를 가진 요소를 검색할 수 있게 해주는 데이터 구조입니다.

## 코드 예제

### 삽입

이진 힙에 요소를 삽입하려면 먼저 요소를 힙의 맨 아래 수준에 추가합니다. 그런 다음 요소를 부모와 비교합니다. 요소가 부모보다 크면 두 요소를 교환합니다. 계속해서 요소를 부모와 비교하고 요소가 올바른 위치에 올 때까지 교체합니다.

```c
void insert(int value) {
  // Add the element to the bottom level of the heap.
  heap[size] = value;
  size++;

  // Compare the element to its parent.
  int index = size - 1;
  int parent = (index - 1) / 2;
  while (index > 0 && heap[parent] < heap[index]) {
    // Swap the two elements.
    int temp = heap[parent];
    heap[parent] = heap[index];
    heap[index] = temp;

    // Update the index and parent.
    index = parent;
    parent = (index - 1) / 2;
  }
}
```

### 삭제

이진 힙에서 요소를 삭제하려면 먼저 힙의 맨 위에서 요소를 제거합니다. 그런 다음 요소를 힙의 마지막 요소로 바꿉니다. 마지막으로 요소를 자식 요소와 비교하고 요소가 올바른 위치에 올 때까지 교체합니다.

```c
void delete(int value) {
  // Remove the element from the top of the heap.
  int index = 0;
  heap[index] = heap[size - 1];
  size--;

  // Compare the element to its children.
  int left = 2 * index + 1;
  int right = 2 * index + 2;
  while (left < size && (heap[index] < heap[left] || heap[index] < heap[right])) {
    // Find the largest child.
    int largest = heap[left];
    int largestIndex = left;
    if (right < size && heap[right] > largest) {
      largest = heap[right];
      largestIndex = right;
    }

    // Swap the element with the largest child.
    int temp = heap[index];
    heap[index] = heap[largestIndex];
    heap[largestIndex] = temp;

    // Update the index and children.
    index = largestIndex;
    left = 2 * index + 1;
    right = 2 * index + 2;
  }
}
```

## 운동

1. 선호하는 프로그래밍 언어로 바이너리 힙을 구현합니다.
2. 바이너리 힙 구현을 사용하여 우선 순위 대기열을 구현합니다.
3. 바이너리 힙에서 삽입 및 삭제의 시간 복잡도는 얼마입니까?

## 답변

1. 삽입 및 삭제에 대한 코드 예제를 참조하십시오.
2. 삽입과 삭제의 시간복잡도는 O(log n)이다.