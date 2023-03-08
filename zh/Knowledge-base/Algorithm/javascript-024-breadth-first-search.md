---
title: [JavaScript] 024：广度优先搜索
description: 
published: true
date: 2023-02-10T02:32:40.307Z
tags: 
editor: markdown
dateCreated: 2023-02-10T02:32:38.688Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 024: Breadth-First Search***English** document is available*](/en/Knowledge-base/Algorithm/javascript-024-breadth-first-search)
{.links-list}


# JavaScript 024：广度优先搜索

在这篇文章中，我们将讨论广度优先搜索 (BFS) 以及如何在 JavaScript 中实现它。广度优先搜索是一种用于遍历树或图的算法。它从根节点开始，探索当前深度的所有邻居节点，然后再移动到下一个深度级别的节点。

我们可以使用队列在 JavaScript 中实现 BFS。队列是一种数据结构，它允许我们以先进先出（FIFO）的方式存储数据。也就是说，最先插入队列的数据是最先从队列中移除的数据。

我们可以使用数组来实现队列。要入队数据，我们可以使用数组的 push() 方法将数据添加到数组的末尾。要使数据出列，我们可以使用数组的 shift() 方法从数组的开头删除数据。

以下是使用数组实现的队列示例：

```javascript
var queue = [];

// enqueue data
queue.push(1);
queue.push(2);
queue.push(3);

// dequeue data
var data = queue.shift(); // data = 1
```

现在我们知道了如何实现队列，让我们来看看如何使用它来实现 BFS。

## BFS 伪代码

BFS算法的伪代码如下：

```
function BFS(root) {
    
    // create a queue and enqueue the root node
    var queue = [];
    queue.push(root);
    
    // while the queue is not empty
    while (queue.length > 0) {
        
        // dequeue a node from the queue
        var node = queue.shift();
        
        // if the node is not null
        if (node != null) {
            
            // process the node
            console.log(node.data);
            
            // enqueue the node's children
            queue.push(node.left);
            queue.push(node.right);
        }
    }
}
```

## BFS 代码示例

下面是一个用 JavaScript 实现的 BFS 算法的代码示例：

```javascript
// Node class
function Node(data) {
    this.data = data;
    this.left = null;
    this.right = null;
}

// Binary Search Tree class
function BinarySearchTree() {
    this.root = null;
}

// insert method
BinarySearchTree.prototype.insert = function(data) {
    var newNode = new Node(data);
    
    if (this.root === null) {
        this.root = newNode;
    } else {
        this.insertNode(this.root, newNode);
    }
}

// insertNode method
BinarySearchTree.prototype.insertNode = function(node, newNode) {
    if (newNode.data < node.data) {
        if (node.left === null) {
            node.left = newNode;
        } else {
            this.insertNode(node.left, newNode);
        }
    } else {
        if (node.right === null) {
            node.right = newNode;
        } else {
            this.insertNode(node.right, newNode);
        }
    }
}

// inorderTraverse method
BinarySearchTree.prototype.inorderTraverse = function(callback) {
    this.inorderTraverseNode(this.root, callback);
}

// inorderTraverseNode method
BinarySearchTree.prototype.inorderTraverseNode = function(node, callback) {
    if (node != null) {
        this.inorderTraverseNode(node.left, callback);
        callback(node.data);
        this.inorderTraverseNode(node.right, callback);
    }
}

// BFS method
BinarySearchTree.prototype.BFS = function() {
    
    // create a queue and enqueue the root node
    var queue = [];
    queue.push(this.root);
    
    // while the queue is not empty
    while (queue.length > 0) {
        
        // dequeue a node from the queue
        var node = queue.shift();
        
        // if the node is not null
        if (node != null) {
            
            // process the node
            console.log(node.data);
            
            // enqueue the node's children
            queue.push(node.left);
            queue.push(node.right);
        }
    }
}

// test
var tree = new BinarySearchTree();
tree.insert(1);
tree.insert(2);
tree.insert(3);
tree.insert(4);
tree.insert(5);
tree.insert(6);
tree.insert(7);
tree.insert(8);
tree.insert(9);
tree.BFS(); // 1 2 3 4 5 6 7 8 9
```

## BFS 时间复杂度

BFS 算法的时间复杂度为 O(n)，其中 n 是树中的节点数。这是因为该算法只访问每个节点一次。

## BFS 空间复杂度

BFS 算法的空间复杂度为 O(n)，其中 n 是树中的节点数。这是因为该算法将树中的所有节点都存储在队列中。