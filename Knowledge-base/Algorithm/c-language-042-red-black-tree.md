---
title: [C언어] 042: 레드-블랙 트리
description: 
published: true
date: 2023-02-12T10:18:19.381Z
tags: 
editor: markdown
dateCreated: 2023-02-12T10:18:17.672Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 042: Red-Black Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-042-red-black-tree)
{.links-list}


# 042: 레드-블랙 트리

Red-Black 트리는 모든 노드가 "빨간색" 또는 "검은색" 값을 갖는 색상 특성을 갖는 자체 균형 이진 검색 트리입니다. 다음은 Red-Black 트리의 시각적 표현입니다.

![레드 블랙 트리](https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Red-black_tree_example.svg/250px-Red-black_tree_example.svg.png)

Red-Black 트리의 각 노드에는 다음 속성이 있습니다.

- **키**: 키는 노드를 식별하는 데 사용되는 값입니다. 위의 예에서 키는 1에서 7까지의 숫자입니다.
- **색상**: 노드는 "빨간색" 또는 "검은색"일 수 있습니다. 루트 노드는 항상 검은색입니다.
- **왼쪽 자식**: 왼쪽 자식 노드에 대한 참조입니다.
- **오른쪽 자식**: 오른쪽 자식 노드에 대한 참조입니다.
- **Parent**: 부모 노드에 대한 참조입니다.

Red-Black 트리에는 다음과 같은 속성이 있습니다.

- **속성 1(빨간색 노드):** 노드는 노드의 자식이 둘 다 검은색인 경우에만 빨간색입니다.
- **속성 2(검은색 노드):** 모든 노드는 빨간색이거나 검은색입니다.
- **속성 3(루트 노드):** 루트 노드는 검은색입니다.
- **속성 4(리프 노드):** 모든 리프 노드(자식이 없는 노드)는 검은색입니다.
- **Property 5(Red-Black 속성):** 노드가 빨간색이면 두 자식 모두 검은색입니다.
- **속성 6(경로):** 노드에서 하위 리프까지의 모든 단순 경로에는 동일한 수의 블랙 노드가 포함됩니다.

다음은 속성 5(Red-Black 속성)를 만족하지 않는 Red-Black 트리의 예입니다.

![잘못된 레드 블랙 트리](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5f/Invalid_red_black_tree.svg/200px-Invalid_red_black_tree.svg.png)

보시다시피 키가 4인 노드는 빨간색이지만 왼쪽 자식도 빨간색입니다. 이는 속성 5를 위반합니다.

Red-Black 트리가 무엇인지 살펴보았으니 이제 어떻게 사용되는지 살펴보겠습니다.

## 애플리케이션

Red-Black 트리는 다음과 같은 다양한 애플리케이션에서 사용됩니다.

- **데이터베이스 인덱스**: Red-Black 트리는 데이터베이스에서 인덱스로 자주 사용됩니다. 빠르게 검색하고 삽입하고 삭제할 수 있기 때문입니다.
- **운영 체제**: Red-Black 트리는 프로세스 정보를 저장하기 위해 Linux 커널에서 사용됩니다.
- **워드 프로세서**: 레드-블랙 트리는 워드 프로세서에서 문서의 단어 위치에 대한 정보를 저장하는 데 사용됩니다.

## 구현

이제 우리는 Red-Black 트리가 무엇인지와 이들이 사용되는 일부 응용 프로그램을 살펴보았으므로 어떻게 구현되는지 살펴보겠습니다.

### 노드

먼저 Node 클래스를 만들어야 합니다. 이 클래스는 노드의 키, 색상, 왼쪽 자식, 오른쪽 자식 및 부모를 저장합니다.

```java
public class Node {
    int key;
    boolean color;
    Node leftChild;
    Node rightChild;
    Node parent;

    public Node(int key, boolean color, Node leftChild, Node rightChild, Node parent) {
        this.key = key;
        this.color = color;
        this.leftChild = leftChild;
        this.rightChild = rightChild;
        this.parent = parent;
    }
}
```

