---
title: [C Language] 024: Breadth-First Search
description: 
published: true
date: 2023-02-13T06:32:56.604Z
tags: 
editor: markdown
dateCreated: 2023-02-13T06:32:49.440Z
---

- [[Lenguaje C] 024: Búsqueda en amplitud***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-024-breadth-first-search)
{.links-list}
- [[C语言]024：广度优先搜索***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-024-breadth-first-search)
{.links-list}
- [[C 언어] 024: 너비 우선 탐색***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-024-breadth-first-search)
{.links-list}


# 024: Breadth-First Search

In this post, we will be discussing the Breadth-First Search (BFS) algorithm. We will cover the concept and theory behind the algorithm, and provide code examples in the C programming language.

## What is Breadth-First Search?

Breadth-First Search is an algorithm used for traversing or searching tree or graph data structures. It starts at the root node and explores all of the neighbor nodes at the present depth before moving on to the nodes at the next depth level.

The algorithm can be used to find the shortest path from the root node to a given node. It can also be used to find the shortest path from a given node to all other nodes in the graph.

## How Does the Algorithm Work?

The Breadth-First Search algorithm works by keeping track of all of the nodes at the current depth level in a queue. It then visits each of those nodes, adding all of their child nodes to the queue. This process is repeated until the desired node is found or the queue is empty.

## Code Example

Here is a code example of the Breadth-First Search algorithm in the C programming language.

```c
#include <stdio.h>
#include <stdlib.h>
 
typedef struct node {
    int data;
    struct node* left;
    struct node* right;
} Node;
 
Node* createNode(int data) {
    Node* node = (Node*)malloc(sizeof(Node));
    node->data = data;
    node->left = NULL;
    node->right = NULL;
    return node;
}
 
void printTree(Node* root) {
    if (root == NULL) return;
 
    printf("%d ", root->data);
    printTree(root->left);
    printTree(root->right);
}
 
void destroyTree(Node* root) {
    if (root == NULL) return;
 
    destroyTree(root->left);
    destroyTree(root->right);
    free(root);
}
 
void breadthFirstSearch(Node* root) {
    if (root == NULL) return;
 
    Node** queue = (Node**)malloc(sizeof(Node*));
    int size = 1;
    int front = 0;
    int rear = 0;
 
    queue[rear] = root;
 
    while (size > 0) {
        Node* node = queue[front];
        size--;
        front++;
 
        printf("%d ", node->data);
 
        if (node->left != NULL) {
            queue = (Node**)realloc(queue, sizeof(Node*) * (size + 1));
            queue[rear] = node->left;
            rear++;
            size++;
        }
 
        if (node->right != NULL) {
            queue = (Node**)realloc(queue, sizeof(Node*) * (size + 1));
            queue[rear] = node->right;
            rear++;
            size++;
        }
    }
 
    free(queue);
}
 
int main() {
    Node* root = createNode(1);
    root->left = createNode(2);
    root->right = createNode(3);
    root->left->left = createNode(4);
    root->left->right = createNode(5);
    root->right->left = createNode(6);
    root->right->right = createNode(7);
 
    printf("Tree: ");
    printTree(root);
    printf("\n");
 
    printf("Breadth-First Search: ");
    breadthFirstSearch(root);
    printf("\n");
 
    destroyTree(root);
 
    return 0;
}
```

## Exercise

Try implementing the Breadth-First Search algorithm in a different programming language.

## Answer Code

Here is the answer code for the exercise above.

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def printTree(root):
    if root == None:
        return

    print(root.data, end=" ")
    printTree(root.left)
    printTree(root.right)

def destroyTree(root):
    if root == None:
        return

    destroyTree(root.left)
    destroyTree(root.right)
    del root

def breadthFirstSearch(root):
    if root == None:
        return

    queue = []
    queue.append(root)

    while len(queue) > 0:
        node = queue.pop(0)

        print(node.data, end=" ")

        if node.left != None:
            queue.append(node.left)

        if node.right != None:
            queue.append(node.right)

if __name__ == "__main__":
    root = Node(1)
    root.left = Node(2)
    root.right = Node(3)
    root.left.left = Node(4)
    root.left.right = Node(5)
    root.right.left = Node(6)
    root.right.right = Node(7)

    print("Tree: ", end="")
    printTree(root)
    print()

    print("Breadth-First Search: ", end="")
    breadthFirstSearch(root)
    print()

    destroyTree(root)
```