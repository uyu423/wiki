---
title: [JavaScript] 041: 피보나치 힙
description: 
published: true
date: 2023-02-10T19:32:29.820Z
tags: 
editor: markdown
dateCreated: 2023-02-10T19:32:28.109Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 041: Fibonacci Heap***English** document is available*](/en/Knowledge-base/Algorithm/javascript-041-fibonacci-heap)
{.links-list}


# 피보나치 힙

컴퓨터 과학에서 피보나치 힙은 힙 정렬된 트리 모음으로 구성된 우선순위 대기열 작업을 위한 데이터 구조입니다. 이진 힙 및 이항 힙을 포함하여 다른 많은 우선순위 큐 데이터 구조보다 더 나은 상각 실행 시간을 갖습니다. Michael L. Fredman과 Robert E. Tarjan은 1984년에 피보나치 힙을 개발하여 1987년 과학 저널에 발표했습니다.

피보나치 힙은 최소 힙 순서 트리의 모음입니다. 각 노드에는 키라고 하는 연결된 값이 있습니다. min-heap 속성은 다음과 같습니다. 노드의 값은 적어도 자식의 값입니다. 즉, 힙의 루트에 최소 키가 있습니다.

Fibonacci 힙 데이터 구조는 insert 및 extract-min의 두 가지 작업을 지원합니다. 이 두 작업 모두 최악의 경우 O(log n)의 시간 복잡도를 갖습니다.

## 코드 예제

### 삽입

피보나치 힙에 새 키를 삽입하기 위해 키를 사용하여 새 노드를 만들고 루트 목록에 삽입하기만 하면 됩니다. 이 새 노드는 루트 목록의 다른 노드와 관련하여 자동으로 힙 순서가 지정되므로 추가 힙 작업을 수행할 필요가 없습니다.

```javascript
function insert(key) {
    // create a new node with the given key
    var node = new Node(key);
    
    // insert the new node into the root list
    if (this.root == null) {
        this.root = node;
    } else {
        node.next = this.root;
        this.root.prev = node;
        this.root = node;
    }
    
    // update the size of the heap
    this.size++;
}
```

### 추출-분

피보나치 힙에서 최소 키를 추출하기 위해 루트 목록에서 최소 노드를 제거하고 반환하기만 하면 됩니다. 이제 루트 목록이 비어 있을 수 있으므로 새 최소 노드를 찾아 루트로 만들어야 합니다. 또한 동일한 등급의 트리를 쌍으로 연결하여 힙을 통합해야 합니다.

```javascript
function extractMin() {
    // if the heap is empty, return null
    if (this.root == null) {
        return null;
    }
    
    // remove the minimum node from the root list
    var minNode = this.root;
    if (this.root.next == this.root) {
        this.root = null;
    } else {
        this.root.prev.next = this.root.next;
        this.root.next.prev = this.root.prev;
        this.root = this.root.next;
    }
    
    // update the size of the heap
    this.size--;
    
    // if the heap is now empty, return the minimum node
    if (this.root == null) {
        return minNode;
    }
    
    // create a new array for the root list
    var roots = [];
    
    // find the new minimum node and add the other nodes to the array
    var current = this.root;
    do {
        roots.push(current);
        current = current.next;
    } while (current != this.root);
    
    // consolidate the heap by pairwise-linking the trees of the same degree
    this.consolidate(roots);
    
    // return the minimum node
    return minNode;
}
```

## 운동

1. 선호하는 프로그래밍 언어로 피보나치 힙 데이터 구조를 구현합니다.

2. 피보나치 힙 데이터 구조를 사용하여 우선 순위 대기열을 구현합니다.

3. 피보나치 힙 데이터 구조를 사용하여 그래프에서 최단 경로 문제를 해결합니다.