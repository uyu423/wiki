---
title: [Lenguaje C] 020: Árbol AVL
description: 
published: true
date: 2023-02-13T04:33:09.584Z
tags: 
editor: markdown
dateCreated: 2023-02-13T04:33:07.991Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 020: AVL Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-020-avl-tree)
{.links-list}


# 020: Árbol AVL

Un árbol AVL es un árbol de búsqueda binario autoequilibrado en el que la diferencia entre las alturas de los subárboles izquierdo y derecho de cualquier nodo no es mayor que uno. Este tipo de árbol lleva el nombre de sus inventores, Georgy Adelson-Velsky y Evgenii Landis, quienes lo publicaron en su artículo de 1962 "Un algoritmo para la organización de la información".

Los árboles AVL a menudo se usan en aplicaciones donde los datos se insertan o eliminan constantemente, como en un sistema en tiempo real. Esto se debe a que los árboles AVL pueden reequilibrarse después de cada inserción o eliminación, mientras que un árbol de búsqueda binaria normal no puede hacerlo.

## Inserción

La inserción en un árbol AVL es similar a la inserción en un árbol de búsqueda binaria normal. La única diferencia es que, después de cada inserción, el árbol debe reequilibrarse. Esto se puede hacer por uno de dos métodos:

- Rotación: Este es el método preferido ya que es más eficiente. Hay dos tipos de rotación: rotación a la izquierda y rotación a la derecha.
- Reequilibrio: este es un método más lento, ya que implica atravesar el árbol desde la raíz hasta el nodo insertado, volver a calcular el factor de equilibrio de cada nodo y luego decidir qué tipo de rotación realizar.

El siguiente pseudocódigo muestra cómo insertar un nodo en un árbol AVL:

```
function insert(node, key)
    if node is null
        return new Node(key)
    if key < node.key
        node.left = insert(node.left, key)
    else if key > node.key
        node.right = insert(node.right, key)
    else
        return node
    node.height = 1 + max(height(node.left), height(node.right))
    balance = getBalance(node)
    if balance > 1 and key < node.left.key
        return rightRotate(node)
    if balance < -1 and key > node.right.key
        return leftRotate(node)
    if balance > 1 and key > node.left.key
        node.left = leftRotate(node.left)
        return rightRotate(node)
    if balance < -1 and key < node.right.key
        node.right = rightRotate(node.right)
        return leftRotate(node)
    return node
```

## Eliminación

La eliminación de un árbol AVL es similar a la eliminación de un árbol de búsqueda binaria normal. La única diferencia es que, después de cada eliminación, el árbol debe reequilibrarse. Esto se puede hacer por uno de dos métodos:

- Rotación: Este es el método preferido ya que es más eficiente. Hay dos tipos de rotación: rotación a la izquierda y rotación a la derecha.
- Reequilibrio: este es un método más lento, ya que implica atravesar el árbol desde la raíz hasta el nodo eliminado, volver a calcular el factor de equilibrio de cada nodo y luego decidir qué tipo de rotación realizar.

El siguiente pseudocódigo muestra cómo eliminar un nodo de un árbol AVL:

```
function delete(node, key)
    if node is null
        return node
    if key < node.key
        node.left = delete(node.left, key)
    else if key > node.key
        node.right = delete(node.right, key)
    else
        if node.left is null or node.right is null
            if node.left is null
                temp = node.right
                node = null
                return temp
            else if node.right is null
                temp = node.left
                node = null
                return temp
        temp = minValueNode(node.right)
        node.key = temp.key
        node.right = delete(node.right, temp.key)
    if node is null
        return node
    node.height = 1 + max(height(node.left), height(node.right))
    balance = getBalance(node)
    if balance > 1 and getBalance(node.left) >= 0
        return rightRotate(node)
    if balance > 1 and getBalance(node.left) < 0
        node.left = leftRotate(node.left)
        return rightRotate(node)
    if balance < -1 and getBalance(node.right) <= 0
        return leftRotate(node)
    if balance < -1 and getBalance(node.right) > 0
        node.right = rightRotate(node.right)
        return leftRotate(node)
    return node
```

## Ejemplos de código

Los siguientes ejemplos de código muestran cómo insertar y eliminar nodos de un árbol AVL en el lenguaje de programación C.

### Inserción

```c
#include <stdio.h>
#include <stdlib.h>
 
struct Node
{
    int key;
    struct Node *left;
    struct Node *right;
    int height;
};
 
int max(int a, int b);
 
int height(struct Node *N)
{
    if (N == NULL)
        return 0;
    return N->height;
}
 
int max(int a, int b)
{
    return (a > b)? a : b;
}
 
struct Node* newNode(int key)
{
    struct Node* node = (struct Node*)
                        malloc(sizeof(struct Node));
    node->key   = key;
    node->left   = NULL;
    node->right  = NULL;
    node->height = 1; 
    return(node);
}
 
struct Node *rightRotate(struct Node *y)
{
    struct Node *x = y->left;
    struct Node *T2 = x->right;
 
    x->right = y;
    y->left = T2;
 
    y->height = max(height(y->left), height(y->right))+1;
    x->height = max(height(x->left), height(x->right))+1;
 
    return x;
}
 
struct Node *leftRotate(struct Node *x)
{
    struct Node *y = x->right;
    struct Node *T2 = y->left;
 
    y->left = x;
    x->right = T2;
 
    x->height = max(height(x->left), height(x->right))+1;
    y->height = max(height(y->left), height(y->right))+1;
 
    return y;
}
 
int getBalance(struct Node *N)
{
    if (N == NULL)
        return 0;
    return height(N->left) - height(N->right);
}
 
struct Node* insert(struct Node* node, int key)
{
    if (node == NULL)
        return(newNode(key));
 
    if (key < node->key)
        node->left  = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);
    else 
        return node;
 
    node->height = 1 + max(height(node->left),
                           height(node->right));
 
    int balance = getBalance(node);
 
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);
 
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);
 
    if (balance > 1 && key > node->left->key)
    {
        node->left =  leftRotate(node->left);
        return rightRotate(node);
    }
 
    if (balance < -1 && key < node->right->key)
    {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }
 
    return node;
}
 
void preOrder(struct Node *root)
{
    if(root != NULL)
    {
        printf("%d ", root->key);
        preOrder(root->left);
        preOrder(root->right);
    }
}
 
int main()
{
  struct Node *root = NULL;
 
  root = insert(root, 10);
  root = insert(root, 20);
  root = insert(root, 30);
  root = insert(root, 40);
  root = insert(root, 50);
  root = insert(root, 25);
 
  printf("Preorder traversal of the constructed AVL"
         " tree is \n");
  preOrder(root);
 
  return 0;
}
```