### 나무

다음으로 Tree 클래스를 만들어야 합니다. 이 클래스는 트리의 루트 노드를 저장합니다.

```java
public class Tree {
    Node root;

    public Tree() {
        this.root = null;
    }
}
```

### 삽입

이제 노드 클래스와 트리 클래스가 있으므로 Red-Black 트리 구현을 시작할 수 있습니다. 우리가 구현할 첫 번째 작업은 삽입 작업입니다.

레드-블랙 트리에 노드를 삽입하려면 먼저 노드를 삽입할 올바른 위치를 찾아야 합니다. 이진 검색 트리 삽입 알고리즘을 사용하여 이를 수행합니다. 노드를 삽입할 올바른 위치를 찾았으면 노드의 색상을 빨간색으로 설정해야 합니다. 그런 다음 트리가 여전히 유효한지 확인해야 합니다. 트리가 유효하지 않으면 수정해야 합니다.

다음은 삽입 알고리즘입니다.

```java
public void insert(int key) {
    // Create a new node with the given key and color it red
    Node newNode = new Node(key, true, null, null, null);

    // Find the correct place to insert the new node
    Node currentNode = root;
    Node parentNode = null;
    while (currentNode != null) {
        parentNode = currentNode;
        if (key < currentNode.key) {
            currentNode = currentNode.leftChild;
        } else {
            currentNode = currentNode.rightChild;
        }
    }

    // Set the new node's parent
    newNode.parent = parentNode;

    // Insert the new node into the tree
    if (parentNode == null) {
        // The new node is the root node
        root = newNode;
    } else if (key < parentNode.key) {
        // The new node is the left child of the parent node
        parentNode.leftChild = newNode;
    } else {
        // The new node is the right child of the parent node
        parentNode.rightChild = newNode;
    }

    // Fix the tree
    fixTree(newNode);
}
```

### 수정 트리

Red-Black 트리에 노드를 삽입하는 방법을 살펴보았으니 이제 트리를 수정하는 방법을 살펴보겠습니다.

Red-Black 트리를 수정할 때 고려해야 할 네 가지 경우가 있습니다.

- 사례 1(노드가 루트 노드임): 노드가 루트 노드인 경우 색상을 검정색으로 설정하기만 하면 됩니다.
- 사례 2(노드가 검은색 부모를 가진 빨간색 노드임): 노드가 검은색 부모를 가진 빨간색 노드인 경우 아무 작업도 수행하지 않습니다.
- 사례 3(노드는 빨간색 부모를 가진 빨간색 노드임): 노드가 빨간색 부모를 가진 빨간색 노드인 경우 노드의 삼촌과 조부모의 색상을 고려해야 합니다. 삼촌도 빨간색이면 노드, 부모, 삼촌의 색상을 검은색으로 설정하고 조부모의 색상을 빨간색으로 설정하기만 하면 됩니다. 그런 다음 상위 노드에서 fixTree() 메서드를 재귀적으로 호출해야 합니다.

아저씨가 검은색이면 부모와 노드의 방향을 고려해야 합니다. 부모와 노드가 모두 왼쪽 자식이거나 둘 다 오른쪽 자식인 경우 부모의 색상을 검은색으로 설정하고 조부모의 색상을 빨간색으로 설정하기만 하면 됩니다. 그런 다음 상위 노드에서 fixTree() 메서드를 재귀적으로 호출해야 합니다.

부모와 노드가 모두 왼쪽 자식이 아니거나 둘 다 오른쪽 자식이 아니면 왼쪽 회전 또는 오른쪽 회전을 수행해야 합니다. 회전 후 노드의 색상을 검은색으로 설정하고 조부모의 색상을 빨간색으로 설정해야 합니다. 그런 다음 상위 노드에서 fixTree() 메서드를 재귀적으로 호출해야 합니다.

