---
title: [JavaScript] 043: 스플레이 트리
description: 
published: true
date: 2023-02-10T21:33:27.972Z
tags: 
editor: markdown
dateCreated: 2023-02-10T21:33:25.923Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 043: Splay Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-043-splay-tree)
{.links-list}


# 스플레이 트리

스플레이 트리는 최근에 액세스한 요소가 다시 빠르게 액세스할 수 있는 속성을 가진 자체 균형 이진 검색 트리입니다. O(log(n)) 시간에 삽입, 조회 및 제거와 같은 기본 작업을 수행합니다.

스플레이 트리는 다음 불변성을 만족하는 이진 트리입니다.

```
After each operation, the node that was accessed is moved to the root of the tree.
```

즉, 가장 자주 액세스되는 노드가 트리의 루트 근처에 있으므로 빠르게 액세스할 수 있습니다.

## 운영

스플레이 트리에서 수행할 수 있는 기본 작업은 삽입, 조회 및 제거입니다.

### 삽입

트리에 새 노드를 삽입하려면 먼저 올바른 위치를 찾아야 합니다. 루트에서 시작하여 삽입하려는 노드보다 큰 노드를 찾을 때까지 트리를 탐색하여 이 작업을 수행합니다. 그런 다음 새 노드를 해당 노드의 자식으로 삽입합니다.

새 노드가 삽입되면 이를 루트로 확장해야 합니다. 이를 위해 먼저 새 노드를 트리의 루트로 만듭니다. 그런 다음 이전에 루트(현재 새 노드의 부모)였던 노드를 추적하여 새 노드의 왼쪽 자식으로 만듭니다. 마지막으로 새 노드의 오른쪽 자식을 이전 루트로 만듭니다.

```javascript
function insert(value) {
    if (root === null) {
        root = new Node(value);
        return;
    }
 
    var curr = root;
    var parent = null;
    while (curr !== null) {
        if (value < curr.value) {
            parent = curr;
            curr = curr.left;
        } else if (value > curr.value) {
            parent = curr;
            curr = curr.right;
        } else {
            // value already exists in tree
            return;
        }
    }
 
    var newNode = new Node(value);
    if (value < parent.value) {
        parent.left = newNode;
    } else {
        parent.right = newNode;
    }
 
    // splay newNode to the root
    splay(newNode);
}
```

### 찾아보기

트리에서 값을 찾기 위해 루트에서 시작하여 값을 찾거나 값이 트리에 있는 노드에 도달할 때까지 트리를 순회합니다.

노드를 찾으면 루트로 확장합니다. 값이 트리에 없으면 루트로 확장되는 노드는 값이 트리에 있는 노드가 됩니다.

```javascript
function lookup(value) {
    if (root === null) {
        return null;
    }
 
    var curr = root;
    while (curr !== null) {
        if (value < curr.value) {
            curr = curr.left;
        } else if (value > curr.value) {
            curr = curr.right;
        } else {
            // value found
            break;
        }
    }
 
    splay(curr);
    return curr;
}
```

### 제거

트리에서 값을 제거하려면 먼저 값이 포함된 노드를 찾아야 합니다. 루트에서 시작하여 값을 찾을 때까지 또는 값이 트리에 있는 노드에 도달할 때까지 트리를 순회하여 이 작업을 수행합니다.

값이 트리에 있으면 노드를 제거하고 부모 노드를 루트로 확장합니다. 값이 트리에 없으면 값이 트리에 있을 경우 노드를 루트로 확장합니다.

```javascript
function remove(value) {
    if (root === null) {
        return;
    }
 
    var curr = root;
    while (curr !== null) {
        if (value < curr.value) {
            curr = curr.left;
        } else if (value > curr.value) {
            curr = curr.right;
        } else {
            // value found
            break;
        }
    }
 
    if (curr === null) {
        // value not in tree
        return;
    }
 
    // remove curr
    if (curr.left === null && curr.right === null) {
        // curr is a leaf
        if (curr === root) {
            root = null;
        } else {
            var parent = curr.parent;
            if (parent.left === curr) {
                parent.left = null;
            } else {
                parent.right = null;
            }
 
            splay(parent);
        }
    } else if (curr.left === null) {
        // curr has only right child
        if (curr === root) {
            root = curr.right;
            root.parent = null;
        } else {
            var parent = curr.parent;
            curr.right.parent = parent;
            if (parent.left === curr) {
                parent.left = curr.right;
            } else {
                parent.right = curr.right;
            }
 
            splay(parent);
        }
    } else if (curr.right === null) {
        // curr has only left child
        if (curr === root) {
            root = curr.left;
            root.parent = null;
        } else {
            var parent = curr.parent;
            curr.left.parent = parent;
            if (parent.left === curr) {
                parent.left = curr.left;
            } else {
                parent.right = curr.left;
            }
 
            splay(parent);
        }
    } else {
        // curr has both left and right child
        var next = curr.right;
        while (next.left !== null) {
            next = next.left;
        }
 
        // next is the successor of curr (the smallest node in curr's right subtree)
        // remove next from its current position and replace it with its right child
        var parent = next.parent;
        if (parent.left === next) {
            parent.left = next.right;
        } else {
            parent.right = next.right;
        }
        if (next.right !== null) {
            next.right.parent = parent;
        }
 
        // replace curr with next
        next.left = curr.left;
        next.right = curr.right;
        next.parent = curr.parent;
        curr.left.parent = next;
        curr.right.parent = next;
        if (curr === root) {
            root = next;
        } else {
            if (curr.parent.left === curr) {
                curr.parent.left = next;
            } else {
                curr.parent.right = next;
            }
        }
 
        splay(next);
    }
}
```

