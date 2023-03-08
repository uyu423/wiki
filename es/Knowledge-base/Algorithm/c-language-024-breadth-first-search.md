---
title: [Lenguaje C] 024: Búsqueda en amplitud
description: 
published: true
date: 2023-02-13T06:32:51.033Z
tags: 
editor: markdown
dateCreated: 2023-02-13T06:32:49.434Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 024: Breadth-First Search***English** document is available*](/en/Knowledge-base/Algorithm/c-language-024-breadth-first-search)
{.links-list}


# 024: Búsqueda en amplitud

En esta publicación, discutiremos el algoritmo Breadth-First Search (BFS). Cubriremos el concepto y la teoría detrás del algoritmo y proporcionaremos ejemplos de código en el lenguaje de programación C.

## ¿Qué es la búsqueda primero en amplitud?

Breadth-First Search es un algoritmo utilizado para recorrer o buscar estructuras de datos de árboles o gráficos. Comienza en el nodo raíz y explora todos los nodos vecinos en la profundidad actual antes de pasar a los nodos en el siguiente nivel de profundidad.

El algoritmo se puede utilizar para encontrar la ruta más corta desde el nodo raíz hasta un nodo determinado. También se puede usar para encontrar la ruta más corta desde un nodo dado a todos los demás nodos en el gráfico.

## ¿Cómo funciona el algoritmo?

El algoritmo Breadth-First Search funciona al realizar un seguimiento de todos los nodos en el nivel de profundidad actual en una cola. Luego visita cada uno de esos nodos, agregando todos sus nodos secundarios a la cola. Este proceso se repite hasta que se encuentra el nodo deseado o la cola está vacía.

## Ejemplo de código

Aquí hay un ejemplo de código del algoritmo Breadth-First Search en el lenguaje de programación C.

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

## Ejercicio

Intente implementar el algoritmo de búsqueda Breadth-First en un lenguaje de programación diferente.

## Código de respuesta

Aquí está el código de respuesta para el ejercicio anterior.

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