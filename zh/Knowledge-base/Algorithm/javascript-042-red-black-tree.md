---
title: [JavaScript] 042：红黑树
description: 
published: true
date: 2023-02-10T20:33:21.399Z
tags: 
editor: markdown
dateCreated: 2023-02-10T20:33:19.802Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 042: Red-Black Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-042-red-black-tree)
{.links-list}


# 红黑树

红黑树是一种自平衡二叉搜索树，其中每个节点都有一个额外的位，该位通常被解释为节点的颜色（红色或黑色）。这些树用于实现关联数组，关联数组可以映射到一组键值对。

这棵树的平衡属性用于在添加和删除元素时保持近似平衡的搜索树。树的平衡并不完美，但足以确保树不会显着不平衡。

红黑树背后的基本思想是以满足以下属性的方式将树的节点着色为红色或黑色：

1. 每个节点要么是红色要么是黑色。
2.根是黑色的。
3. 每片叶子 (NIL) 都是黑色的。
4. 如果一个节点是红色的，那么它的两个孩子都是黑色的。
5.对于每个节点，从该节点到后代叶子的所有简单路径都包含相同数量的黑色节点。

这些属性确保树是平衡的，因此树的高度为 O(log n)。

## 代码示例

下面是 JavaScript 中红黑树的简单实现。我们首先定义一个 Node 类，它有一个值、一种颜色以及左右子节点。

```javascript
class Node {
  constructor(value, color, left, right) {
    this.value = value;
    this.color = color;
    this.left = left;
    this.right = right;
  }
}
```

我们还需要一种方法来比较两个节点，以便我们可以以正确的顺序将它们插入到树中。我们可以使用比较函数来完成此操作，该函数接受两个节点并返回一个数字，指示第一个节点是小于、等于还是大于第二个节点。

```javascript
function compare(a, b) {
  if (a.value < b.value) {
    return -1;
  }
  if (a.value > b.value) {
    return 1;
  }
  return 0;
}
```

现在我们可以定义我们的红黑树类了。我们将从一个构造函数开始，它将一个比较函数作为参数。我们还将一个根节点初始化为空。

```javascript
class RedBlackTree {
  constructor(compare) {
    this.compare = compare;
    this.root = null;
  }
}
```

我们现在可以实现插入功能。此函数将一个值作为参数并将其插入到树中的正确位置。如果该值已经在树中，则不会再次插入。

```javascript
RedBlackTree.prototype.insert = function(value) {
  //create a new node
  let node = new Node(value, "red", null, null);

  //insert the node into the tree in the correct position
  if (this.root === null) {
    this.root = node;
  } else {
    let current = this.root;
    let parent;
    while (true) {
      parent = current;
      if (this.compare(node, current) < 0) {
        current = current.left;
        if (current === null) {
          parent.left = node;
          break;
        }
      } else if (this.compare(node, current) > 0) {
        current = current.right;
        if (current === null) {
          parent.right = node;
          break;
        }
      } else {
        //the value is already in the tree, so we don't insert it
        break;
      }
    }
  }

  //fix any violations of the red-black properties
  this.fixViolations(node);
};
```

请注意，我们不需要将新节点的颜色显式设置为红色，因为默认情况下它已设置为红色。

我们还需要实现一个 fixViolations 函数，该函数将节点作为参数并修复任何违反红黑属性的情况。

```javascript
RedBlackTree.prototype.fixViolations = function(node) {
  let current = node;
  let parent = current.parent;
  let grandParent = parent.parent;

  while (parent && parent.color === "red") {
    if (grandParent.left === parent) {
      //we are on the left side of the tree
      let uncle = grandParent.right;
      if (uncle && uncle.color === "red") {
        //case 1: the parent and uncle are both red
        parent.color = "black";
        uncle.color = "black";
        grandParent.color = "red";
        current = grandParent;
      } else {
        if (current === parent.right) {
          //case 2: the parent is red and the current node is on the right side
          //of the tree
          this.rotateLeft(parent);
          current = parent;
          parent = current.parent;
        }
        //case 3: the parent is red and the current node is on the left side
        //of the tree
        parent.color = "black";
        grandParent.color = "red";
        this.rotateRight(grandParent);
      }
    } else {
      //we are on the right side of the tree
      let uncle = grandParent.left;
      if (uncle && uncle.color === "red") {
        //case 1: the parent and uncle are both red
        parent.color = "black";
        uncle.color = "black";
        grandParent.color = "red";
        current = grandParent;
      } else {
        if (current === parent.left) {
          //case 2: the parent is red and the current node is on the left side
          //of the tree
          this.rotateRight(parent);
          current = parent;
          parent = current.parent;
        }
        //case 3: the parent is red and the current node is on the right side
        //of the tree
        parent.color = "black";
        grandParent.color = "red";
        this.rotateLeft(grandParent);
      }
    }
    parent = current.parent;
    grandParent = parent.parent;
  }

  //make sure the root node is black
  this.root.color = "black";
};
```