Producción:

```
Preorder traversal of the constructed AVL tree is 
30 20 10 25 40 50 
```

### Eliminación

```c
#include <stdio.h>
#include <stdlib.h>
 
struct Node
{
    int key;
    struct Node *left;
    struct Node *right;
    int height;
};
 
int max(int a, int b);
 
int height(struct Node *N)
{
    if (N == NULL)
        return 0;
    return N->height;
}
 
int max(int a, int b)
{
    return (a > b)? a : b;
}
 
struct Node* newNode(int key)
{
    struct Node* node = (struct Node*)
                        malloc(sizeof(struct Node));
    node->key   = key;
    node->left   = NULL;
    node->right  = NULL;
    node->height = 1;
    return(node);
}
 
struct Node *rightRotate(struct Node *y)
{
    struct Node *x = y->left;
    struct Node *T2 = x->right;
 
    x->right = y;
    y->left = T2;
 
    y->height = max(height(y->left), height(y->right))+1;
    x->height = max(height(x->left), height(x->right))+1;
 
    return x;
}
 
struct Node *leftRotate(struct Node *x)
{
    struct Node *y = x->right;
    struct Node *T2 = y->left;
 
    y->left = x;
    x->right = T2;
 
    x->height = max(height(x->left), height(x->right))+1;
    y->height = max(height(y->left), height(y->right))+1;
 
    return y;
}
 
int getBalance(struct Node *N)
{
    if (N == NULL)
        return 0;
    return height(N->left) - height(N->right);
}
 
struct Node* insert(struct Node* node, int key)
{
    if (node == NULL)
        return(newNode(key));
 
    if (key < node->key)
        node->left  = insert(node->left, key);
    else if (key > node->key)
        node->right = insert(node->right, key);
    else 
        return node;
 
    node->height = 1 + max(height(node->left),
                           height(node->right));
 
    int balance = getBalance(node);
 
    if (balance > 1 && key < node->left->key)
        return rightRotate(node);
 
    if (balance < -1 && key > node->right->key)
        return leftRotate(node);
 
    if (balance > 1 && key > node->left->key)
    {
        node->left =  leftRotate(node->left);
        return rightRotate(node);
    }
 
    if (balance < -1 && key < node->right->key)
    {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }
 
    return node;
}
 
struct Node* minValueNode(struct Node* node)
{
    struct Node* current = node;
 
    while (current->left != NULL)
        current = current->left;
 
    return current;
}
 
struct Node* deleteNode(struct Node* root, int key)
{
    if (root == NULL)
        return root;
 
    if ( key < root->key )
        root->left = deleteNode(root->left, key);
 
    else if( key > root->key )
        root->right = deleteNode(root->right, key);
 
    else
    {
        if( (root->left == NULL) || 
            (root->right == NULL) )
        {
            struct Node *temp;
            if (root->left != NULL)
                temp = root->left;
            else
                temp = root->right;
 
            if (temp == NULL)
            {
                temp = root;
                root = NULL;
            }
            else
             *root = *temp;
            free(temp);
        }
        else
        {
            struct Node* temp = minValueNode(root->right);
 
            root->key = temp->key;
 
            root->right = deleteNode(root->right,
                                     temp->key);
        }
    }
 
    if (root == NULL)
      return root;
 
    root->height = 1 + max(height(root->left),
                           height(root->right));
 
    int balance = getBalance(root);
 
    if (balance > 1 && getBalance(root->left) >= 0)
        return rightRotate(root);
 
    if (balance > 1 && getBalance(root->left) < 0)
    {
        root->left =  leftRotate(root->left);
        return rightRotate(root);
    }
 
    if (balance < -1 && getBalance(root->right) <= 0)
        return leftRotate(root);
 
    if (balance < -1 && getBalance(root->right) > 0)
    {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }
 
    return root;
}
 
void preOrder(struct Node *root)
{
    if(root != NULL)
    {
        printf("%d ", root->key);
        preOrder(root->left);
        preOrder(root->right);
    }
}
 
int main()
{
  struct Node *root = NULL;
 
  root = insert(root, 9);
  root = insert(root, 5);
  root = insert(root, 10);
  root = insert(root, 0);
  root = insert(root, 6);
  root = insert(root, 11);
  root = insert(root, -1);
  root = insert(root, 1);
  root = insert(root, 2);
 
  printf("Preorder traversal of the constructed AVL"
         " tree is \n");
  preOrder(root);
 
  root = deleteNode(root, 10);
 
  printf("\nPreorder traversal after deletion of 10 \n");
  preOrder(root);
 
  return 0;
}
```

Producción:

```
Preorder traversal of the constructed AVL tree is 
1 0 -1 2 5 6 9 10 11 
Preorder traversal after deletion of 10 
1 0 -1 2 5 6 9 11 
```

## Ejercicio