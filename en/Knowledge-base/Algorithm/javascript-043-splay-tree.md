---
title: [JavaScript] 043: Splay Tree
description: 
published: true
date: 2023-02-10T21:33:32.518Z
tags: 
editor: markdown
dateCreated: 2023-02-10T21:33:25.931Z
---

- [[JavaScript] 043: Árbol Splay***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-043-splay-tree)
{.links-list}
- [[JavaScript] 043：八叉树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-043-splay-tree)
{.links-list}
- [[JavaScript] 043: 스플레이 트리***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-043-splay-tree)
{.links-list}


# Splay Tree

A splay tree is a self-balancing binary search tree with the property that recently accessed elements are quick to access again. It performs basic operations such as insertion, look-up and removal in O(log(n)) time.

A splay tree is a binary tree that satisfies the following invariant:

```
After each operation, the node that was accessed is moved to the root of the tree.
```

This means that the node that is accessed most frequently will end up near the root of the tree, making it quick to access.

## Operations

The basic operations that can be performed on a splay tree are insertion, look-up and removal.

### Insertion

To insert a new node into the tree, we first need to find the correct position for it. We do this by starting at the root and traversing the tree until we find the node that is greater than the one we are inserting. We then insert the new node as a child of that node.

Once the new node has been inserted, we need to splay it to the root. To do this, we first make the new node the root of the tree. Then, we keep track of the node that was previously the root (now the new node's parent) and make it the new node's left child. Finally, we make the new node's right child the previous root.

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

### Look-up

To look up a value in the tree, we start at the root and traverse the tree until we find the value or we reach a node where the value would be if it were in the tree.

Once we find the node, we splay it to the root. If the value is not in the tree, the node that we end up splaying to the root will be the node where the value would be if it were in the tree.

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

### Removal

To remove a value from the tree, we first need to find the node that contains the value. We do this by starting at the root and traversing the tree until we find the value or we reach a node where the value would be if it were in the tree.

If the value is in the tree, we remove the node and splay its parent to the root. If the value is not in the tree, we splay the node where the value would be if it were in the tree to the root.

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

## Splaying

Splaying is the process of moving a node to the root of the tree. This is done by a series of rotations. The type of rotation performed depends on the position of the node relative to the root.

There are three possible cases:

- The node is the root: no rotation is needed.
- The node is a child of the root: a single rotation is needed.
- The node is not a child of the root: a double rotation is needed.

### Single Rotation

A single rotation is performed when the node to be splayed is a child of the root. There are two possible cases, depending on whether the node is the root's left child or right child.

#### Left Rotation

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

#### Right Rotation

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

### Double Rotation

A double rotation is performed when the node to be splayed is not a child of the root. There are four possible cases, depending on whether the node is the root's left child or right child and whether the node's parent is the root's left child or right child.

#### Left-Right Rotation

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

#### Right-Left Rotation

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

## Complexity

The time complexity of the operations on a splay tree is amortized O(log(n)). This means that, on average, the operations will take O(log(n)) time. However, in the worst case, they can take O(n) time.

The space complexity of a splay tree is O(n), where n is the number of nodes in the tree.