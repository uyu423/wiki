---
title: [C语言]024：广度优先搜索
description: 
published: true
date: 2023-02-13T06:32:51.025Z
tags: 
editor: markdown
dateCreated: 2023-02-13T06:32:49.428Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 024: Breadth-First Search***English** document is available*](/en/Knowledge-base/Algorithm/c-language-024-breadth-first-search)
{.links-list}


# 024：广度优先搜索

在这篇文章中，我们将讨论广度优先搜索 (BFS) 算法。我们将涵盖算法背后的概念和理论，并提供 C 编程语言的代码示例。

## 什么是广度优先搜索？

广度优先搜索是一种用于遍历或搜索树或图形数据结构的算法。它从根节点开始，探索当前深度的所有邻居节点，然后再移动到下一个深度级别的节点。

该算法可用于查找从根节点到给定节点的最短路径。它还可用于查找从给定节点到图中所有其他节点的最短路径。

## 该算法如何工作？

广度优先搜索算法通过跟踪队列中当前深度级别的所有节点来工作。然后它访问每个节点，将它们的所有子节点添加到队列中。重复此过程，直到找到所需的节点或队列为空。

## 代码示例

下面是一个 C 语言的广度优先搜索算法的代码示例。

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

## 锻炼

尝试用不同的编程语言实现广度优先搜索算法。

## 答案代码

这是上述练习的答案代码。

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