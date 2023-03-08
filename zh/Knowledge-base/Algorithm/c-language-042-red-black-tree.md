---
title: 【C语言】042：红黑树
description: 
published: true
date: 2023-02-12T10:18:19.380Z
tags: 
editor: markdown
dateCreated: 2023-02-12T10:18:17.671Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 042: Red-Black Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-042-red-black-tree)
{.links-list}


# 042：红黑树

红黑树是一种自平衡二叉搜索树，其中每个节点都有一个颜色属性，值为“红色”或“黑色”。以下是红黑树的可视化表示：

![红黑树](https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Red-black_tree_example.svg/250px-Red-black_tree_example.svg.png)

红黑树的每个节点都有以下属性：

- **键**：键是用于标识节点的值。在上面的示例中，键是数字 1 到 7。
- **颜色**：节点可以是“红色”或“黑色”。根节点始终为黑色。
- **Left Child**：对左子节点的引用。
- **Right Child**：对右子节点的引用。
- **Parent**：对父节点的引用。

红黑树具有以下属性：

- **属性 1（红色节点）：**当且仅当它的两个子节点都是黑色时，一个节点是红色的。
- **属性 2（黑色节点）：**每个节点都是红色或黑色。
- **属性 3（根节点）：**根节点为黑色。
- **属性 4（叶节点）：**所有叶节点（没有子节点的节点）都是黑色的。
- **属性 5（红黑属性）：**如果一个节点是红色的，那么它的两个孩子都是黑色的。
- **属性 6（路径）：**从节点到其后代叶子的所有简单路径都包含相同数量的黑色节点。

下面是一个不满足属性5（Red-Black Property）的红黑树的例子：

![无效的红黑树](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5f/Invalid_red_black_tree.svg/200px-Invalid_red_black_tree.svg.png)

如您所见，键为 4 的节点是红色的，但它的左子节点也是红色的。这违反了性质 5。

现在我们已经了解了什么是红黑树，让我们来看看它们是如何使用的。

## 应用

红黑树用于各种应用，例如：

- **数据库索引**：红黑树通常用作数据库中的索引。这是因为可以快速搜索、插入和删除它们。
- **操作系统**：红黑树在 Linux 内核中用于存储进程信息。
- **文字处理器**：文字处理器中使用红黑树来存储有关文字在文档中的位置的信息。

## 执行

现在我们已经了解了红黑树是什么以及使用它们的一些应用程序，让我们来看看它们是如何实现的。

### 节点

首先，我们需要创建一个 Node 类。此类将存储节点的键、颜色、左子节点、右子节点和父节点。

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

### 树

接下来，我们需要创建一个 Tree 类。这个类将存储树的根节点。

```java
public class Tree {
    Node root;

    public Tree() {
        this.root = null;
    }
}
```

### 插入

现在我们有了一个 Node 类和一个 Tree 类，我们可以开始实现红黑树了。我们要实现的第一个操作是插入操作。

要将节点插入到红黑树中，我们首先需要找到正确的插入位置。我们通过使用二叉搜索树插入算法来做到这一点。找到插入节点的正确位置后，我们需要将节点的颜色设置为红色。然后，我们需要检查树是否仍然有效。如果树无效，我们需要修复它。

下面是插入算法：

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

### 修复树

现在我们已经了解了如何将节点插入到红黑树中，让我们来看看如何修复树。

在修复红黑树时，我们需要考虑四种情况：

- Case 1 (Node is the root node): 如果节点是根节点，那么我们只需要将它的颜色设置为黑色即可。
- Case 2 (Node is a red node with a black parent)：如果节点是红色节点，父节点为黑色，那么我们什么都不做。
- 情况 3（节点是红色节点，父节点为红色）：如果节点是红色节点，父节点为红色，那么我们需要考虑节点的叔叔和祖父母的颜色。如果叔叔也是红色的，那么我们只需要将节点、父节点和叔叔的颜色设置为黑色，将祖父母的颜色设置为红色即可。然后，我们需要在祖父节点上递归调用 fixTree() 方法。

如果叔叔是黑色的，那么我们需要考虑父节点和节点的方向。如果父节点和节点都是左孩子或都是右孩子，那么我们只需要将父节点的颜色设置为黑色，将祖父母的颜色设置为红色即可。然后，我们需要在祖父节点上递归调用 fixTree() 方法。

如果父节点和节点既不是左孩子也不是右孩子，那么我们需要进行左旋转或右旋转。旋转后，我们需要将节点的颜色设置为黑色，将祖父母的颜色设置为红色。然后，我们需要在祖父节点上递归调用 fixTree() 方法。

- 情况 4（节点是黑色节点，父节点是红色）：如果节点是黑色节点，父节点是红色，那么我们需要考虑节点的叔叔和祖父母的颜色。如果叔叔也是红色的，那么我们只需要将父母和叔叔的颜色设置为黑色，将祖父母的颜色设置为红色。然后，我们需要在祖父节点上递归调用 fixTree() 方法。

如果叔叔是黑色的，那么我们需要考虑父节点和节点的方向。如果父节点和节点都是左孩子或者都是右孩子，那么我们需要将父节点的颜色设置为黑色。然后，我们需要在父节点上递归调用 fixTree() 方法。

如果父节点和节点既不是左孩子也不是右孩子，那么我们需要进行左旋转或右旋转。旋转后，我们需要将祖父母的颜色设置为红色。然后，我们需要在祖父节点上递归调用 fixTree() 方法。

以下是 fixTree() 算法：

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

### 左旋转

现在我们已经了解了如何修复红黑树，让我们来看看如何执行左旋转。

当节点的右孩子比左孩子重时，左旋转用于平衡树。下面是一个左旋转的例子：

![左旋转](https://upload.wikimedia.org/wikipedia/commons/2/2d/Left-rotation.svg)

如您所见，正在旋转的节点是键为 3 的节点。该节点的左孩子是键为 2 的节点，右孩子是键为 4 的节点。旋转后，键为 3 的节点是键为 4 的节点的左孩子，键为 2 的节点是键为 3 的节点的右孩子。

以下是 leftRotate() 算法：

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

### 向右旋转

现在我们已经了解了如何执行左旋转，让我们来看看如何执行右旋转。

当节点的左孩子比右孩子重时，右旋转用于平衡树。以下是右旋转的示例：

![右旋转](https://upload.wikimedia.org/wikipedia/commons/d/d4/Right-rotation.svg)

如您所见，正在旋转的节点是键为 3 的节点。该节点的左孩子是键为 2 的节点，右孩子是键为 4 的节点。旋转后，键为 3 的节点是键为 2 的节点的右孩子，键为 4 的节点是键为 3 的节点的左孩子。

下面是rightRotate()算法：

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

### 删除

现在我们已经了解了如何执行右旋转，让我们看一下如何从红黑树中删除节点。

要从红黑树中删除节点，我们首先需要找到要删除的节点。我们通过使用二叉搜索树删除算法来做到这一点。找到要删除的节点后，我们需要检查树是否仍然有效。如果树无效，我们需要修复它。

下面是删除算法：

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

### 删除节点

既然我们已经了解了如何从红黑树中删除节点，那么让我们看一下如何删除节点。

从 Red-Black 中删除节点时，我们需要考虑三种情况