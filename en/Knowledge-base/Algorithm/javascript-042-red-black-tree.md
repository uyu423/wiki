---
title: [JavaScript] 042: Red-Black Tree
description: 
published: true
date: 2023-02-10T20:33:26.449Z
tags: 
editor: markdown
dateCreated: 2023-02-10T20:33:19.815Z
---

- [[JavaScript] 042: Árbol rojo-negro***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-042-red-black-tree)
{.links-list}
- [[JavaScript] 042：红黑树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-042-red-black-tree)
{.links-list}
- [[JavaScript] 042: 레드-블랙 트리***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-042-red-black-tree)
{.links-list}


# Red-Black Tree

A red-black tree is a kind of self-balancing binary search tree in which each node has an extra bit, and that bit is often interpreted as the color (red or black) of the node. These trees are used to implement associative arrays, which can be mapped to a set of key-value pairs.

The balanced property of this tree is used to maintain an approximately balanced search tree as elements are added and removed. The balance of the tree is not perfect, but it is good enough to ensure that the tree is not significantly unbalanced.

The basic idea behind a red-black tree is to color the nodes of the tree red or black in such a way that the following properties are satisfied:

1.  Every node is either red or black.
2.  The root is black.
3.  Every leaf (NIL) is black.
4.  If a node is red, then both its children are black.
5.  For each node, all simple paths from the node to descendant leaves contain the same number of black nodes.

These properties ensure that the tree is balanced, so that the height of the tree is O(log n).

## Code Examples

Here is a simple implementation of a red-black tree in JavaScript. We start by defining a Node class, which has a value, a color, and left and right child nodes.

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

We also need a way to compare two nodes, so that we can insert them into the tree in the correct order. We can do this with a compare function, which takes two nodes and returns a number indicating whether the first node is less than, equal to, or greater than the second node.

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

Now we can define our red-black tree class. We'll start with a constructor function, which takes a compare function as an argument. We'll also initialize a root node to null.

```javascript
class RedBlackTree {
  constructor(compare) {
    this.compare = compare;
    this.root = null;
  }
}
```

We can now implement the insert function. This function takes a value as an argument and inserts it into the tree in the correct position. If the value is already in the tree, it will not be inserted again.

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

Note that we don't need to explicitly set the color of the new node to red, as it is already set to red by default.

We also need to implement a fixViolations function, which takes a node as an argument and fixes any violations of the red-black properties.

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

Note that we need to keep track of the parent, grandparent, and uncle of the current node, as well as the current node itself.

We also need to implement rotateLeft and rotateRight functions. These functions take a node as an argument and rotate the tree around that node.

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

These functions are fairly simple. We just need to keep track of the parent, child, and grandchild of the node being rotated.

We can also implement a remove function, which takes a value as an argument and removes the node with that value from the tree.

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

This function is similar to the insert function. We just need to keep track of the parent, child, and grandchild of the node being removed.

We also need to implement a getSuccessor function, which takes a node as an argument and returns the successor of that node.

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

This function is similar to the remove function. We just need to keep track of the parent, child, and grandchild of the node being removed.

## Related Exercises

- [ ] Implement a function to check if a binary tree is a binary search tree.
- [ ] Implement a function to find the kth smallest element in a binary search tree.