- 사례 4(노드는 빨간색 부모를 가진 검은색 노드임): 노드가 빨간색 부모를 가진 검은색 노드인 경우 노드의 삼촌과 조부모의 색상을 고려해야 합니다. 삼촌도 빨간색이면 부모와 삼촌의 색을 검은색으로 설정하고 조부모의 색을 빨간색으로 설정하기만 하면 됩니다. 그런 다음 상위 노드에서 fixTree() 메서드를 재귀적으로 호출해야 합니다.

아저씨가 검은색이면 부모와 노드의 방향을 고려해야 합니다. 부모와 노드가 모두 왼쪽 자식이거나 둘 다 오른쪽 자식인 경우 부모의 색상을 검은색으로 설정해야 합니다. 그런 다음 부모 노드에서 fixTree() 메서드를 재귀적으로 호출해야 합니다.

부모와 노드가 모두 왼쪽 자식이 아니거나 둘 다 오른쪽 자식이 아니면 왼쪽 회전 또는 오른쪽 회전을 수행해야 합니다. 회전 후 조부모의 색상을 빨간색으로 설정해야 합니다. 그런 다음 상위 노드에서 fixTree() 메서드를 재귀적으로 호출해야 합니다.

다음은 fixTree() 알고리즘입니다.

```java
public void fixTree(Node node) {
    // Case 1 (Node is the root node)
    if (node.parent == null) {
        node.color = false;
        return;
    }

    // Case 2 (Node is a red node with a black parent)
    if (node.color && !node.parent.color) {
        return;
    }

    // Case 3 (Node is a red node with a red parent)
    if (node.color && node.parent.color) {
        Node uncle = getUncle(node);

        if (uncle != null && uncle.color) {
            // Set the colors of the node, parent, and uncle to black and the color of the grandparent to red
            node.parent.color = false;
            uncle.color = false;
            getGrandparent(node).color = true;

            // Recursively call the fixTree() method on the grandparent node
            fixTree(getGrandparent(node));
        } else {
            // Perform a left rotation or right rotation
            if (node == node.parent.rightChild && node.parent == getGrandparent(node).leftChild) {
                // Perform a left rotation
                leftRotate(node.parent);

                // Set the colors of the node and parent to black and the color of the grandparent to red
                node.color = false;
                node.leftChild.color = true;
            } else if (node == node.parent.leftChild && node.parent == getGrandparent(node).rightChild) {
                // Perform a right rotation
                rightRotate(node.parent);

                // Set the colors of the node and parent to black and the color of the grandparent to red
                node.color = false;
                node.rightChild.color = true;
            }

            // Case 4 (Node is a black node with a red parent)
            if (node == node.parent.leftChild) {
                // Perform a right rotation
                rightRotate(getGrandparent(node));
            } else {
                // Perform a left rotation
                leftRotate(getGrandparent(node));
            }

            // Set the color of the grandparent to red
            getGrandparent(node).color = true;

            // Set the color of the parent to black
            node.parent.color = false;
        }
    }
}
```

### 왼쪽 회전

이제 Red-Black 트리를 수정하는 방법을 살펴보았으므로 왼쪽 회전을 수행하는 방법을 살펴보겠습니다.

노드의 오른쪽 자식이 왼쪽 자식보다 무거울 때 트리의 균형을 맞추기 위해 왼쪽 회전이 사용됩니다. 다음은 왼쪽 회전의 예입니다.