请注意，我们需要跟踪当前节点的父节点、祖父节点和叔叔节点，以及当前节点本身。

我们还需要实现 rotateLeft 和 rotateRight 功能。这些函数将节点作为参数并围绕该节点旋转树。

```javascript
RedBlackTree.prototype.rotateLeft = function(node) {
  let rightChild = node.right;
  node.right = rightChild.left;

  if (rightChild.left !== null) {
    rightChild.left.parent = node;
  }

  rightChild.parent = node.parent;

  if (node.parent === null) {
    this.root = rightChild;
  } else if (node === node.parent.left) {
    node.parent.left = rightChild;
  } else {
    node.parent.right = rightChild;
  }

  rightChild.left = node;
  node.parent = rightChild;
};

RedBlackTree.prototype.rotateRight = function(node) {
  let leftChild = node.left;
  node.left = leftChild.right;

  if (leftChild.right !== null) {
    leftChild.right.parent = node;
  }

  leftChild.parent = node.parent;

  if (node.parent === null) {
    this.root = leftChild;
  } else if (node === node.parent.right) {
    node.parent.right = leftChild;
  } else {
    node.parent.left = leftChild;
  }

  leftChild.right = node;
  node.parent = leftChild;
};
```

这些功能相当简单。我们只需要跟踪正在旋转的节点的父节点、子节点和孙节点。

我们还可以实现一个 remove 函数，它将一个值作为参数，并从树中删除具有该值的节点。

```javascript
RedBlackTree.prototype.remove = function(value) {
  //find the node to be removed
  let current = this.root;
  let parent = current;
  let isLeftChild = true;
  while (current.value !== value) {
    parent = current;
    if (this.compare(value, current) < 0) {
      //the value is less than the current node, so go to the left child
      isLeftChild = true;
      current = current.left;
    } else {
      //the value is greater than the current node, so go to the right child
      isLeftChild = false;
      current = current.right;
    }
    if (current === null) {
      //the value is not in the tree
      return false;
    }
  }

  //case 1: the node to be removed is a leaf
  if (current.left === null && current.right === null) {
    if (current === this.root) {
      //the tree is empty
      this.root = null;
    } else if (isLeftChild) {
      //the node is a left child
      parent.left = null;
    } else {
      //the node is a right child
      parent.right = null;
    }
  }
  //case 2: the node to be removed has one child
  else if (current.right === null) {
    //the node is a left child
    if (current === this.root) {
      this.root = current.left;
    } else if (isLeftChild) {
      parent.left = current.left;
    } else {
      parent.right = current.left;
    }
  } else if (current.left === null) {
    //the node is a right child
    if (current === this.root) {
      this.root = current.right;
    } else if (isLeftChild) {
      parent.left = current.right;
    } else {
      parent.right = current.right;
    }
  }
  //case 3: the node to be removed has two children
  else {
    //find the successor of the node to be removed
    let successor = this.getSuccessor(current);

    //connect the parent of the current node to the successor
    if (current === this.root) {
      this.root = successor;
    } else if (isLeftChild) {
      parent.left = successor;
    } else {
      parent.right = successor;
    }

    //connect the left child of the current node to the successor
    successor.left = current.left;
  }

  //fix any violations of the red-black properties
  this.fixViolations(node);

  //return true to indicate that the node was removed
  return true;
};
```

该函数类似于插入函数。我们只需要跟踪被删除节点的父节点、子节点和孙节点。

我们还需要实现一个 getSuccessor 函数，它将一个节点作为参数并返回该节点的后继节点。

```javascript
RedBlackTree.prototype.getSuccessor = function(node) {
  let current = node.right;
  let parent = node;
  while (current.left !== null) {
    parent = current;
    current = current.left;
  }
  if (current !== node.right) {
    parent.left = current.right;
    current.right = node.right;
  }
  return current;
};
```

此功能类似于删除功能。我们只需要跟踪被删除节点的父节点、子节点和孙节点。

## 相关练习

- []实现一个函数来检查二叉树是否是二叉搜索树。
- [] 实现一个函数来查找二叉搜索树中第 k 个最小的元素。