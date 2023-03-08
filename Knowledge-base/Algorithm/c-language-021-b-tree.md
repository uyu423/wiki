---
title: [C언어] 021: B-트리
description: 
published: true
date: 2023-02-13T05:33:45.763Z
tags: 
editor: markdown
dateCreated: 2023-02-13T05:33:44.097Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 021: B-Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-021-b-tree)
{.links-list}


# 021: B-트리

B-트리는 정렬된 데이터를 유지하고 대수 시간에 검색, 순차 액세스, 삽입 및 삭제를 허용하는 자체 균형 트리 데이터 구조입니다. B-트리는 노드가 둘 이상의 자식을 가질 수 있다는 점에서 이진 검색 트리의 일반화입니다.

## 개념

B-트리는 각 노드에 M개 이하의 자식이 있는 루트 트리입니다. B-트리는 최소 차수 't'라는 용어로 정의됩니다. 루트 노드에는 `t` 자식보다 적을 수 있습니다. 노드가 루트 노드가 아니고 리프 노드가 아닌 경우 적어도 `t`개의 자식이 있어야 합니다. 노드가 리프 노드인 경우 적어도 't-1' 키가 있어야 합니다. 모든 리프는 동일한 레벨에 나타나며 `k` 자식이 있는 리프가 아닌 노드에는 `k-1` 키가 포함됩니다.

우리는 노드의 인덱스 `i`를 노드가 가진 자식의 수로 정의합니다. 예를 들어 루트 노드의 인덱스는 0이고 루트 노드의 첫 번째 하위 노드의 인덱스는 1입니다.

B-트리의 높이는 루트에서 리프까지 가장 긴 경로의 레벨 수입니다.

다음은 최소 차수가 `t=2`인 B-트리의 예입니다.

