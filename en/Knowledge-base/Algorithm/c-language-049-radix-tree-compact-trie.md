---
title: [C Language] 049: Radix Tree (Compact Trie)
description: 
published: true
date: 2023-02-10T12:55:25.729Z
tags: 
editor: markdown
dateCreated: 2023-02-10T12:55:19.362Z
---

- [[Lenguaje C] 049: Árbol Radix (Trie compacto)***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-049-radix-tree-compact-trie)
{.links-list}
- [【C语言】049：基数树（Compact Trie）***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-049-radix-tree-compact-trie)
{.links-list}
- [[C언어] 049: Radix Tree(Compact Trie)***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-049-radix-tree-compact-trie)
{.links-list}


# 049: Radix Tree (Compact Trie)

## 1. Introduction

A radix tree, also known as a compact trie, is a space-efficient data structure that is used to store strings. It is similar to a binary tree, but each node has only two children, rather than two children per node.

## 2. Algorithm

The radix tree algorithm is a space-efficient way to store strings. It is similar to a binary tree, but each node has only two children, rather than two children per node.

The radix tree algorithm is a space-efficient way to store strings. It is similar to a binary tree, but each node has only two children, rather than two children per node.

To insert a string into a radix tree, we first find the longest common prefix between the string and the root node. If the longest common prefix is the same as the string, we insert the string into the tree at the root node. Otherwise, we insert the string into the tree at the node that corresponds to the longest common prefix.

To search for a string in a radix tree, we first find the longest common prefix between the string and the root node. If the longest common prefix is the same as the string, we return the root node. Otherwise, we search for the string in the subtree that corresponds to the longest common prefix.

## 3. Code Examples

### 3.1 Insert

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

### 3.2 Search

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

## 4. Exercises

1. Implement the radix tree algorithm in your favorite programming language.

2. Use the radix tree algorithm to store a list of English words.

3. Use the radix tree algorithm to store a list of DNA strings.

## 5. Answers

1. See code examples above.

2. See code example 3.2.

3. See code example 3.1.