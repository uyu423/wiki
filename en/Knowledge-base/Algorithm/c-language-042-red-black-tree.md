---
title: [C Language] 042: Red-Black Tree
description: 
published: true
date: 2023-02-12T10:18:24.576Z
tags: 
editor: markdown
dateCreated: 2023-02-12T10:18:17.678Z
---

- [[Lenguaje C] 042: árbol rojo-negro***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-042-red-black-tree)
{.links-list}
- [【C语言】042：红黑树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-042-red-black-tree)
{.links-list}
- [[C언어] 042: 레드-블랙 트리***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-042-red-black-tree)
{.links-list}


# 042: Red-Black Tree

A Red-Black Tree is a self-balancing binary search tree in which every node has a color attribute, with the value being either "red" or "black". The following is a visual representation of a Red-Black Tree:

![Red Black Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Red-black_tree_example.svg/250px-Red-black_tree_example.svg.png)

Each node of a Red-Black Tree has the following attributes:

- **Key**: A key is a value used to identify a node. In the above example, the keys are the numbers 1 through 7.
- **Color**: A node can be either "red" or "black". The root node is always black.
- **Left Child**: A reference to the left child node.
- **Right Child**: A reference to the right child node.
- **Parent**: A reference to the parent node.

A Red-Black Tree has the following properties:

- **Property 1 (Red Nodes):** A node is red if and only if both of its children are black.
- **Property 2 (Black Nodes):** Every node is either red or black.
- **Property 3 (Root Node):** The root node is black.
- **Property 4 (Leaf Nodes):** All leaf nodes (nodes with no children) are black.
- **Property 5 (Red-Black Property):** If a node is red, then both of its children are black.
- **Property 6 (Paths):** All simple paths from a node to its descendant leaves contain the same number of black nodes.

The following is an example of a Red-Black Tree that does not satisfy Property 5 (Red-Black Property):

![Invalid Red Black Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5f/Invalid_red_black_tree.svg/200px-Invalid_red_black_tree.svg.png)

As you can see, the node with key 4 is red, but its left child is also red. This violates Property 5.

Now that we've seen what a Red-Black Tree is, let's take a look at how they are used.

## Applications

Red-Black Trees are used in a variety of applications, such as:

- **Database Indexes**: Red-Black Trees are often used as indexes in databases. This is because they can be quickly searched, inserted, and deleted.
- **Operating Systems**: Red-Black Trees are used in the Linux kernel for storing process information.
- **Word Processors**: Red-Black Trees are used in word processors to store information about the positions of words in a document.

## Implementation

Now that we've seen what a Red-Black Tree is and some of the applications they are used in, let's take a look at how they are implemented.

### Node

First, we need to create a Node class. This class will store the key, color, left child, right child, and parent of a node.

```java
public class Node {
    int key;
    boolean color;
    Node leftChild;
    Node rightChild;
    Node parent;

    public Node(int key, boolean color, Node leftChild, Node rightChild, Node parent) {
        this.key = key;
        this.color = color;
        this.leftChild = leftChild;
        this.rightChild = rightChild;
        this.parent = parent;
    }
}
```

### Tree

Next, we need to create a Tree class. This class will store the root node of the tree.

```java
public class Tree {
    Node root;

    public Tree() {
        this.root = null;
    }
}
```

### Insert

Now that we have a Node class and a Tree class, we can start implementing the Red-Black Tree. The first operation we'll implement is the insert operation.

To insert a node into a Red-Black Tree, we first need to find the correct place to insert it. We do this by using the binary search tree insert algorithm. Once we've found the correct place to insert the node, we need to set the node's color to red. Then, we need to check if the tree is still valid. If the tree is not valid, we need to fix it.

The following is the insert algorithm:

