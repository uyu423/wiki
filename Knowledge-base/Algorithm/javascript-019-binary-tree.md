---
title: [JavaScript] 019: 이진 트리
description: 
published: true
date: 2023-02-09T21:32:36.321Z
tags: 
editor: markdown
dateCreated: 2023-02-09T21:32:34.691Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 019: Binary Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-019-binary-tree)
{.links-list}


# 이진 트리

컴퓨터 과학에서 이진 트리는 각 노드가 왼쪽 자식과 오른쪽 자식이라고 하는 최대 두 개의 자식을 갖는 트리 데이터 구조입니다.

이진 트리는 두 가지 작업을 허용하는 구조입니다.

- 트리에서 최대 요소 찾기.
- 트리에서 최소 요소 찾기.

이 두 작업의 시간 복잡도는 O(log n)입니다. 여기서 n은 트리의 노드 수입니다.

이진 트리는 이진 검색 트리 및 힙을 구현하는 데 사용됩니다.

## 코드 예

다음은 JavaScript에서 이진 트리의 예입니다.

```javascript
var tree = {
  value: 10,
  left: {
    value: 5,
    left: {
      value: 2,
      left: null,
      right: null
    },
    right: {
      value: 7,
      left: null,
      right: null
    }
  },
  right: {
    value: 15,
    left: {
      value: 12,
      left: null,
      right: null
    },
    right: {
      value: 17,
      left: null,
      right: null
    }
  }
};
```

## 최대 요소 찾기

이진 트리에서 최대 요소를 찾기 위해 재귀 알고리즘을 사용할 수 있습니다.

아이디어는 루트 노드를 왼쪽 및 오른쪽 자식 노드와 비교하는 것입니다. 루트 노드가 두 자식 노드보다 크면 최대 요소입니다. 그렇지 않으면 최대 요소는 두 자식 노드 중 더 큽니다.

그런 다음 왼쪽 및 오른쪽 자식 노드에서 동일한 알고리즘을 재귀적으로 호출할 수 있습니다.

다음은 알고리즘의 의사 코드입니다.

```
function findMax(node) {
  if (node is null) {
    return null;
  }
 
  var max = node.value;
  var leftMax = findMax(node.left);
  var rightMax = findMax(node.right);
 
  if (leftMax > max) {
    max = leftMax;
  }
 
  if (rightMax > max) {
    max = rightMax;
  }
 
  return max;
}
```

## 최소 요소 찾기

이진 트리에서 최소 요소를 찾기 위해 재귀 알고리즘을 사용할 수 있습니다.

아이디어는 루트 노드를 왼쪽 및 오른쪽 자식 노드와 비교하는 것입니다. 루트 노드가 두 자식 노드보다 작으면 최소 요소입니다. 그렇지 않으면 최소 요소는 두 자식 노드 중 작은 것이 됩니다.

그런 다음 왼쪽 및 오른쪽 자식 노드에서 동일한 알고리즘을 재귀적으로 호출할 수 있습니다.

다음은 알고리즘의 의사 코드입니다.

```
function findMin(node) {
  if (node is null) {
    return null;
  }
 
  var min = node.value;
  var leftMin = findMin(node.left);
  var rightMin = findMin(node.right);
 
  if (leftMin < min) {
    min = leftMin;
  }
 
  if (rightMin < min) {
    min = rightMin;
  }
 
  return min;
}
```

## 관련 연습

- [이진 트리의 최대 깊이](https://leetcode.com/problems/maximum-depth-of-binary-tree/)
- [이진 트리의 최소 깊이](https://leetcode.com/problems/minimum-depth-of-binary-tree/)
- [대칭 트리](https://leetcode.com/problems/symmetric-tree/)
- [이진 트리 중위 순회](https://leetcode.com/problems/binary-tree-inorder-traversal/)
- [이진 트리 후위 순회](https://leetcode.com/problems/binary-tree-postorder-traversal/)
- [이진 트리 선주문 순회](https://leetcode.com/problems/binary-tree-preorder-traversal/)