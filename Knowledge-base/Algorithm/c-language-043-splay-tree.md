---
title: [C언어] 043: 스플레이 트리
description: 
published: true
date: 2023-02-10T07:55:35.685Z
tags: 
editor: markdown
dateCreated: 2023-02-10T07:55:34.088Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 043: Splay Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-043-splay-tree)
{.links-list}


# 스플레이 트리

스플레이 트리는 최근에 액세스한 요소가 다시 빠르게 액세스할 수 있는 추가 속성이 있는 자체 균형 이진 검색 트리입니다. 대수 시간에 삽입, 조회 및 제거와 같은 기본 작업을 수행합니다.

스플레이 트리는 다음 불변성을 만족하는 이진 트리입니다.

* 트리가 비어 있거나
* 트리는 루트 노드와 좌우 2개의 하위 트리로 구성되며,
* 루트 노드의 값이 왼쪽 하위 트리의 모든 값보다 크고,
* 루트 노드의 값이 오른쪽 하위 트리의 모든 값보다 작습니다.

다음 그림은 스플레이 트리의 예를 보여줍니다.

![스플레이 트리](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Splay_tree_animation.gif/250px-Splay_tree_animation.gif)

Splay 트리는 자체 균형 조정입니다. 즉, 가장 최근에 액세스한 요소가 다시 빠르게 액세스할 수 있도록 트리가 자체적으로 조정됩니다. 이는 액세스된 요소를 트리의 루트로 이동하여 수행됩니다.

다음 작업은 스플레이 트리에서 지원됩니다.

* 삽입
* 조회
* 제거

이러한 모든 작업은 대수 시간으로 수행됩니다.

## 삽입

스플레이 트리에 삽입하는 것은 이진 검색 트리에 삽입하는 것과 유사합니다. 먼저 트리를 순회하여 새 요소의 올바른 위치를 찾습니다. 그런 다음 새 요소를 트리에 삽입합니다.

그러나 삽입 후에는 새 요소를 루트로 확장해야 합니다. 이것은 일련의 트리 회전에 의해 수행됩니다.

다음 그림은 splay 트리에 삽입하는 예를 보여줍니다.

![Splay 트리에 삽입](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b0/Splay-tree-insert.gif/250px-Splay-tree-insert.gif)

## 조회

스플레이 트리에서의 조회는 이진 검색 트리에서의 조회와 유사합니다. 먼저 트리를 순회하여 찾고자 하는 요소를 찾습니다. 그런 다음 요소를 반환합니다.

그러나 조회 후 요소를 루트로 확장해야 합니다. 이것은 일련의 트리 회전에 의해 수행됩니다.

다음 그림은 스플레이 트리에서 조회하는 예를 보여줍니다.

![Splay 트리에서 조회](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Splay-tree-lookup.gif/250px-Splay-tree-lookup.gif)

## 제거

스플레이 트리에서 제거하는 것은 이진 검색 트리에서 제거하는 것과 유사합니다. 먼저 트리를 순회하여 제거하려는 요소를 찾습니다. 그런 다음 요소를 제거합니다.

그러나 제거 후에 제거된 요소의 부모를 루트로 확장해야 합니다. 이것은 일련의 트리 회전에 의해 수행됩니다.

다음 그림은 스플레이 트리에서 제거하는 예를 보여줍니다.

![Splay 트리에서 제거](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Splay-tree-delete.gif/250px-Splay-tree-delete.gif)

## 구현

스플레이 트리는 이진 검색 트리로 구현할 수 있습니다. 다음 의사 코드는 splay 트리에 요소를 삽입하는 방법의 예를 보여줍니다.

```
insert(x, t)
  if t is empty
    return new node with value x
  if x < t.value
    t.left = insert(x, t.left)
  else
    t.right = insert(x, t.right)
  return t
```

다음 의사 코드는 splay 트리에서 요소를 조회하는 방법의 예를 보여줍니다.

```
lookup(x, t)
  if t is empty
    return null
  if x < t.value
    return lookup(x, t.left)
  else if x > t.value
    return lookup(x, t.right)
  else
    return t
```

다음 의사 코드는 splay 트리에서 요소를 제거하는 방법의 예를 보여줍니다.

```
remove(x, t)
  if t is empty
    return null
  if x < t.value
    t.left = remove(x, t.left)
  else if x > t.value
    t.right = remove(x, t.right)
  else
    t = remove(t)
  return t

remove(t)
  if t.left is empty and t.right is empty
    return null
  if t.left is empty
    return t.right
  if t.right is empty
    return t.left
  y = t.right
  while y.left is not empty
    y = y.left
  t.right = remove(y.value, t.right)
  y.left = t.left
  y.right = t.right
  return y
```

## 복잡성

스플레이 트리가 지원하는 작업의 시간 복잡도는 다음과 같습니다.

* 삽입: O(log n)
* 조회: O(log n)
* 제거: O(log n)

스플레이 트리의 공간 복잡도는 O(n)이며, 여기서 n은 트리의 요소 수입니다.