## 스플레잉

스플레이는 노드를 트리의 루트로 이동하는 프로세스입니다. 이것은 일련의 회전에 의해 수행됩니다. 수행되는 회전 유형은 루트에 대한 노드의 위치에 따라 다릅니다.

세 가지 가능한 경우가 있습니다.

- 노드가 루트이므로 회전이 필요하지 않습니다.
- 노드는 루트의 자식입니다. 단일 회전이 필요합니다.
- 노드가 루트의 자식이 아닙니다. 이중 회전이 필요합니다.

### 단일 회전

확장할 노드가 루트의 자식일 때 단일 회전이 수행됩니다. 노드가 루트의 왼쪽 자식인지 오른쪽 자식인지에 따라 두 가지 가능한 경우가 있습니다.

#### 왼쪽 회전

```javascript
function leftRotate(node) {
    var rightChild = node.right;
    node.right = rightChild.left;
    if (rightChild.left !== null) {
        rightChild.left.parent = node;
    }
    rightChild.parent = node.parent;
    if (node.parent === null) {
        root = rightChild;
    } else if (node === node.parent.left) {
        node.parent.left = rightChild;
    } else {
        node.parent.right = rightChild;
    }
    rightChild.left = node;
    node.parent = rightChild;
}
```

#### 오른쪽 회전

```javascript
function rightRotate(node) {
    var leftChild = node.left;
    node.left = leftChild.right;
    if (leftChild.right !== null) {
        leftChild.right.parent = node;
    }
    leftChild.parent = node.parent;
    if (node.parent === null) {
        root = leftChild;
    } else if (node === node.parent.right) {
        node.parent.right = leftChild;
    } else {
        node.parent.left = leftChild;
    }
    leftChild.right = node;
    node.parent = leftChild;
}
```

### 이중 회전

확장할 노드가 루트의 자식이 아닌 경우 이중 회전이 수행됩니다. 노드가 루트의 왼쪽 자식인지 오른쪽 자식인지, 노드의 부모가 루트의 왼쪽 자식인지 오른쪽 자식인지에 따라 네 가지 가능한 경우가 있습니다.

#### 좌우 회전

```javascript
function leftRightRotate(node) {
    var leftChild = node.left;
    var leftRightChild = leftChild.right;
    leftChild.right = leftRightChild.left;
    if (leftRightChild.left !== null) {
        leftRightChild.left.parent = leftChild;
    }
    node.left = leftRightChild.right;
    if (leftRightChild.right !== null) {
        leftRightChild.right.parent = node;
    }
    leftRightChild.left = leftChild;
    leftRightChild.right = node;
    leftChild.parent = leftRightChild;
    node.parent = leftRightChild;
    leftRightChild.parent = node.parent;
    if (node.parent === null) {
        root = leftRightChild;
    } else if (node === node.parent.left) {
        node.parent.left = leftRightChild;
    } else {
        node.parent.right = leftRightChild;
    }
}
```

#### 오른쪽-왼쪽 회전

```javascript
function rightLeftRotate(node) {
    var rightChild = node.right;
    var rightLeftChild = rightChild.left;
    rightChild.left = rightLeftChild.right;
    if (rightLeftChild.right !== null) {
        rightLeftChild.right.parent = rightChild;
    }
    node.right = rightLeftChild.left;
    if (rightLeftChild.left !== null) {
        rightLeftChild.left.parent = node;
    }
    rightLeftChild.right = rightChild;
    rightLeftChild.left = node;
    rightChild.parent = rightLeftChild;
    node.parent = rightLeftChild;
    rightLeftChild.parent = node.parent;
    if (node.parent === null) {
        root = rightLeftChild;
    } else if (node === node.parent.left) {
        node.parent.left = rightLeftChild;
    } else {
        node.parent.right = rightLeftChild;
    }
}
```

## 복잡성

스플레이 트리 작업의 시간 복잡도는 O(log(n))로 상각됩니다. 이는 평균적으로 작업에 O(log(n)) 시간이 걸린다는 것을 의미합니다. 그러나 최악의 경우 O(n) 시간이 걸릴 수 있습니다.

스플레이 트리의 공간 복잡도는 O(n)이며, 여기서 n은 트리의 노드 수입니다.