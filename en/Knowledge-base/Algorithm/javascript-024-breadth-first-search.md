---
title: [JavaScript] 024: Breadth-First Search
description: 
published: true
date: 2023-02-10T02:32:45.002Z
tags: 
editor: markdown
dateCreated: 2023-02-10T02:32:38.695Z
---

- [[JavaScript] 024: Búsqueda en amplitud***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-024-breadth-first-search)
{.links-list}
- [[JavaScript] 024：广度优先搜索***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-024-breadth-first-search)
{.links-list}
- [[JavaScript] 024: 너비 우선 검색***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-024-breadth-first-search)
{.links-list}


# JavaScript 024: Breadth-First Search

In this post we will be discussing breadth-first search (BFS) and how to implement it in JavaScript. Breadth-first search is an algorithm used to traverse a tree or graph. It starts at the root node and explores all of the neighbor nodes at the present depth before moving on to the nodes at the next depth level.

We can implement BFS in JavaScript using a queue. A queue is a data structure that allows us to store data in a first-in, first-out (FIFO) manner. That is, the data that is inserted first into the queue is the first data that is removed from the queue.

We can use an array to implement a queue. To enqueue data, we can use the array's push() method to add data to the end of the array. To dequeue data, we can use the array's shift() method to remove data from the beginning of the array.

Here is an example of a queue implemented using an array:

```javascript
var queue = [];

// enqueue data
queue.push(1);
queue.push(2);
queue.push(3);

// dequeue data
var data = queue.shift(); // data = 1
```

Now that we know how to implement a queue, let's take a look at how we can use it to implement BFS.

## BFS pseudocode

The pseudocode for the BFS algorithm is as follows:

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

## BFS code example

Here is a code example of the BFS algorithm implemented in JavaScript:

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

## BFS time complexity

The time complexity of the BFS algorithm is O(n), where n is the number of nodes in the tree. This is because the algorithm visits each node exactly once.

## BFS space complexity

The space complexity of the BFS algorithm is O(n), where n is the number of nodes in the tree. This is because the algorithm stores all of the nodes in the tree in the queue.