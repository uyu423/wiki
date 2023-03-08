---
title: 【C语言】025：深度优先搜索
description: 
published: true
date: 2023-02-10T13:55:50.463Z
tags: 
editor: markdown
dateCreated: 2023-02-10T13:55:44.197Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 025: Depth-First Search***English** document is available*](/en/Knowledge-base/Algorithm/c-language-025-depth-first-search)
{.links-list}


# 025：深度优先搜索

## 介绍

在本文中，我们将讨论深度优先搜索 (DFS)，这是一种遍历树或图的技术。我们将介绍 DFS、代码示例和相关练习背后的概念和理论。

## 概念与理论

DFS 是一种遍历树或图的技术。该算法从根节点开始，在回溯之前尽可能沿着每个分支探索。

DFS 与其他树遍历算法（例如广度优先搜索 (BFS)）的主要区别在于访问节点的顺序。在 BFS 中，以广度优先的方式访问节点，这意味着在进入下一个级别之前访问同一级别的所有节点。在 DFS 中，以深度优先的方式访问节点，这意味着该算法在移动到下一个分支之前尽可能探索每个分支。

下面是一个 DFS 的简单例子。考虑以下树：

![树](https://raw.githubusercontent.com/Algorithm-DataStructure-Blog/Algorithm-DataStructure-Blog.github.io/master/img/tree.png)

如果我们要使用 DFS 遍历这棵树，我们将从根节点 (A) 开始，尽可能探索左侧分支。这会将我们带到节点 D 和 E。然后我们将回溯到节点 C 并探索右分支，这将带我们到达节点 F。然后我们将回溯到节点 B 并探索左分支，这将带我们到节点 G。然后我们将回溯到节点 A 并探索正确的分支，这将带我们到节点 H。然后我们将回溯到根节点并停止，因为没有更多节点可供探索。

本例中访问节点的顺序为：A、B、G、C、F、D、E、H。

## 代码示例

现在我们已经介绍了 DFS 背后的概念和理论，让我们看一些代码示例。

下面是DFS在C++中的简单实现。我们将使用与上一个示例相同的树。

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

在此示例中，我们使用 DFS 的递归实现。该算法从根节点开始，递归访问左右子树。

下面是C++中DFS的非递归实现。

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

在此示例中，我们使用 DFS 的迭代实现。我们正在使用堆栈来跟踪需要处理的节点。我们将根节点压入堆栈，然后将节点从堆栈中弹出，直到它为空。

## 练习

现在我们已经看过一些代码示例，让我们尝试一些练习。

1.使用DFS遍历下面的树，打印每个节点的值：

![tree2](https://raw.githubusercontent.com/Algorithm-DataStructure-Blog/Algorithm-DataStructure-Blog.github.io/master/img/tree2.png)

2.使用DFS遍历下图，打印每个节点的值：

![图](https://raw.githubusercontent.com/Algorithm-DataStructure-Blog/Algorithm-DataStructure-Blog.github.io/master/img/graph.png)

## 答案

1.节点被访问的顺序是：A、B、D、E、C、F、G、H、I。

2、访问节点的顺序是：A、B、D、F、E、G、C、H。