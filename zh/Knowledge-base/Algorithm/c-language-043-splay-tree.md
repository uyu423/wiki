---
title: 【C语言】043：八叉树
description: 
published: true
date: 2023-02-10T07:55:35.686Z
tags: 
editor: markdown
dateCreated: 2023-02-10T07:55:34.089Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 043: Splay Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-043-splay-tree)
{.links-list}


# 张开树

splay 树是一种自平衡二叉搜索树，具有最近访问过的元素可以快速再次访问的附加属性。它以对数时间执行插入、查找和删除等基本操作。

splay 树是满足以下不变量的二叉树：

* 树要么是空的，要么
* 树由一个根节点和左右两个子树组成
* 根节点的值大于左子树中的所有值，并且
* 根节点的值小于右子树中的所有值。

下图显示了一个 splay 树的示例：

![张开树](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Splay_tree_animation.gif/250px-Splay_tree_animation.gif)

Splay 树是自平衡的，这意味着树会自我调整，以便可以快速再次访问最近访问的元素。这是通过将访问的元素移动到树的根来完成的。

展开树支持以下操作：

* 插入
* 抬头
* 移动

所有这些操作都以对数时间执行。

## 插入

插入 splay 树类似于插入二叉搜索树。首先，我们通过遍历树找到新元素的正确位置。然后，我们将新元素插入到树中。

但是，插入后，我们需要将新元素展开到根。这是通过一系列树旋转来完成的。

下图展示了一个插入splay tree的例子：

![插入 Splay 树](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b0/Splay-tree-insert.gif/250px-Splay-tree-insert.gif)

## 抬头

在 splay 树中查找类似于在二叉搜索树中查找。首先，我们通过遍历树找到我们要找的元素。然后，我们返回元素。

但是，在查找之后，我们需要将元素展开到根。这是通过一系列树旋转来完成的。

下图显示了在展开树中查找的示例：

![在 Splay 树中查找](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Splay-tree-lookup.gif/250px-Splay-tree-lookup.gif)

## 移动

从 splay 树中删除类似于从二叉搜索树中删除。首先，我们通过遍历树找到要删除的元素。然后，我们删除元素。

但是，在移除之后，我们需要将被移除元素的父元素展开到根。这是通过一系列树旋转来完成的。

下图显示了从 splay 树中删除的示例：

![从 Splay 树中移除](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Splay-tree-delete.gif/250px-Splay-tree-delete.gif)

## 执行

展开树可以实现为二叉搜索树。以下伪代码显示了如何将元素插入 splay 树的示例：

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

以下伪代码显示了如何在展开树中查找元素的示例：

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

以下伪代码显示了如何从 splay 树中删除元素的示例：

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

## 复杂性

splay tree支持的操作的时间复杂度如下：

* 插入：O(log n)
* 查找：O(log n)
* 移除：O(log n)

splay 树的空间复杂度为 O(n)，其中 n 是树中元素的数量。