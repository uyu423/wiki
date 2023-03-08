---
title: [C Language] 020: AVL Tree
description: 
published: true
date: 2023-02-13T04:33:15.016Z
tags: 
editor: markdown
dateCreated: 2023-02-13T04:33:07.992Z
---

- [[Lenguaje C] 020: Árbol AVL***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-020-avl-tree)
{.links-list}
- [【C语言】020：AVL树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-020-avl-tree)
{.links-list}
- [[C언어] 020: AVL 트리***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-020-avl-tree)
{.links-list}


# 020: AVL Tree

An AVL tree is a self-balancing binary search tree in which the difference between the left and right subtree heights of any node is not greater than one. This type of tree is named after its inventors, Georgy Adelson-Velsky and Evgenii Landis, who published it in their 1962 paper "An Algorithm for the Organization of Information".

AVL trees are often used in applications where data is constantly being inserted or deleted, such as in a real-time system. This is because AVL trees can rebalance themselves after each insertion or deletion, whereas a normal binary search tree cannot.

## Insertion

Insertion into an AVL tree is similar to insertion into a normal binary search tree. The only difference is that, after each insertion, the tree must be rebalanced. This can be done by one of two methods:

- Rotation: This is the preferred method as it is more efficient. There are two types of rotation: left rotation and right rotation.
- Rebalancing: This is a slower method as it involves traversing the tree from the root to the inserted node, recalculating the balance factor of each node, and then deciding which type of rotation to perform.

The following pseudocode shows how to insert a node into an AVL tree:

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

## Deletion

Deletion from an AVL tree is similar to deletion from a normal binary search tree. The only difference is that, after each deletion, the tree must be rebalanced. This can be done by one of two methods:

- Rotation: This is the preferred method as it is more efficient. There are two types of rotation: left rotation and right rotation.
- Rebalancing: This is a slower method as it involves traversing the tree from the root to the deleted node, recalculating the balance factor of each node, and then deciding which type of rotation to perform.

The following pseudocode shows how to delete a node from an AVL tree:

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

## Code Examples

The following code examples show how to insert and delete nodes from an AVL tree in the C programming language.

### Insertion

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

Output:

```
Preorder traversal of the constructed AVL tree is 
30 20 10 25 40 50 
```

### Deletion

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

Output:

```
Preorder traversal of the constructed AVL tree is 
1 0 -1 2 5 6 9 10 11 
Preorder traversal after deletion of 10 
1 0 -1 2 5 6 9 11 
```

## Exerc