```java
public void insert(int key) {
    // Create a new node with the given key and color it red
    Node newNode = new Node(key, true, null, null, null);

    // Find the correct place to insert the new node
    Node currentNode = root;
    Node parentNode = null;
    while (currentNode != null) {
        parentNode = currentNode;
        if (key < currentNode.key) {
            currentNode = currentNode.leftChild;
        } else {
            currentNode = currentNode.rightChild;
        }
    }

    // Set the new node's parent
    newNode.parent = parentNode;

    // Insert the new node into the tree
    if (parentNode == null) {
        // The new node is the root node
        root = newNode;
    } else if (key < parentNode.key) {
        // The new node is the left child of the parent node
        parentNode.leftChild = newNode;
    } else {
        // The new node is the right child of the parent node
        parentNode.rightChild = newNode;
    }

    // Fix the tree
    fixTree(newNode);
}
```

### Fix Tree

Now that we've seen how to insert a node into a Red-Black Tree, let's take a look at how to fix the tree.

There are four cases we need to consider when fixing a Red-Black Tree:

- Case 1 (Node is the root node): If the node is the root node, then we simply need to set its color to black.
- Case 2 (Node is a red node with a black parent): If the node is a red node with a black parent, then we do nothing.
- Case 3 (Node is a red node with a red parent): If the node is a red node with a red parent, then we need to consider the colors of the node's uncle and grandparent. If the uncle is also red, then we simply need to set the colors of the node, parent, and uncle to black and the color of the grandparent to red. Then, we need to recursively call the fixTree() method on the grandparent node.

If the uncle is black, then we need to consider the orientation of the parent and node. If the parent and node are both left children or both right children, then we simply need to set the color of the parent to black and the color of the grandparent to red. Then, we need to recursively call the fixTree() method on the grandparent node.

If the parent and node are not both left children or both right children, then we need to perform a left rotation or right rotation. After the rotation, we need to set the color of the node to black and the color of the grandparent to red. Then, we need to recursively call the fixTree() method on the grandparent node.

- Case 4 (Node is a black node with a red parent): If the node is a black node with a red parent, then we need to consider the colors of the node's uncle and grandparent. If the uncle is also red, then we simply need to set the colors of the parent and uncle to black and the color of the grandparent to red. Then, we need to recursively call the fixTree() method on the grandparent node.

If the uncle is black, then we need to consider the orientation of the parent and node. If the parent and node are both left children or both right children, then we need to set the color of the parent to black. Then, we need to recursively call the fixTree() method on the parent node.

If the parent and node are not both left children or both right children, then we need to perform a left rotation or right rotation. After the rotation, we need to set the color of the grandparent to red. Then, we need to recursively call the fixTree() method on the grandparent node.

The following is the fixTree() algorithm:

```java
public void fixTree(Node node) {
    // Case 1 (Node is the root node)
    if (node.parent == null) {
        node.color = false;
        return;
    }

    // Case 2 (Node is a red node with a black parent)
    if (node.color && !node.parent.color) {
        return;
    }

    // Case 3 (Node is a red node with a red parent)
    if (node.color && node.parent.color) {
        Node uncle = getUncle(node);

        if (uncle != null && uncle.color) {
            // Set the colors of the node, parent, and uncle to black and the color of the grandparent to red
            node.parent.color = false;
            uncle.color = false;
            getGrandparent(node).color = true;

            // Recursively call the fixTree() method on the grandparent node
            fixTree(getGrandparent(node));
        } else {
            // Perform a left rotation or right rotation
            if (node == node.parent.rightChild && node.parent == getGrandparent(node).leftChild) {
                // Perform a left rotation
                leftRotate(node.parent);

                // Set the colors of the node and parent to black and the color of the grandparent to red
                node.color = false;
                node.leftChild.color = true;
            } else if (node == node.parent.leftChild && node.parent == getGrandparent(node).rightChild) {
                // Perform a right rotation
                rightRotate(node.parent);

                // Set the colors of the node and parent to black and the color of the grandparent to red
                node.color = false;
                node.rightChild.color = true;
            }

            // Case 4 (Node is a black node with a red parent)
            if (node == node.parent.leftChild) {
                // Perform a right rotation
                rightRotate(getGrandparent(node));
            } else {
                // Perform a left rotation
                leftRotate(getGrandparent(node));
            }

            // Set the color of the grandparent to red
            getGrandparent(node).color = true;

            // Set the color of the parent to black
            node.parent.color = false;
        }
    }
}
```

