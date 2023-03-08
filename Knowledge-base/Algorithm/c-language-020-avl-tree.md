---
title: [C언어] 020: AVL 트리
description: 
published: true
date: 2023-02-13T04:33:09.593Z
tags: 
editor: markdown
dateCreated: 2023-02-13T04:33:07.978Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 020: AVL Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-020-avl-tree)
{.links-list}


# 020: AVL 트리

AVL 트리는 모든 노드의 왼쪽 및 오른쪽 하위 트리 높이의 차이가 1보다 크지 않은 자체 균형 이진 검색 트리입니다. 이 유형의 트리는 발명가인 Georgy Adelson-Velsky와 Evgenii Landis의 이름을 따서 명명되었습니다. 그는 1962년 논문 "정보 조직을 위한 알고리즘"에서 이를 발표했습니다.

AVL 트리는 실시간 시스템과 같이 데이터가 지속적으로 삽입되거나 삭제되는 애플리케이션에서 자주 사용됩니다. 이는 AVL 트리가 각 삽입 또는 삭제 후에 자체적으로 균형을 재조정할 수 있는 반면 일반 이진 검색 트리는 그렇지 않기 때문입니다.

## 삽입

AVL 트리에 삽입하는 것은 일반 이진 검색 트리에 삽입하는 것과 유사합니다. 유일한 차이점은 삽입할 때마다 트리의 균형을 재조정해야 한다는 것입니다. 이는 다음 두 가지 방법 중 하나로 수행할 수 있습니다.

- 회전: 이것은 더 효율적이기 때문에 선호되는 방법입니다. 회전에는 왼쪽 회전과 오른쪽 회전의 두 가지 유형이 있습니다.
- 재조정: 루트에서 삽입된 노드까지 트리를 순회하고 각 노드의 균형 요소를 다시 계산한 다음 수행할 회전 유형을 결정하므로 속도가 느린 방법입니다.

다음 의사 코드는 AVL 트리에 노드를 삽입하는 방법을 보여줍니다.

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

## 삭제

AVL 트리에서 삭제하는 것은 일반 이진 검색 트리에서 삭제하는 것과 유사합니다. 유일한 차이점은 삭제할 때마다 트리의 균형을 재조정해야 한다는 것입니다. 이는 다음 두 가지 방법 중 하나로 수행할 수 있습니다.

- 회전: 이것은 더 효율적이기 때문에 선호되는 방법입니다. 회전에는 왼쪽 회전과 오른쪽 회전의 두 가지 유형이 있습니다.
- Rebalancing: 루트에서 삭제된 노드까지 트리를 순회하고 각 노드의 균형 요소를 다시 계산한 다음 수행할 회전 유형을 결정하므로 속도가 느린 방법입니다.

다음 의사 코드는 AVL 트리에서 노드를 삭제하는 방법을 보여줍니다.

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

## 코드 예제

다음 코드 예제는 C 프로그래밍 언어로 AVL 트리에서 노드를 삽입하고 삭제하는 방법을 보여줍니다.

### 삽입

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

산출:

```
Preorder traversal of the constructed AVL tree is 
30 20 10 25 40 50 
```

### 삭제

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

산출:

```
Preorder traversal of the constructed AVL tree is 
1 0 -1 2 5 6 9 10 11 
Preorder traversal after deletion of 10 
1 0 -1 2 5 6 9 11 
```

## 운동