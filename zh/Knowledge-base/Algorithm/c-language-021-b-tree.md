---
title: 【C语言】021：B树
description: 
published: true
date: 2023-02-13T05:33:45.754Z
tags: 
editor: markdown
dateCreated: 2023-02-13T05:33:44.098Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 021: B-Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-021-b-tree)
{.links-list}


# 021：B树

B 树是一种自平衡树数据结构，它维护已排序的数据并允许在对数时间内进行搜索、顺序访问、插入和删除。 B 树是二叉搜索树的推广，因为一个节点可以有两个以上的子节点。

## 概念

B 树是一棵有根树，其中每个节点的子节点不超过 M 个。 B 树由术语最小度“t”定义。根节点可能有少于“t”个孩子。如果一个节点既不是根节点也不是叶节点，那么它必须至少有“t”个孩子。如果一个节点是叶节点，它必须至少有“t-1”个键。所有叶子都出现在同一级别，并且具有“k”个子节点的非叶子节点包含“k-1”个键。

我们将节点的索引“i”定义为其拥有的子节点数。例如，根节点的索引为 0，根节点的第一个子节点的索引为 1，依此类推。

B 树的高度是从根到叶的最长路径中的层数。

以下是最小度数为“t=2”的 B 树示例：

![BTree](https://upload.wikimedia.org/wikipedia/commons/thumb/d/df/B-tree_example.svg/300px-B-tree_example.svg.png)

## 操作

B 树支持以下操作：

- 搜索：给定键“k”，找到与“k”关联的值。
- 插入：给定键值对 `(k,v)`，将 `(k,v)` 插入到 B 树中。
- 删除：给定键“k”，从 B 树中删除键值对“(k,v)”。

所有这些操作都以对数时间执行。

## 执行

B 树可以使用数组或链表来实现。

### 数组实现

在数组实现中，B 树的每个节点都由一个大小为“M”的数组表示。数组的第一个元素是节点中键的数量，“n”。剩余的“M-1”元素依次是节点的“n”键和“n+1”子节点。

例如上图中的根节点用数组`[3, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120]`表示。

可以以类似于二叉搜索树的方式执行搜索、插入和删除操作。

### 链表实现

在链表实现中，B 树的每个节点都由大小为“M”的链表表示。链表的第一个元素是节点中键的数量，“n”。剩余的“M-1”元素依次是节点的“n”键和“n+1”子节点。

例如上图中的根节点用链表`[3, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120]`表示。

可以以类似于二叉搜索树的方式执行搜索、插入和删除操作。

## 代码示例

### 数组实现

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

### 链表实现

```c
# include <stdio.h>
# include <标准库.h>

# 定义 M 4

typedef 结构 btreenode {
  诠释 n;
  整数键[M-1]；
  结构 btreenode* 儿童 [M];
} b树节点；

btreenode* btree_create()
{
  btreenode* root = (btreenode*)malloc(sizeof(btreenode));
  根->n = 0；
  返回根；
}

void btree_search(btreenode* root, int key, btreenode** out_node, int* out_index)
{
  诠释我= 0;
  while (i < root->n && key > root->keys[i]) {
    我++；
  }
  if (i < root->n && key == root->keys[i]) {
    *输出节点=根；
    *输出索引=我；
    返回;
  }
  如果 (root->children[i] == NULL) {
    *out_node = NULL;
    返回;
  }
  btree_search(root->children[i], key, out_node, out_index);
}

void btree_insert(btreenode* root, int key, int value)
{
  btreenode*节点；
  整数索引；
  btree_search(root, key, &node, &index);
  如果（节点！= NULL）{
    // 键已经存在，更新值
    节点->值[索引] = 值；
    返回;
  }
  // 键不存在，插入键值对
  如果（根->n < M-1）{
    // 插入节点
    int i = root->n-1;
    while (i >= 0 && key < root->keys[i]) {
      root->keys[i+1] = root->keys[i];
      root->values[i+1] = root->values[i];
      我 - ;
    }
    root->keys[i+1] = key;
    根->值[i+1] = 值；
    根->n++；
  } 别的 {
    // 节点已满，拆分节点
    btreenode* left = (btreenode*)malloc(sizeof(btreenode));
    btreenode* right = (btreenode*)malloc(sizeof(btreenode));
    诠释我，j，k;
    // 将键和值复制到左右节点
    对于 (i = 0, j = 0, k = 0; i < root->n; i++) {
      如果（我==j）{
        // 复制key到左节点
        left->keys[k] = root->keys[i];
        left->values[k] = root->values[i];
        k++;
      } 别的 {
        // 复制key到右节点
        right->keys[j] = root->keys[i];
        right->values[j] = root->values[i];
        j++;
      }
      如果（k == M/2）{
        // 左节点已满，将剩余的键和值复制到右节点
        while (i < root->n) {
          right->keys[j] = root->keys[i];
          right->values[j] = root->values[i];
          我++；
          j++;
        }
      }
    }
    //更新根
    根->n = 1；
    root->keys[0] = left->keys[M/2];
    root->children[0] = left;
    root->children[1] = 正确；
    // 将键和值插入适当的节点
    如果（键<根->键[0]）{
      btree_insert（左，键，值）；
    } 别的 {
      btree_insert（右，键，值）；
    }
  }
}

void btree_delete(btreenode* root, int key)
{
  btreenode*节点；
  整数索引；
  btree_search(root, key, &node, &index);
  如果（节点== NULL）{
    // 键不存在
    返回;
  }
  // key存在，删除键值对
  if (node->children[index] == NULL) {
    // key在叶节点中，删除即可
    诠释我;
    for (i = index; i < node->n-1; i++) {
      节点->键[i] = 节点->键[i+1];
      节点->值[i] = 节点->值[i+1]；
    }
    节点->n--;
  } 别的 {
    // key 在内部节点中，查找前驱（或后继）
    btreenode* pred = node->children[index];
    while (pred->children[pred->n] != NULL) {
      pred = pred->children[pred->n];
    }
    // 用前任的密钥替换密钥
    node->keys[index] = pred->keys[pred->n-1];
    // 递归删除前导
    btree_delete(pred, pred->keys[pred->n-1]);
  }
}

void btree_destroy(btreenode* root)
{
  如果（root == NULL）返回；
  诠释我;
  对于 (i = 0; i <= root->n; i++) {
    btree_destroy(root->children[i]);
  }
  免费（根）；
}

主函数()
{
  btreenode* root = btree_create();
  btree_insert(根, 10, 1);
  btree_insert(根, 20, 2);
  btree_insert(根, 30, 3);
  btree_insert(根, 40, 4);
  btree_insert(根, 50, 5);
  btree_insert(根, 60, 6);
  btree_insert(根, 70, 7);
  btree_insert(根, 80, 8);