### Left Rotate

Now that we've seen how to fix a Red-Black Tree, let's take a look at how to perform a left rotation.

A left rotation is used to balance a tree when the right child of a node is heavier than the left child. The following is an example of a left rotation:

![Left Rotation](https://upload.wikimedia.org/wikipedia/commons/2/2d/Left-rotation.svg)

As you can see, the node that is being rotated is the node with key 3. The left child of this node is the node with key 2 and the right child is the node with key 4. After the rotation, the node with key 3 is the left child of the node with key 4 and the node with key 2 is the right child of the node with key 3.

The following is the leftRotate() algorithm:

```java
public void leftRotate(Node node) {
    // Check if the node has a right child
    if (node.rightChild == null) {
        return;
    }

    // Set the right child of the node to be the new root of the subtree
    Node newRoot = node.rightChild;

    // Set the left child of the new root to be the node's right child
    newRoot.leftChild = node;

    // Set the node's right child to be the new root's left child
    node.rightChild = newRoot.leftChild;

    // Set the new root's parent to be the node's parent
    newRoot.parent = node.parent;

    // Check if the node is the root node
    if (node.parent == null) {
        // Set the new root to be the root node
        root = newRoot;
    } else if (node == node.parent.leftChild) {
        // Set the new root to be the node's left child
        node.parent.leftChild = newRoot;
    } else {
        // Set the new root to be the node's right child
        node.parent.rightChild = newRoot;
    }

    // Set the node's parent to be the new root
    node.parent = newRoot;
}
```

### Right Rotate

Now that we've seen how to perform a left rotation, let's take a look at how to perform a right rotation.

A right rotation is used to balance a tree when the left child of a node is heavier than the right child. The following is an example of a right rotation:

![Right Rotation](https://upload.wikimedia.org/wikipedia/commons/d/d4/Right-rotation.svg)

As you can see, the node that is being rotated is the node with key 3. The left child of this node is the node with key 2 and the right child is the node with key 4. After the rotation, the node with key 3 is the right child of the node with key 2 and the node with key 4 is the left child of the node with key 3.

The following is the rightRotate() algorithm:

```java
public void rightRotate(Node node) {
    // Check if the node has a left child
    if (node.leftChild == null) {
        return;
    }

    // Set the left child of the node to be the new root of the subtree
    Node newRoot = node.leftChild;

    // Set the right child of the new root to be the node's left child
    newRoot.rightChild = node;

    // Set the node's left child to be the new root's right child
    node.leftChild = newRoot.rightChild;

    // Set the new root's parent to be the node's parent
    newRoot.parent = node.parent;

    // Check if the node is the root node
    if (node.parent == null) {
        // Set the new root to be the root node
        root = newRoot;
    } else if (node == node.parent.rightChild) {
        // Set the new root to be the node's right child
        node.parent.rightChild = newRoot;
    } else {
        // Set the new root to be the node's left child
        node.parent.leftChild = newRoot;
    }

    // Set the node's parent to be the new root
    node.parent = newRoot;
}
```

### Delete

Now that we've seen how to perform a right rotation, let's take a look at how to delete a node from a Red-Black Tree.

To delete a node from a Red-Black Tree, we first need to find the node to delete. We do this by using the binary search tree delete algorithm. Once we've found the node to delete, we need to check if the tree is still valid. If the tree is not valid, we need to fix it.

The following is the delete algorithm:

```java
public void delete(int key) {
    // Find the node to delete
    Node node = find(key);

    // Check if the node was found
    if (node == null) {
        return;
    }

    // Delete the node
    deleteNode(node);
}
```

### Delete Node

Now that we've seen how to delete a node from a Red-Black Tree, let's take a look at how to delete a node.

There are three cases we need to consider when deleting a node from a Red-Black