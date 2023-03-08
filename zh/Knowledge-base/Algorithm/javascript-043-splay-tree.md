---
title: [JavaScript] 043：八叉树
description: 
published: true
date: 2023-02-10T21:33:27.656Z
tags: 
editor: markdown
dateCreated: 2023-02-10T21:33:25.922Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 043: Splay Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-043-splay-tree)
{.links-list}


# 张开树

splay 树是一种自平衡二叉搜索树，具有最近访问过的元素可以快速再次访问的特性。它在 O(log(n)) 时间内执行基本操作，例如插入、查找和删除。

splay 树是满足以下不变量的二叉树：

```
After each operation, the node that was accessed is moved to the root of the tree.
```

这意味着最常访问的节点将在树的根部附近结束，从而可以快速访问。

## 操作

可以在 splay 树上执行的基本操作是插入、查找和删除。

### 插入

要在树中插入一个新节点，我们首先需要为它找到正确的位置。为此，我们从根开始遍历树，直到找到比我们插入的节点大的节点。然后我们将新节点作为该节点的子节点插入。

插入新节点后，我们需要将其展开到根节点。为此，我们首先使新节点成为树的根。然后，我们跟踪以前是根的节点（现在是新节点的父节点）并使它成为新节点的左子节点。最后，我们让新节点的右孩子成为前一个根。

```javascript
function insert(value) {
    if (root === null) {
        root = new Node(value);
        return;
    }
 
    var curr = root;
    var parent = null;
    while (curr !== null) {
        if (value < curr.value) {
            parent = curr;
            curr = curr.left;
        } else if (value > curr.value) {
            parent = curr;
            curr = curr.right;
        } else {
            // value already exists in tree
            return;
        }
    }
 
    var newNode = new Node(value);
    if (value < parent.value) {
        parent.left = newNode;
    } else {
        parent.right = newNode;
    }
 
    // splay newNode to the root
    splay(newNode);
}
```

### 抬头

要在树中查找值，我们从根开始并遍历树，直到找到该值或者我们到达一个节点，如果它在树中，该节点就是该值。

找到节点后，我们将其展开到根。如果值不在树中，我们最终展开到根的节点将是值在树中时所在的节点。

```javascript
function lookup(value) {
    if (root === null) {
        return null;
    }
 
    var curr = root;
    while (curr !== null) {
        if (value < curr.value) {
            curr = curr.left;
        } else if (value > curr.value) {
            curr = curr.right;
        } else {
            // value found
            break;
        }
    }
 
    splay(curr);
    return curr;
}
```

### 移动

要从树中删除一个值，我们首先需要找到包含该值的节点。我们通过从根开始并遍历树直到找到值或到达一个节点，如果它在树中，该节点就是该值。

如果该值在树中，我们删除该节点并将其父节点展开到根节点。如果该值不在树中，则将值在树中的节点展开到根。

```javascript
function remove(value) {
    if (root === null) {
        return;
    }
 
    var curr = root;
    while (curr !== null) {
        if (value < curr.value) {
            curr = curr.left;
        } else if (value > curr.value) {
            curr = curr.right;
        } else {
            // value found
            break;
        }
    }
 
    if (curr === null) {
        // value not in tree
        return;
    }
 
    // remove curr
    if (curr.left === null && curr.right === null) {
        // curr is a leaf
        if (curr === root) {
            root = null;
        } else {
            var parent = curr.parent;
            if (parent.left === curr) {
                parent.left = null;
            } else {
                parent.right = null;
            }
 
            splay(parent);
        }
    } else if (curr.left === null) {
        // curr has only right child
        if (curr === root) {
            root = curr.right;
            root.parent = null;
        } else {
            var parent = curr.parent;
            curr.right.parent = parent;
            if (parent.left === curr) {
                parent.left = curr.right;
            } else {
                parent.right = curr.right;
            }
 
            splay(parent);
        }
    } else if (curr.right === null) {
        // curr has only left child
        if (curr === root) {
            root = curr.left;
            root.parent = null;
        } else {
            var parent = curr.parent;
            curr.left.parent = parent;
            if (parent.left === curr) {
                parent.left = curr.left;
            } else {
                parent.right = curr.left;
            }
 
            splay(parent);
        }
    } else {
        // curr has both left and right child
        var next = curr.right;
        while (next.left !== null) {
            next = next.left;
        }
 
        // next is the successor of curr (the smallest node in curr's right subtree)
        // remove next from its current position and replace it with its right child
        var parent = next.parent;
        if (parent.left === next) {
            parent.left = next.right;
        } else {
            parent.right = next.right;
        }
        if (next.right !== null) {
            next.right.parent = parent;
        }
 
        // replace curr with next
        next.left = curr.left;
        next.right = curr.right;
        next.parent = curr.parent;
        curr.left.parent = next;
        curr.right.parent = next;
        if (curr === root) {
            root = next;
        } else {
            if (curr.parent.left === curr) {
                curr.parent.left = next;
            } else {
                curr.parent.right = next;
            }
        }
 
        splay(next);
    }
}
```

