---
title: [C 언어] 024: 너비 우선 탐색
description: 
published: true
date: 2023-02-13T06:32:51.089Z
tags: 
editor: markdown
dateCreated: 2023-02-13T06:32:49.429Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 024: Breadth-First Search***English** document is available*](/en/Knowledge-base/Algorithm/c-language-024-breadth-first-search)
{.links-list}


# 024: 너비 우선 검색

이번 포스팅에서는 BFS(Breadth-First Search) 알고리즘에 대해 알아보겠습니다. 알고리즘 이면의 개념과 이론을 다루고 C 프로그래밍 언어로 된 코드 예제를 제공합니다.

## 너비 우선 검색이란 무엇입니까?

Breadth-First Search는 트리 또는 그래프 데이터 구조를 순회하거나 검색하는 데 사용되는 알고리즘입니다. 루트 노드에서 시작하여 다음 깊이 수준의 노드로 이동하기 전에 현재 깊이의 모든 이웃 노드를 탐색합니다.

이 알고리즘은 루트 노드에서 주어진 노드까지의 최단 경로를 찾는 데 사용할 수 있습니다. 또한 주어진 노드에서 그래프의 다른 모든 노드까지의 최단 경로를 찾는 데 사용할 수 있습니다.

## 알고리즘은 어떻게 작동합니까?

Breadth-First Search 알고리즘은 대기열의 현재 깊이 수준에 있는 모든 노드를 추적하여 작동합니다. 그런 다음 각 노드를 방문하여 모든 하위 노드를 대기열에 추가합니다. 이 과정은 원하는 노드를 찾거나 대기열이 비워질 때까지 반복됩니다.

## 코드 예

다음은 C 프로그래밍 언어의 Breadth-First Search 알고리즘의 코드 예제입니다.

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

## 운동

다른 프로그래밍 언어로 Breadth-First Search 알고리즘을 구현해 보십시오.

## 응답 코드

다음은 위의 연습에 대한 응답 코드입니다.

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