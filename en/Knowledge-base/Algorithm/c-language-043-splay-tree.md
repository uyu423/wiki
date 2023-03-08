---
title: [C Language] 043: Splay Tree
description: 
published: true
date: 2023-02-10T07:55:40.369Z
tags: 
editor: markdown
dateCreated: 2023-02-10T07:55:34.092Z
---

- [[Lenguaje C] 043: árbol de reproducción***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-043-splay-tree)
{.links-list}
- [【C语言】043：八叉树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-043-splay-tree)
{.links-list}
- [[C언어] 043: 스플레이 트리***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-043-splay-tree)
{.links-list}


# Splay Tree

A splay tree is a self-balancing binary search tree with the additional property that recently accessed elements are quick to access again. It performs basic operations such as insertion, look-up and removal in logarithmic time.

A splay tree is a binary tree that satisfies the following invariant:

* The tree is either empty, or
* The tree consists of a root node and two subtrees, left and right, and
* The root node's value is greater than all values in the left subtree, and
* The root node's value is less than all values in the right subtree.

The following figure shows an example of a splay tree:

![Splay Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Splay_tree_animation.gif/250px-Splay_tree_animation.gif)

Splay trees are self-balancing, meaning that the tree adjusts itself so that the most recently accessed elements are quick to access again. This is done by moving the accessed element to the root of the tree.

The following operations are supported by splay trees:

* Insertion
* Look-up
* Removal

All of these operations are performed in logarithmic time.

## Insertion

Insertion into a splay tree is similar to insertion into a binary search tree. First, we find the correct position for the new element by traversing the tree. Then, we insert the new element into the tree.

However, after insertion, we need to splay the new element to the root. This is done by a series of tree rotations.

The following figure shows an example of insertion into a splay tree:

![Insertion into a Splay Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b0/Splay-tree-insert.gif/250px-Splay-tree-insert.gif)

## Look-up

Look-up in a splay tree is similar to look-up in a binary search tree. First, we find the element that we are looking for by traversing the tree. Then, we return the element.

However, after look-up, we need to splay the element to the root. This is done by a series of tree rotations.

The following figure shows an example of look-up in a splay tree:

![Look-up in a Splay Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Splay-tree-lookup.gif/250px-Splay-tree-lookup.gif)

## Removal

Removal from a splay tree is similar to removal from a binary search tree. First, we find the element that we want to remove by traversing the tree. Then, we remove the element.

However, after removal, we need to splay the parent of the removed element to the root. This is done by a series of tree rotations.

The following figure shows an example of removal from a splay tree:

![Removal from a Splay Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Splay-tree-delete.gif/250px-Splay-tree-delete.gif)

## Implementation

A splay tree can be implemented as a binary search tree. The following pseudo-code shows an example of how to insert an element into a splay tree:

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

The following pseudo-code shows an example of how to look-up an element in a splay tree:

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

The following pseudo-code shows an example of how to remove an element from a splay tree:

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

## Complexity

The time complexity of the operations supported by splay trees is as follows:

* Insertion: O(log n)
* Look-up: O(log n)
* Removal: O(log n)

The space complexity of a splay tree is O(n), where n is the number of elements in the tree.