---
title: [JavaScript] 021: B-트리
description: 
published: true
date: 2023-02-09T23:32:52.986Z
tags: 
editor: markdown
dateCreated: 2023-02-09T23:32:51.275Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 021: B-Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-021-b-tree)
{.links-list}


# JavaScript 021: B-트리

B-트리는 정렬된 데이터를 유지하고 대수 시간에 검색, 삽입 및 삭제를 허용하는 자체 균형 트리 데이터 구조입니다. B-트리는 노드가 둘 이상의 자식을 가질 수 있다는 점에서 이진 검색 트리의 일반화입니다.

## 개념

B-트리는 데이터를 정렬된 상태로 유지하고 로그 시간에 검색, 삽입 및 삭제를 허용하는 트리 데이터 구조입니다. B-트리는 노드가 둘 이상의 자식을 가질 수 있다는 점에서 이진 검색 트리의 일반화입니다. 이진 검색 트리에 비해 B-트리의 장점은 삽입 및 삭제와 같은 작업에 필요한 디스크 액세스가 적다는 것입니다.

순서 m의 B-트리는 각 노드가 최대 m개의 자식을 갖는 트리입니다. 루트 노드에는 적어도 두 개의 자식이 있습니다. 두 노드의 자식 수 차이가 최대 1인 경우 B-트리가 균형을 이룹니다.

B-트리의 높이는 트리의 수준 수입니다. 나무의 높이는 뿌리에서 잎까지 가장 긴 경로의 길이입니다.

차수 m의 B-트리는 최대 m의 높이를 가질 수 있습니다.

## 코드 예제

다음은 JavaScript에서 B-tree를 간단하게 구현한 것입니다.

```javascript
class Node {
  constructor(keys, children) {
    this.keys = keys;
    this.children = children;
  }
}

class BTree {
  constructor(order) {
    this.order = order;
    this.root = null;
  }
  
  insert(key) {
    if (this.root === null) {
      this.root = new Node([key], []);
    } else {
      this._insert(key, this.root);
    }
  }
  
  _insert(key, node) {
    if (node.keys.length < this.order - 1) {
      this._insertKey(key, node);
    } else {
      const medianIndex = Math.floor((this.order - 1) / 2);
      const median = node.keys[medianIndex];
      const leftKeys = node.keys.slice(0, medianIndex);
      const rightKeys = node.keys.slice(medianIndex + 1);
      const leftChildren = node.children.slice(0, medianIndex + 1);
      const rightChildren = node.children.slice(medianIndex + 1);
      const newNode = new Node([median], [
        new Node(leftKeys, leftChildren),
        new Node(rightKeys, rightChildren)
      ]);
      if (key < median) {
        this._insert(key, newNode.children[0]);
      } else {
        this._insert(key, newNode.children[1]);
      }
      this.root = newNode;
    }
  }
  
  _insertKey(key, node) {
    let i = 0;
    while (i < node.keys.length && key > node.keys[i]) {
      i++;
    }
    node.keys = [
      ...node.keys.slice(0, i),
      key,
      ...node.keys.slice(i)
    ];
    node.children = [
      ...node.children.slice(0, i + 1),
      new Node([], []),
      ...node.children.slice(i + 1)
    ];
  }
  
  search(key) {
    return this._search(key, this.root);
  }
  
  _search(key, node) {
    if (node === null) {
      return false;
    }
    let i = 0;
    while (i < node.keys.length && key > node.keys[i]) {
      i++;
    }
    if (i < node.keys.length && key === node.keys[i]) {
      return true;
    }
    return this._search(key, node.children[i]);
  }
}
```

## 운동

1. B-트리에 대한 삭제 작업을 구현합니다.

2. B-트리에 대한 범위 검색 작업을 구현합니다. 범위 검색은 두 개의 키(하한 및 상한)를 사용하고 두 경계 사이에 있는 트리의 모든 키를 반환해야 합니다.

## 답변

1.

```javascript
class BTree {
  delete(key) {
    if (this.root === null) {
      return;
    }
    this._delete(key, this.root);
  }
  
  _delete(key, node) {
    let i = 0;
    while (i < node.keys.length && key > node.keys[i]) {
      i++;
    }
    if (i < node.keys.length && key === node.keys[i]) {
      if (node.children[i].keys.length >= this.order) {
        const predecessor = this._getPredecessor(node.children[i]);
        node.keys[i] = predecessor;
        this._delete(predecessor, node.children[i]);
      } else if (node.children[i + 1].keys.length >= this.order) {
        const successor = this._getSuccessor(node.children[i + 1]);
        node.keys[i] = successor;
        this._delete(successor, node.children[i + 1]);
      } else {
        this._merge(node, i);
        this._delete(key, node.children[i]);
      }
    } else {
      this._delete(key, node.children[i]);
    }
  }
  
  _getPredecessor(node) {
    let current = node;
    while (current.children.length !== 0) {
      current = current.children[current.children.length - 1];
    }
    return current.keys[current.keys.length - 1];
  }
  
  _getSuccessor(node) {
    let current = node;
    while (current.children.length !== 0) {
      current = current.children[0];
    }
    return current.keys[0];
  }
  
  _merge(node, i) {
    const left = node.children[i];
    const right = node.children[i + 1];
    const key = node.keys[i];
    left.keys = [...left.keys, key, ...right.keys];
    left.children = [...left.children, ...right.children];
    node.keys = node.keys.filter((k, index) => index !== i);
    node.children = node.children.filter((child, index) => index !== i + 1);
  }
}
```

2.

```javascript
class BTree {
  rangeSearch(lowerBound, upperBound) {
    if (this.root === null) {
      return [];
    }
    return this._rangeSearch(lowerBound, upperBound, this.root);
  }
  
  _rangeSearch(lowerBound, upperBound, node) {
    let i = 0;
    while (i < node.keys.length && lowerBound > node.keys[i]) {
      i++;
    }
    let results = [];
    while (i < node.keys.length && upperBound >= node.keys[i]) {
      if (node.children.length === 0) {
        results.push(node.keys[i]);
      } else {
        results = [...results, ...this._rangeSearch(lowerBound, upperBound, node.children[i])];
      }
      i++;
    }
    if (node.children.length > 0) {
      results = [...results, ...this._rangeSearch(lowerBound, upperBound, node.children[i])];
    }
    return results;
  }
}
```