![왼쪽 회전](https://upload.wikimedia.org/wikipedia/commons/2/2d/Left-rotation.svg)

보시다시피 회전되는 노드는 키가 3인 노드입니다. 이 노드의 왼쪽 자식은 키가 2인 노드이고 오른쪽 자식은 키가 4인 노드입니다. 회전 후 키가 3인 노드는 는 키가 4인 노드의 왼쪽 자식이고 키가 2인 노드는 키가 3인 노드의 오른쪽 자식입니다.

다음은 leftRotate() 알고리즘입니다.

```java
public void leftRotate(Node node) {
    // Check if the node has a right child
    if (node.rightChild == null) {
        return;
    }

    // Set the right child of the node to be the new root of the subtree
    Node newRoot = node.rightChild;

    // Set the left child of the new root to be the node's right child
    newRoot.leftChild = node;

    // Set the node's right child to be the new root's left child
    node.rightChild = newRoot.leftChild;

    // Set the new root's parent to be the node's parent
    newRoot.parent = node.parent;

    // Check if the node is the root node
    if (node.parent == null) {
        // Set the new root to be the root node
        root = newRoot;
    } else if (node == node.parent.leftChild) {
        // Set the new root to be the node's left child
        node.parent.leftChild = newRoot;
    } else {
        // Set the new root to be the node's right child
        node.parent.rightChild = newRoot;
    }

    // Set the node's parent to be the new root
    node.parent = newRoot;
}
```

### 오른쪽 회전

왼쪽 회전을 수행하는 방법을 살펴보았으니 이제 오른쪽 회전을 수행하는 방법을 살펴보겠습니다.

오른쪽 회전은 노드의 왼쪽 자식이 오른쪽 자식보다 무거울 때 트리의 균형을 맞추기 위해 사용됩니다. 다음은 오른쪽 회전의 예입니다.

![오른쪽 회전](https://upload.wikimedia.org/wikipedia/commons/d/d4/Right-rotation.svg)

보시다시피 회전되는 노드는 키가 3인 노드입니다. 이 노드의 왼쪽 자식은 키가 2인 노드이고 오른쪽 자식은 키가 4인 노드입니다. 회전 후 키가 3인 노드는 는 키가 2인 노드의 오른쪽 자식이고 키가 4인 노드는 키가 3인 노드의 왼쪽 자식입니다.

다음은 rightRotate() 알고리즘입니다.

```java
public void rightRotate(Node node) {
    // Check if the node has a left child
    if (node.leftChild == null) {
        return;
    }

    // Set the left child of the node to be the new root of the subtree
    Node newRoot = node.leftChild;

    // Set the right child of the new root to be the node's left child
    newRoot.rightChild = node;

    // Set the node's left child to be the new root's right child
    node.leftChild = newRoot.rightChild;

    // Set the new root's parent to be the node's parent
    newRoot.parent = node.parent;

    // Check if the node is the root node
    if (node.parent == null) {
        // Set the new root to be the root node
        root = newRoot;
    } else if (node == node.parent.rightChild) {
        // Set the new root to be the node's right child
        node.parent.rightChild = newRoot;
    } else {
        // Set the new root to be the node's left child
        node.parent.leftChild = newRoot;
    }

    // Set the node's parent to be the new root
    node.parent = newRoot;
}
```

### 삭제

오른쪽 회전을 수행하는 방법을 살펴보았으므로 이제 Red-Black 트리에서 노드를 삭제하는 방법을 살펴보겠습니다.

Red-Black Tree에서 노드를 삭제하려면 먼저 삭제할 노드를 찾아야 합니다. 이진 검색 트리 삭제 알고리즘을 사용하여 이를 수행합니다. 삭제할 노드를 찾으면 트리가 여전히 유효한지 확인해야 합니다. 트리가 유효하지 않으면 수정해야 합니다.

다음은 삭제 알고리즘입니다.

```java
public void delete(int key) {
    // Find the node to delete
    Node node = find(key);

    // Check if the node was found
    if (node == null) {
        return;
    }

    // Delete the node
    deleteNode(node);
}
```

### 노드 삭제

Red-Black Tree에서 노드를 삭제하는 방법을 살펴보았으니 이제 노드를 삭제하는 방법을 살펴보겠습니다.

Red-Black에서 노드를 삭제할 때 고려해야 할 세 가지 경우가 있습니다.