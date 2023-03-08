---
title: [JavaScript] 042: 레드-블랙 트리
description: 
published: true
date: 2023-02-10T20:33:21.448Z
tags: 
editor: markdown
dateCreated: 2023-02-10T20:33:19.809Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 042: Red-Black Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-042-red-black-tree)
{.links-list}


# 레드-블랙 트리

레드-블랙 트리는 각 노드에 추가 비트가 있는 일종의 자체 균형 이진 검색 트리이며 해당 비트는 종종 노드의 색상(빨간색 또는 검은색)으로 해석됩니다. 이러한 트리는 키-값 쌍 세트에 매핑될 수 있는 연관 배열을 구현하는 데 사용됩니다.

이 트리의 균형 속성은 요소가 추가되고 제거될 때 대략적으로 균형 잡힌 검색 트리를 유지하는 데 사용됩니다. 트리의 균형이 완벽하지는 않지만 트리가 크게 불균형하지 않은지 확인하기에 충분합니다.

레드-블랙 트리의 기본 아이디어는 다음 속성이 충족되는 방식으로 트리의 노드를 빨간색 또는 검은색으로 색칠하는 것입니다.

1. 모든 노드는 빨강 또는 검정입니다.
2. 뿌리가 검다.
3. 모든 리프(NIL)는 검은색입니다.
4. 노드가 빨간색이면 두 자식 모두 검은색입니다.
5. 각 노드에 대해 노드에서 자손 리프까지의 모든 단순 경로에는 동일한 수의 블랙 노드가 포함됩니다.

이러한 속성은 트리가 균형을 이루도록 하여 트리의 높이가 O(log n)이 되도록 합니다.

## 코드 예제

다음은 JavaScript에서 red-black 트리를 간단하게 구현한 것입니다. 값, 색상, 왼쪽 및 오른쪽 하위 노드가 있는 Node 클래스를 정의하는 것으로 시작합니다.

```javascript
class Node {
  constructor(value, color, left, right) {
    this.value = value;
    this.color = color;
    this.left = left;
    this.right = right;
  }
}
```

또한 올바른 순서로 트리에 삽입할 수 있도록 두 노드를 비교하는 방법도 필요합니다. 비교 함수를 사용하여 이 작업을 수행할 수 있습니다. 이 함수는 두 개의 노드를 가져와서 첫 번째 노드가 두 번째 노드보다 작은지, 같은지, 큰지를 나타내는 숫자를 반환합니다.

```javascript
function compare(a, b) {
  if (a.value < b.value) {
    return -1;
  }
  if (a.value > b.value) {
    return 1;
  }
  return 0;
}
```

이제 레드-블랙 트리 클래스를 정의할 수 있습니다. 비교 함수를 인수로 취하는 생성자 함수부터 시작하겠습니다. 또한 루트 노드를 null로 초기화합니다.

```javascript
class RedBlackTree {
  constructor(compare) {
    this.compare = compare;
    this.root = null;
  }
}
```

이제 삽입 기능을 구현할 수 있습니다. 이 함수는 값을 인수로 받아 트리의 올바른 위치에 삽입합니다. 값이 이미 트리에 있으면 다시 삽입되지 않습니다.

```javascript
RedBlackTree.prototype.insert = function(value) {
  //create a new node
  let node = new Node(value, "red", null, null);

  //insert the node into the tree in the correct position
  if (this.root === null) {
    this.root = node;
  } else {
    let current = this.root;
    let parent;
    while (true) {
      parent = current;
      if (this.compare(node, current) < 0) {
        current = current.left;
        if (current === null) {
          parent.left = node;
          break;
        }
      } else if (this.compare(node, current) > 0) {
        current = current.right;
        if (current === null) {
          parent.right = node;
          break;
        }
      } else {
        //the value is already in the tree, so we don't insert it
        break;
      }
    }
  }

  //fix any violations of the red-black properties
  this.fixViolations(node);
};
```

기본적으로 이미 빨간색으로 설정되어 있으므로 새 노드의 색상을 빨간색으로 명시적으로 설정할 필요가 없습니다.

또한 노드를 인수로 사용하고 red-black 속성의 모든 위반을 수정하는 fixViolations 함수를 구현해야 합니다.

```javascript
RedBlackTree.prototype.fixViolations = function(node) {
  let current = node;
  let parent = current.parent;
  let grandParent = parent.parent;

  while (parent && parent.color === "red") {
    if (grandParent.left === parent) {
      //we are on the left side of the tree
      let uncle = grandParent.right;
      if (uncle && uncle.color === "red") {
        //case 1: the parent and uncle are both red
        parent.color = "black";
        uncle.color = "black";
        grandParent.color = "red";
        current = grandParent;
      } else {
        if (current === parent.right) {
          //case 2: the parent is red and the current node is on the right side
          //of the tree
          this.rotateLeft(parent);
          current = parent;
          parent = current.parent;
        }
        //case 3: the parent is red and the current node is on the left side
        //of the tree
        parent.color = "black";
        grandParent.color = "red";
        this.rotateRight(grandParent);
      }
    } else {
      //we are on the right side of the tree
      let uncle = grandParent.left;
      if (uncle && uncle.color === "red") {
        //case 1: the parent and uncle are both red
        parent.color = "black";
        uncle.color = "black";
        grandParent.color = "red";
        current = grandParent;
      } else {
        if (current === parent.left) {
          //case 2: the parent is red and the current node is on the left side
          //of the tree
          this.rotateRight(parent);
          current = parent;
          parent = current.parent;
        }
        //case 3: the parent is red and the current node is on the right side
        //of the tree
        parent.color = "black";
        grandParent.color = "red";
        this.rotateLeft(grandParent);
      }
    }
    parent = current.parent;
    grandParent = parent.parent;
  }

  //make sure the root node is black
  this.root.color = "black";
};
```

