---
title: [C Language] 021: B-Tree
description: 
published: true
date: 2023-02-13T05:33:50.977Z
tags: 
editor: markdown
dateCreated: 2023-02-13T05:33:44.102Z
---

- [[Lenguaje C] 021: Árbol B***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-021-b-tree)
{.links-list}
- [【C语言】021：B树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-021-b-tree)
{.links-list}
- [[C언어] 021: B-트리***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-021-b-tree)
{.links-list}


# 021: B-Tree

A B-tree is a self-balancing tree data structure that maintains sorted data and allows searches, sequential access, insertions, and deletions in logarithmic time. The B-tree is a generalization of a binary search tree in that a node can have more than two children.

## Concept

A B-tree is a rooted tree in which each node has no more than M children. A B-tree is defined by the term minimum degree `t`. The root node may have fewer than `t` children. If a node is not the root node and is not a leaf node, it must have at least `t` children. If a node is a leaf node, it must have at least `t-1` keys. All leaves appear in the same level, and a non-leaf node with `k` children contains `k-1` keys.

We define the index `i` of a node to be the number of children it has. For example, the root node has index 0, the first child of the root node has index 1, and so on.

The height of a B-tree is the number of levels in the longest path from the root to a leaf.

The following is an example of a B-tree of minimum degree `t=2`:

![BTree](https://upload.wikimedia.org/wikipedia/commons/thumb/d/df/B-tree_example.svg/300px-B-tree_example.svg.png)

## Operations

A B-tree supports the following operations:

- Search: Given a key `k`, find the value associated with `k`.
- Insert: Given a key-value pair `(k,v)`, insert `(k,v)` into the B-tree.
- Delete: Given a key `k`, delete the key-value pair `(k,v)` from the B-tree.

All of these operations are performed in logarithmic time.

## Implementation

A B-tree can be implemented using an array or a linked list.

### Array Implementation

In an array implementation, each node of the B-tree is represented by an array of size `M`. The first element of the array is the number of keys in the node, `n`. The remaining `M-1` elements are the `n` keys and the `n+1` children of the node, in order.

For example, the root node in the above figure is represented by the array `[3, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120]`.

The search, insert, and delete operations can be performed in a similar way to a binary search tree.

### Linked List Implementation

In a linked list implementation, each node of the B-tree is represented by a linked list of size `M`. The first element of the linked list is the number of keys in the node, `n`. The remaining `M-1` elements are the `n` keys and the `n+1` children of the node, in order.

For example, the root node in the above figure is represented by the linked list `[3, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120]`.

The search, insert, and delete operations can be performed in a similar way to a binary search tree.

## Code Examples

### Array Implementation

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

### Linked List Implementation

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