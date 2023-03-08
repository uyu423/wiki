---
title: 【C语言】049：基数树（Compact Trie）
description: 
published: true
date: 2023-02-10T12:55:21.025Z
tags: 
editor: markdown
dateCreated: 2023-02-10T12:55:19.355Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 049: Radix Tree (Compact Trie)***English** document is available*](/en/Knowledge-base/Algorithm/c-language-049-radix-tree-compact-trie)
{.links-list}


# 049：基数树（Compact Trie）

## 1.简介

基数树，也称为紧凑型特里树，是一种节省空间的数据结构，用于存储字符串。它类似于二叉树，但每个节点只有两个孩子，而不是每个节点两个孩子。

## 2. 算法

基数树算法是一种节省空间的字符串存储方式。它类似于二叉树，但每个节点只有两个孩子，而不是每个节点两个孩子。

基数树算法是一种节省空间的字符串存储方式。它类似于二叉树，但每个节点只有两个孩子，而不是每个节点两个孩子。

要将字符串插入基数树，我们首先要找到字符串和根节点之间的最长公共前缀。如果最长公共前缀与字符串相同，我们将字符串插入根节点的树中。否则，我们将字符串插入树中对应于最长公共前缀的节点。

要在基数树中搜索字符串，我们首先要找到字符串与根节点之间的最长公共前缀。如果最长公共前缀与字符串相同，则返回根节点。否则，我们在子树中搜索与最长公共前缀对应的字符串。

## 3.代码示例

### 3.1插入

```c
void insert(Node* root, char* str) {
  int i, j, k;
  Node* cur = root;
  for (i = 0; str[i] != '\0'; i++) {
    for (j = 0; j < cur->n; j++) {
      if (cur->children[j]->c == str[i]) {
        cur = cur->children[j];
        break;
      }
    }
    if (j == cur->n) {
      Node* newNode = malloc(sizeof(Node));
      newNode->c = str[i];
      newNode->n = 1;
      cur->children[cur->n] = newNode;
      cur->n++;
    }
  }
}
```

### 3.2 搜索

```c
Node* search(Node* root, char* str) {
  int i, j;
  Node* cur = root;
  for (i = 0; str[i] != '\0'; i++) {
    for (j = 0; j < cur->n; j++) {
      if (cur->children[j]->c == str[i]) {
        cur = cur->children[j];
        break;
      }
    }
    if (j == cur->n) {
      return NULL;
    }
  }
  return cur;
}
```

## 4.练习

1. 用你喜欢的编程语言实现基数树算法。

2. 使用基数树算法存储英文单词列表。

3. 使用基数树算法存储 DNA 字符串列表。

## 5. 答案

1. 参见上面的代码示例。

2. 请参见代码示例 3.2。

3. 参见代码示例 3.1。