현재 노드 자체뿐만 아니라 부모, 조부모, 삼촌을 추적해야 한다는 점에 유의하십시오.

우리는 또한 rotateLeft 및 rotateRight 함수를 구현해야 합니다. 이 함수는 노드를 인수로 사용하고 해당 노드를 중심으로 트리를 회전합니다.

```javascript
RedBlackTree.prototype.rotateLeft = function(node) {
  let rightChild = node.right;
  node.right = rightChild.left;

  if (rightChild.left !== null) {
    rightChild.left.parent = node;
  }

  rightChild.parent = node.parent;

  if (node.parent === null) {
    this.root = rightChild;
  } else if (node === node.parent.left) {
    node.parent.left = rightChild;
  } else {
    node.parent.right = rightChild;
  }

  rightChild.left = node;
  node.parent = rightChild;
};

RedBlackTree.prototype.rotateRight = function(node) {
  let leftChild = node.left;
  node.left = leftChild.right;

  if (leftChild.right !== null) {
    leftChild.right.parent = node;
  }

  leftChild.parent = node.parent;

  if (node.parent === null) {
    this.root = leftChild;
  } else if (node === node.parent.right) {
    node.parent.right = leftChild;
  } else {
    node.parent.left = leftChild;
  }

  leftChild.right = node;
  node.parent = leftChild;
};
```

이러한 기능은 매우 간단합니다. 회전 중인 노드의 부모, 자식 및 손자만 추적하면 됩니다.

또한 값을 인수로 사용하고 해당 값이 있는 노드를 트리에서 제거하는 제거 함수를 구현할 수도 있습니다.

```javascript
RedBlackTree.prototype.remove = function(value) {
  //find the node to be removed
  let current = this.root;
  let parent = current;
  let isLeftChild = true;
  while (current.value !== value) {
    parent = current;
    if (this.compare(value, current) < 0) {
      //the value is less than the current node, so go to the left child
      isLeftChild = true;
      current = current.left;
    } else {
      //the value is greater than the current node, so go to the right child
      isLeftChild = false;
      current = current.right;
    }
    if (current === null) {
      //the value is not in the tree
      return false;
    }
  }

  //case 1: the node to be removed is a leaf
  if (current.left === null && current.right === null) {
    if (current === this.root) {
      //the tree is empty
      this.root = null;
    } else if (isLeftChild) {
      //the node is a left child
      parent.left = null;
    } else {
      //the node is a right child
      parent.right = null;
    }
  }
  //case 2: the node to be removed has one child
  else if (current.right === null) {
    //the node is a left child
    if (current === this.root) {
      this.root = current.left;
    } else if (isLeftChild) {
      parent.left = current.left;
    } else {
      parent.right = current.left;
    }
  } else if (current.left === null) {
    //the node is a right child
    if (current === this.root) {
      this.root = current.right;
    } else if (isLeftChild) {
      parent.left = current.right;
    } else {
      parent.right = current.right;
    }
  }
  //case 3: the node to be removed has two children
  else {
    //find the successor of the node to be removed
    let successor = this.getSuccessor(current);

    //connect the parent of the current node to the successor
    if (current === this.root) {
      this.root = successor;
    } else if (isLeftChild) {
      parent.left = successor;
    } else {
      parent.right = successor;
    }

    //connect the left child of the current node to the successor
    successor.left = current.left;
  }

  //fix any violations of the red-black properties
  this.fixViolations(node);

  //return true to indicate that the node was removed
  return true;
};
```

이 기능은 삽입 기능과 유사합니다. 제거되는 노드의 부모, 자식 및 손자만 추적하면 됩니다.

또한 노드를 인수로 사용하고 해당 노드의 후속 노드를 반환하는 getSuccessor 함수를 구현해야 합니다.

```javascript
RedBlackTree.prototype.getSuccessor = function(node) {
  let current = node.right;
  let parent = node;
  while (current.left !== null) {
    parent = current;
    current = current.left;
  }
  if (current !== node.right) {
    parent.left = current.right;
    current.right = node.right;
  }
  return current;
};
```

이 기능은 제거 기능과 유사합니다. 제거되는 노드의 부모, 자식 및 손자만 추적하면 됩니다.

## 관련 연습

- [ ] 이진 트리가 이진 검색 트리인지 확인하는 기능을 구현합니다.
- [ ] 이진 검색 트리에서 k번째로 작은 요소를 찾는 함수를 구현합니다.