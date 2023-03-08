---
title: [JavaScript] 020: AVL Tree
description: 
published: true
date: 2023-02-09T22:32:23.903Z
tags: 
editor: markdown
dateCreated: 2023-02-09T22:32:17.616Z
---

- [[JavaScript] 020: Árbol AVL***Spanish** document is available*](/es/Knowledge-base/Algorithm/javascript-020-avl-tree)
{.links-list}
- [[JavaScript] 020: AVL 树***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/javascript-020-avl-tree)
{.links-list}
- [[JavaScript] 020: AVL 트리***Korean** document is available*](/ko/Knowledge-base/Algorithm/javascript-020-avl-tree)
{.links-list}


# JavaScript 020: AVL Tree

An AVL tree is a type of self-balancing binary search tree, in which the nodes are arranged such that the heights of the two child subtrees of any node differ by at most one. This balancing of the tree allows it to be more efficient when searching for values, as the tree is more likely to be closer to a balanced state.

The height of an AVL tree is the number of edges in the longest path from the root to a leaf. The height of an empty tree is defined to be −1. An AVL tree is said to be balanced if the height of the left and right subtrees of the root differ by at most 1, and the left and right subtrees are AVL trees.

## Code example

The following is an example of how to insert a node into an AVL tree in JavaScript.

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

## Exercises

1. Implement an AVL tree in JavaScript.

2. Given a list of numbers, create an AVL tree of those numbers.

3. Find the height of an AVL tree.

4. Find the minimum value in an AVL tree.

5. Find the maximum value in an AVL tree.

6. Find the predecessor of a given value in an AVL tree.

7. Find the successor of a given value in an AVL tree.

8. Delete a value from an AVL tree.

9. Perform a pre-order traversal of an AVL tree.

10. Perform an in-order traversal of an AVL tree.

11. Perform a post-order traversal of an AVL tree.