---
title: [C언어] 025: 깊이 우선 탐색
description: 
published: true
date: 2023-02-10T13:55:50.463Z
tags: 
editor: markdown
dateCreated: 2023-02-10T13:55:44.196Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 025: Depth-First Search***English** document is available*](/en/Knowledge-base/Algorithm/c-language-025-depth-first-search)
{.links-list}


# 025: 깊이 우선 검색

## 소개

이번 포스트에서는 트리나 그래프를 순회하는 기술인 깊이 우선 탐색(DFS)에 대해 논의할 것입니다. DFS의 개념과 이론, 코드 예제 및 관련 연습을 다룰 것입니다.

## 개념과 이론

DFS는 트리 또는 그래프를 순회하는 기술입니다. 알고리즘은 루트 노드에서 시작하여 역추적하기 전에 각 분기를 따라 가능한 멀리 탐색합니다.

DFS와 너비 우선 검색(BFS)과 같은 다른 트리 순회 알고리즘 간의 주요 차이점은 노드를 방문하는 순서입니다. BFS에서 노드는 너비 우선 방식으로 방문됩니다. 즉, 다음 레벨로 이동하기 전에 동일한 레벨에 있는 모든 노드를 방문합니다. DFS에서 노드는 깊이 우선 방식으로 방문됩니다. 즉, 알고리즘은 다음 분기로 이동하기 전에 각 분기 아래에서 가능한 한 멀리 탐색합니다.

다음은 DFS의 간단한 예입니다. 다음 트리를 고려하십시오.

![트리](https://raw.githubusercontent.com/Algorithm-DataStructure-Blog/Algorithm-DataStructure-Blog.github.io/master/img/tree.png)

DFS를 사용하여 이 트리를 탐색하려면 루트 노드(A)에서 시작하여 가능한 한 왼쪽 분기를 탐색합니다. 이렇게 하면 노드 D와 E로 이동합니다. 그런 다음 노드 C로 역추적하고 오른쪽 분기를 탐색하여 노드 F로 이동합니다. 그런 다음 노드 B로 역추적하고 왼쪽 분기를 탐색하여 노드 G. 그런 다음 노드 A로 역추적하고 오른쪽 분기를 탐색하여 노드 H로 이동합니다. 탐색할 노드가 더 이상 없으므로 루트 노드로 역추적하고 중지합니다.

이 예에서 노드를 방문하는 순서는 A, B, G, C, F, D, E, H입니다.

## 코드 예제

이제 DFS의 개념과 이론을 다루었으므로 몇 가지 코드 예제를 살펴보겠습니다.

다음은 C++에서 DFS를 간단하게 구현한 것입니다. 이전 예제와 동일한 트리를 사용합니다.

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

이 예에서는 DFS의 재귀 구현을 사용하고 있습니다. 알고리즘은 루트 노드에서 시작하여 왼쪽 및 오른쪽 하위 트리를 재귀적으로 방문합니다.

다음은 C++에서 DFS의 비재귀적 구현입니다.

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

이 예에서는 DFS의 반복 구현을 사용하고 있습니다. 처리해야 하는 노드를 추적하기 위해 스택을 사용하고 있습니다. 루트 노드를 스택에 푸시한 다음 비어 있을 때까지 스택에서 노드를 팝합니다.

## 운동

이제 몇 가지 코드 예제를 보았으므로 몇 가지 연습을 해보겠습니다.

1. DFS를 사용하여 다음 트리를 순회하고 각 노드의 값을 인쇄합니다.

![tree2](https://raw.githubusercontent.com/Algorithm-DataStructure-Blog/Algorithm-DataStructure-Blog.github.io/master/img/tree2.png)

2. DFS를 사용하여 다음 그래프를 순회하고 각 노드의 값을 인쇄합니다.

![그래프](https://raw.githubusercontent.com/Algorithm-DataStructure-Blog/Algorithm-DataStructure-Blog.github.io/master/img/graph.png)

## 답변

1. 노드를 방문하는 순서는 A, B, D, E, C, F, G, H, I입니다.

2. 노드를 방문하는 순서는 A, B, D, F, E, G, C, H입니다.