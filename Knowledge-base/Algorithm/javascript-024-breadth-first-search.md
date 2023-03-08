---
title: [JavaScript] 024: 너비 우선 검색
description: 
published: true
date: 2023-02-10T02:32:40.319Z
tags: 
editor: markdown
dateCreated: 2023-02-10T02:32:38.691Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 024: Breadth-First Search***English** document is available*](/en/Knowledge-base/Algorithm/javascript-024-breadth-first-search)
{.links-list}


# JavaScript 024: 너비 우선 검색

이 게시물에서는 너비 우선 검색(BFS)과 JavaScript에서 이를 구현하는 방법에 대해 논의할 것입니다. 너비 우선 탐색은 트리 또는 그래프를 순회하는 데 사용되는 알고리즘입니다. 루트 노드에서 시작하여 다음 깊이 수준의 노드로 이동하기 전에 현재 깊이의 모든 이웃 노드를 탐색합니다.

대기열을 사용하여 JavaScript에서 BFS를 구현할 수 있습니다. 큐는 선입선출(FIFO) 방식으로 데이터를 저장할 수 있는 데이터 구조입니다. 즉, 큐에 가장 먼저 삽입되는 데이터가 큐에서 제거되는 첫 번째 데이터입니다.

배열을 사용하여 대기열을 구현할 수 있습니다. 데이터를 대기열에 넣기 위해 배열의 push() 메서드를 사용하여 배열 끝에 데이터를 추가할 수 있습니다. 데이터를 대기열에서 빼기 위해 배열의 shift() 메서드를 사용하여 배열의 시작 부분에서 데이터를 제거할 수 있습니다.

다음은 배열을 사용하여 구현된 대기열의 예입니다.

```javascript
var queue = [];

// enqueue data
queue.push(1);
queue.push(2);
queue.push(3);

// dequeue data
var data = queue.shift(); // data = 1
```

이제 대기열을 구현하는 방법을 알았으므로 대기열을 사용하여 BFS를 구현하는 방법을 살펴보겠습니다.

## BFS 의사 코드

BFS 알고리즘의 의사 코드는 다음과 같습니다.

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

## BFS 코드 예제

다음은 JavaScript로 구현된 BFS 알고리즘의 코드 예제입니다.

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

## BFS 시간 복잡도

BFS 알고리즘의 시간 복잡도는 O(n)이며, 여기서 n은 트리의 노드 수입니다. 이는 알고리즘이 각 노드를 정확히 한 번만 방문하기 때문입니다.

## BFS 공간 복잡도

BFS 알고리즘의 공간 복잡도는 O(n)이며, 여기서 n은 트리의 노드 수입니다. 이는 알고리즘이 트리의 모든 노드를 대기열에 저장하기 때문입니다.