![BTree](https://upload.wikimedia.org/wikipedia/commons/thumb/d/df/B-tree_example.svg/300px-B-tree_example.svg.png)

## 운영

B-트리는 다음 작업을 지원합니다.

- 검색: `k` 키가 주어지면 `k`와 연관된 값을 찾습니다.
- 삽입: 키-값 쌍 `(k,v)`가 주어지면 `(k,v)`를 B-트리에 삽입합니다.
- 삭제: 키 `k`가 주어지면 B-트리에서 키-값 쌍 `(k,v)`를 삭제합니다.

이러한 모든 작업은 대수 시간으로 수행됩니다.

## 구현

B-트리는 배열 또는 연결 목록을 사용하여 구현할 수 있습니다.

### 어레이 구현

배열 구현에서 B-트리의 각 노드는 'M' 크기의 배열로 표시됩니다. 배열의 첫 번째 요소는 노드 'n'의 키 수입니다. 나머지 `M-1` 요소는 순서대로 `n` 키와 노드의 `n+1` 자식입니다.

예를 들어, 위 그림의 루트 노드는 배열 `[3, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120]`으로 표시됩니다.

검색, 삽입 및 삭제 작업은 이진 검색 트리와 유사한 방식으로 수행할 수 있습니다.

### 연결 리스트 구현

연결된 목록 구현에서 B-트리의 각 노드는 'M' 크기의 연결된 목록으로 표시됩니다. 연결된 목록의 첫 번째 요소는 노드 'n'의 키 수입니다. 나머지 `M-1` 요소는 순서대로 `n` 키와 노드의 `n+1` 자식입니다.

예를 들어, 위 그림의 루트 노드는 연결된 목록 `[3, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120]`으로 표시됩니다.

검색, 삽입 및 삭제 작업은 이진 검색 트리와 유사한 방식으로 수행할 수 있습니다.

## 코드 예제

### 어레이 구현

```c
#include <stdio.h>
#include <stdlib.h>

#define M 4

typedef struct btreenode {
  int n;
  int keys[M-1];
  struct btreenode* children[M];
} btreenode;

btreenode* btree_create()
{
  btreenode* root = (btreenode*)malloc(sizeof(btreenode));
  root->n = 0;
  return root;
}

void btree_search(btreenode* root, int key, btreenode** out_node, int* out_index)
{
  int i = 0;
  while (i < root->n && key > root->keys[i]) {
    i++;
  }
  if (i < root->n && key == root->keys[i]) {
    *out_node = root;
    *out_index = i;
    return;
  }
  if (root->children[i] == NULL) {
    *out_node = NULL;
    return;
  }
  btree_search(root->children[i], key, out_node, out_index);
}

void btree_insert(btreenode* root, int key, int value)
{
  btreenode* node;
  int index;
  btree_search(root, key, &node, &index);
  if (node != NULL) {
    // key already exists, update value
    node->values[index] = value;
    return;
  }
  // key does not exist, insert key-value pair
  if (root->n < M-1) {
    // insert into node
    int i = root->n-1;
    while (i >= 0 && key < root->keys[i]) {
      root->keys[i+1] = root->keys[i];
      root->values[i+1] = root->values[i];
      i--;
    }
    root->keys[i+1] = key;
    root->values[i+1] = value;
    root->n++;
  } else {
    // node is full, split node
    btreenode* left = (btreenode*)malloc(sizeof(btreenode));
    btreenode* right = (btreenode*)malloc(sizeof(btreenode));
    int i, j, k;
    // copy keys and values to left and right nodes
    for (i = 0, j = 0, k = 0; i < root->n; i++) {
      if (i == j) {
        // copy key to left node
        left->keys[k] = root->keys[i];
        left->values[k] = root->values[i];
        k++;
      } else {
        // copy key to right node
        right->keys[j] = root->keys[i];
        right->values[j] = root->values[i];
        j++;
      }
      if (k == M/2) {
        // left node is full, copy remaining keys and values to right node
        while (i < root->n) {
          right->keys[j] = root->keys[i];
          right->values[j] = root->values[i];
          i++;
          j++;
        }
      }
    }
    // update root
    root->n = 1;
    root->keys[0] = left->keys[M/2];
    root->children[0] = left;
    root->children[1] = right;
    // insert key and value into appropriate node
    if (key < root->keys[0]) {
      btree_insert(left, key, value);
    } else {
      btree_insert(right, key, value);
    }
  }
}

void btree_delete(btreenode* root, int key)
{
  btreenode* node;
  int index;
  btree_search(root, key, &node, &index);
  if (node == NULL) {
    // key does not exist
    return;
  }
  // key exists, delete key-value pair
  if (node->children[index] == NULL) {
    // key is in leaf node, simply delete it
    int i;
    for (i = index; i < node->n-1; i++) {
      node->keys[i] = node->keys[i+1];
      node->values[i] = node->values[i+1];
    }
    node->n--;
  } else {
    // key is in an internal node, find predecessor (or successor)
    btreenode* pred = node->children[index];
    while (pred->children[pred->n] != NULL) {
      pred = pred->children[pred->n];
    }
    // replace key with predecessor's key
    node->keys[index] = pred->keys[pred->n-1];
    // recursively delete predecessor
    btree_delete(pred, pred->keys[pred->n-1]);
  }
}

void btree_destroy(btreenode* root)
{
  if (root == NULL) return;
  int i;
  for (i = 0; i <= root->n; i++) {
    btree_destroy(root->children[i]);
  }
  free(root);
}

int main()
{
  btreenode* root = btree_create();
  btree_insert(root, 10, 1);
  btree_insert(root, 20, 2);
  btree_insert(root, 30, 3);
  btree_insert(root, 40, 4);
  btree_insert(root, 50, 5);
  btree_insert(root, 60, 6);
  btree_insert(root, 70, 7);
  btree_insert(root, 80, 8);
  btree_insert(root, 90, 9);
  btree_insert(root, 100, 10);
  btree_insert(root, 110, 11);
  btree_insert(root, 120, 12);
  btree_destroy(root);
  return 0;
}
```

### 연결 리스트 구현

```c
# include <stdio.h>
# include <stdlib.h>

# define M 4

typedef 구조체 btreenode {
  정수 n;
  정수 키[M-1];
  struct btreenode* children[M];
} btree노드;

btreenode* btree_create()
{
  btreenode* root = (btreenode*)malloc(sizeof(btreenode));
  루트->n = 0;
  리턴 루트;
}

무효 btree_search(btreenode* 루트, int 키, btreenode** out_node, int* out_index)
{
  정수 i = 0;
  동안 (i < 루트->n && 키 > 루트->키[i]) {
    i++;
  }
  if (i < 루트->n && 키 == 루트->키[i]) {
    *out_node = 루트;
    *out_index = i;
    반품;
  }
  if (루트->어린이[i] == NULL) {
    *out_node = NULL;
    반품;
  }
  btree_search(root->children[i], 키, out_node, out_index);
}

무효 btree_insert(btreenode* 루트, int 키, int 값)
{
  btreenode* 노드;
  정수 인덱스;
  btree_search(루트, 키, &노드, &인덱스);
  if (노드 != NULL) {
    // 키가 이미 존재합니다. 값을 업데이트합니다.
    노드->값[인덱스] = 값;
    반품;
  }
  // 키가 존재하지 않음, 키-값 쌍 삽입
  if (루트->n < M-1) {
    // 노드에 삽입
    int i = 루트->n-1;
    동안 (i >= 0 && 키 < 루트->키[i]) {
      루트->키[i+1] = 루트->키[i];
      루트->값[i+1] = 루트->값[i];
      나--;
    }
    루트->키[i+1] = 키;
    루트->값[i+1] = 값;
    루트->n++;
  } 또 다른 {
    // 노드가 꽉 찼습니다. 노드 분할
    btreenode* 왼쪽 = (btreenode*)malloc(sizeof(btreenode));
    btreenode* right = (btreenode*)malloc(sizeof(btreenode));
    정수 i, j, k;
    // 키와 값을 왼쪽 및 오른쪽 노드에 복사
    for (i = 0, j = 0, k = 0; i < root->n; i++) {
      if (i == j) {
        // 키를 왼쪽 노드에 복사
        왼쪽->키[k] = 루트->키[i];
        왼쪽->값[k] = 루트->값[i];
        k++;
      } 또 다른 {
        // 오른쪽 노드에 키 복사
        오른쪽->키[j] = 루트->키[i];
        right->values[j] = 루트->values[i];
        j++;
      }
      if (k == M/2) {
        // 왼쪽 노드가 가득 찼습니다. 나머지 키와 값을 오른쪽 노드에 복사합니다.
        동안 (i < 루트->n) {
          오른쪽->키[j] = 루트->키[i];
          right->values[j] = 루트->values[i];
          i++;
          j++;
        }
      }
    }
    // 루트 업데이트
    루트->n = 1;
    루트->키[0] = 왼쪽->키[M/2];
    root->children[0] = 왼쪽;
    root->children[1] = 오른쪽;
    // 키와 값을 적절한 노드에 삽입
    if (키 < 루트->키[0]) {
      btree_insert(왼쪽, 키, 값);
    } 또 다른 {
      btree_insert(오른쪽, 키, 값);
    }
  }
}

무효 btree_delete(btreenode* 루트, int 키)
{
  btreenode* 노드;
  정수 인덱스;
  btree_search(루트, 키, &노드, &인덱스);
  if (노드 == NULL) {
    // 키가 존재하지 않음
    반품;
  }
  // 키 존재, 키-값 쌍 삭제
  if (노드->자식[인덱스] == NULL) {
    // 키가 리프 노드에 있으므로 삭제하기만 하면 됩니다.
    정수 i;
    for (i = 인덱스; i < 노드->n-1; i++) {
      노드->키[i] = 노드->키[i+1];
      노드->값[i] = 노드->값[i+1];
    }
    노드->n--;
  } 또 다른 {
    // 키가 내부 노드에 있음, 선행자(또는 후임자) 찾기
    btreenode* pred = 노드->자식[인덱스];
    동안 (pred->children[pred->n] != NULL) {
      pred = pred->children[pred->n];
    }
    // 키를 전임자의 키로 교체
    node->keys[index] = pred->keys[pred->n-1];
    // 선행 항목을 재귀적으로 삭제
    btree_delete(pred, pred->keys[pred->n-1]);
  }
}

무효 btree_destroy(btreenode* 루트)
{
  if (루트 == NULL) 반환;
  정수 i;
  for (i = 0; i <= root->n; i++) {
    btree_destroy(root->children[i]);
  }
  무료(루트);
}

정수 메인()
{
  btreenode* 루트 = btree_create();
  btree_insert(루트, 10, 1);
  btree_insert(루트, 20, 2);
  btree_insert(루트, 30, 3);
  btree_insert(루트, 40, 4);
  btree_insert(루트, 50, 5);
  btree_insert(루트, 60, 6);
  btree_insert(루트, 70, 7);
  btree_insert(루트, 80, 8);