## 展开

展开是将节点移动到树根的过程。这是通过一系列旋转来完成的。执行的旋转类型取决于节点相对于根的位置。

存在三种可能的情况：

- 节点是根：不需要旋转。
- 该节点是根的子节点：需要单次旋转。
- 该节点不是根的子节点：需要进行双重旋转。

### 单次旋转

当要展开的节点是根的子节点时，将执行一次旋转。有两种可能的情况，取决于节点是根的左孩子还是右孩子。

#### 左旋转

```javascript
function leftRotate(node) {
    var rightChild = node.right;
    node.right = rightChild.left;
    if (rightChild.left !== null) {
        rightChild.left.parent = node;
    }
    rightChild.parent = node.parent;
    if (node.parent === null) {
        root = rightChild;
    } else if (node === node.parent.left) {
        node.parent.left = rightChild;
    } else {
        node.parent.right = rightChild;
    }
    rightChild.left = node;
    node.parent = rightChild;
}
```

#### 右旋转

```javascript
function rightRotate(node) {
    var leftChild = node.left;
    node.left = leftChild.right;
    if (leftChild.right !== null) {
        leftChild.right.parent = node;
    }
    leftChild.parent = node.parent;
    if (node.parent === null) {
        root = leftChild;
    } else if (node === node.parent.right) {
        node.parent.right = leftChild;
    } else {
        node.parent.left = leftChild;
    }
    leftChild.right = node;
    node.parent = leftChild;
}
```

### 双旋转

当要展开的节点不是根的子节点时，将执行双旋转。有四种可能的情况，取决于节点是根的左孩子还是右孩子，以及节点的父节点是根的左孩子还是右孩子。

#### 左右旋转

```javascript
function leftRightRotate(node) {
    var leftChild = node.left;
    var leftRightChild = leftChild.right;
    leftChild.right = leftRightChild.left;
    if (leftRightChild.left !== null) {
        leftRightChild.left.parent = leftChild;
    }
    node.left = leftRightChild.right;
    if (leftRightChild.right !== null) {
        leftRightChild.right.parent = node;
    }
    leftRightChild.left = leftChild;
    leftRightChild.right = node;
    leftChild.parent = leftRightChild;
    node.parent = leftRightChild;
    leftRightChild.parent = node.parent;
    if (node.parent === null) {
        root = leftRightChild;
    } else if (node === node.parent.left) {
        node.parent.left = leftRightChild;
    } else {
        node.parent.right = leftRightChild;
    }
}
```

#### 左右旋转

```javascript
function rightLeftRotate(node) {
    var rightChild = node.right;
    var rightLeftChild = rightChild.left;
    rightChild.left = rightLeftChild.right;
    if (rightLeftChild.right !== null) {
        rightLeftChild.right.parent = rightChild;
    }
    node.right = rightLeftChild.left;
    if (rightLeftChild.left !== null) {
        rightLeftChild.left.parent = node;
    }
    rightLeftChild.right = rightChild;
    rightLeftChild.left = node;
    rightChild.parent = rightLeftChild;
    node.parent = rightLeftChild;
    rightLeftChild.parent = node.parent;
    if (node.parent === null) {
        root = rightLeftChild;
    } else if (node === node.parent.left) {
        node.parent.left = rightLeftChild;
    } else {
        node.parent.right = rightLeftChild;
    }
}
```

## 复杂性

splay 树上操作的时间复杂度为 O(log(n))。这意味着，平均而言，这些操作将花费 O(log(n)) 时间。然而，在最坏的情况下，它们可能需要 O(n) 的时间。

splay 树的空间复杂度为 O(n)，其中 n 是树中的节点数。