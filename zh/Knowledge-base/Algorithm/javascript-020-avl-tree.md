---
title: [JavaScript] 020: AVL 树
description: 
published: true
date: 2023-02-09T22:32:19.217Z
tags: 
editor: markdown
dateCreated: 2023-02-09T22:32:17.588Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[JavaScript] 020: AVL Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-020-avl-tree)
{.links-list}


# JavaScript 020：AVL 树

AVL树是一种自平衡二叉搜索树，其中节点的排列使得任何节点的两个子树的高度最多相差一个。树的这种平衡使其在搜索值时更有效，因为树更有可能接近平衡状态。

AVL 树的高度是从根到叶的最长路径中的边数。空树的高度定义为-1。如果根的左右子树的高度最多相差 1，并且左右子树都是 AVL 树，则称这棵 AVL 树是平衡的。

## 代码示例

以下是如何在 JavaScript 中将节点插入 AVL 树的示例。

```javascript
function insert(root, key) { 
    // Step 1 - Perform normal BST insertion 
    if (root == null) 
        return new Node(key); 
  
    if (key < root.key) 
        root.left = insert(root.left, key); 
    else if (key > root.key) 
        root.right = insert(root.right, key); 
    else // Equal keys are not allowed in BST 
        return root; 
  
    // Step 2 - Update the height of the  
             // ancestor node 
    root.height = 1 + Math.max(height(root.left), 
                              height(root.right)); 
  
    // Step 3 - Get the balance factor 
    let balance = getBalance(root); 
  
    // Step 4 - If the node is unbalanced,  
    // then there are 4 cases 
  
    // Left Left Case 
    if (balance > 1 && key < root.left.key) 
        return rightRotate(root); 
  
    // Right Right Case 
    if (balance < -1 && key > root.right.key) 
        return leftRotate(root); 
  
    // Left Right Case 
    if (balance > 1 && key > root.left.key) { 
        root.left = leftRotate(root.left); 
        return rightRotate(root); 
    } 
  
    // Right Left Case 
    if (balance < -1 && key < root.right.key) { 
        root.right = rightRotate(root.right); 
        return leftRotate(root); 
    } 
  
    /* return the (unchanged) node pointer */
    return root; 
} 
```

## 练习

1.用JavaScript实现一个AVL树。

2. 给定一个数字列表，创建这些数字的 AVL 树。

3. 求一棵 AVL 树的高度。

4. 找到 AVL 树中的最小值。

5. 找到 AVL 树中的最大值。

6. 在 AVL 树中查找给定值的前驱。

7. 在 AVL 树中查找给定值的后继。

8. 从 AVL 树中删除一个值。

9. 执行 AVL 树的预序遍历。

10. 执行 AVL 树的中序遍历。

11. 执行 AVL 树的后序遍历。