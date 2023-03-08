---
title: [C Language] 025: Depth-First Search
description: 
published: true
date: 2023-02-10T13:55:45.873Z
tags: 
editor: markdown
dateCreated: 2023-02-10T13:55:44.200Z
---

- [[Lenguaje C] 025: Búsqueda en profundidad primero***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-025-depth-first-search)
{.links-list}
- [【C语言】025：深度优先搜索***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-025-depth-first-search)
{.links-list}
- [[C언어] 025: 깊이 우선 탐색***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-025-depth-first-search)
{.links-list}


# 025: Depth-First Search

## Introduction

In this post, we will be discussing depth-first search (DFS), a technique for traversing trees or graphs. We will cover the concept and theory behind DFS, code examples, and related exercises.

## Concept and Theory

DFS is a technique for traversing a tree or graph. The algorithm starts at the root node and explores as far as possible along each branch before backtracking.

The main difference between DFS and other tree traversal algorithms, such as breadth-first search (BFS), is the order in which the nodes are visited. In BFS, the nodes are visited in a breadth-first manner, meaning that all of the nodes at the same level are visited before moving on to the next level. In DFS, the nodes are visited in a depth-first manner, meaning that the algorithm explores as far as possible down each branch before moving on to the next branch.

The following is a simple example of DFS. Consider the following tree:

![tree](https://raw.githubusercontent.com/Algorithm-DataStructure-Blog/Algorithm-DataStructure-Blog.github.io/master/img/tree.png)

If we were to use DFS to traverse this tree, we would start at the root node (A) and explore the left branch as far as possible. This would take us to the nodes D and E. We would then backtrack to node C and explore the right branch, which would take us to node F. We would then backtrack to node B and explore the left branch, which would take us to node G. We would then backtrack to node A and explore the right branch, which would take us to node H. We would then backtrack to the root node and stop, since there are no more nodes to explore.

The order in which the nodes are visited in this example is: A, B, G, C, F, D, E, H.

## Code Examples

Now that we've covered the concept and theory behind DFS, let's look at some code examples.

The following is a simple implementation of DFS in C++. We will be using the same tree from the previous example.

```C++
void dfs(Node* root) {
    if (root == nullptr) {
        return;
    }

    // visit the root
    cout << root->val << " ";

    // visit the left subtree
    dfs(root->left);

    // visit the right subtree
    dfs(root->right);
}
```

In this example, we are using a recursive implementation of DFS. The algorithm starts at the root node and visits the left and right subtrees recursively.

The following is a non-recursive implementation of DFS in C++.

```C++
void dfs(Node* root) {
    if (root == nullptr) {
        return;
    }

    stack<Node*> st;
    st.push(root);

    while (!st.empty()) {
        Node* curr = st.top();
        st.pop();

        // visit the node
        cout << curr->val << " ";

        // push the right child first
        // so that it will be processed last
        if (curr->right != nullptr) {
            st.push(curr->right);
        }

        // push the left child
        if (curr->left != nullptr) {
            st.push(curr->left);
        }
    }
}
```

In this example, we are using an iterative implementation of DFS. We are using a stack to keep track of the nodes that need to be processed. We push the root node onto the stack and then pop nodes off of the stack until it is empty.

## Exercises

Now that we've seen some code examples, let's try some exercises.

1. Traverse the following tree using DFS and print the value of each node:

![tree2](https://raw.githubusercontent.com/Algorithm-DataStructure-Blog/Algorithm-DataStructure-Blog.github.io/master/img/tree2.png)

2. Traverse the following graph using DFS and print the value of each node:

![graph](https://raw.githubusercontent.com/Algorithm-DataStructure-Blog/Algorithm-DataStructure-Blog.github.io/master/img/graph.png)

## Answers

1. The order in which the nodes are visited is: A, B, D, E, C, F, G, H, I.

2. The order in which the nodes are visited is: A, B, D, F, E, G, C, H.