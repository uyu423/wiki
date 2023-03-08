---
title: 【C语言】020：AVL树
description: 
published: true
date: 2023-02-13T04:33:09.636Z
tags: 
editor: markdown
dateCreated: 2023-02-13T04:33:07.977Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 020: AVL Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-020-avl-tree)
{.links-list}


# 020：AVL树

AVL树是一种自平衡二叉搜索树，其中任意节点的左右子树高度之差不大于1。这种树以其发明者 Georgy Adelson-Velsky 和 Evgenii Landis 的名字命名，他们将其发表在 1962 年的论文“信息组织算法”中。

AVL 树通常用于不断插入或删除数据的应用程序，例如实时系统。这是因为 AVL 树可以在每次插入或删除后重新平衡自己，而普通的二叉搜索树则不能。

## 插入

插入 AVL 树类似于插入普通的二叉搜索树。唯一的区别是，每次插入后，树都必须重新平衡。这可以通过以下两种方法之一来完成：

- 旋转：这是首选方法，因为它更有效。旋转有两种类型：左旋转和右旋转。
- 重新平衡：这是一种较慢的方法，因为它涉及从根到插入节点遍历树，重新计算每个节点的平衡因子，然后决定执行哪种类型的旋转。

以下伪代码显示了如何将节点插入 AVL 树：

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

## 删除

从 AVL 树中删除类似于从普通二叉搜索树中删除。唯一的区别是，每次删除后，树都必须重新平衡。这可以通过以下两种方法之一来完成：

- 旋转：这是首选方法，因为它更有效。旋转有两种类型：左旋转和右旋转。
- 重新平衡：这是一种较慢的方法，因为它涉及从根遍历树到删除的节点，重新计算每个节点的平衡因子，然后决定执行哪种类型的旋转。

以下伪代码显示了如何从 AVL 树中删除节点：

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

## 代码示例

以下代码示例显示了如何使用 C 编程语言从 AVL 树中插入和删除节点。

### 插入

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

输出：

```
Preorder traversal of the constructed AVL tree is 
30 20 10 25 40 50 
```

### 删除

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

输出：

```
Preorder traversal of the constructed AVL tree is 
1 0 -1 2 5 6 9 10 11 
Preorder traversal after deletion of 10 
1 0 -1 2 5 6 9 11 
```

## 练习