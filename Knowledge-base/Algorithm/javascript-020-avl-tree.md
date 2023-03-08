---
title: [JavaScript] 020: AVL 트리
description: 
published: true
date: 2023-02-09T22:32:19.234Z
tags: 
editor: markdown
dateCreated: 2023-02-09T22:32:17.581Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[JavaScript] 020: AVL Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-020-avl-tree)
{.links-list}


# JavaScript 020: AVL 트리

AVL 트리는 자체 균형 이진 검색 트리의 한 유형으로, 임의 노드의 두 자식 하위 트리 높이가 최대 1만큼 차이가 나도록 노드가 배열됩니다. 이 트리 균형을 통해 트리가 균형 상태에 더 가까워질 가능성이 높으므로 값을 검색할 때 더 효율적입니다.

AVL 트리의 높이는 루트에서 리프까지 가장 긴 경로의 가장자리 수입니다. 빈 트리의 높이는 -1로 정의됩니다. 루트의 왼쪽 및 오른쪽 하위 트리의 높이가 최대 1만큼 다르고 왼쪽 및 오른쪽 하위 트리가 AVL 트리인 경우 AVL 트리가 균형을 이룬다고 합니다.

## 코드 예시

다음은 JavaScript에서 AVL 트리에 노드를 삽입하는 방법의 예입니다.

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

## 운동

1. JavaScript에서 AVL 트리를 구현합니다.

2. 숫자 목록이 주어지면 해당 숫자의 AVL 트리를 만듭니다.

3. AVL 트리의 높이를 찾습니다.

4. AVL 트리에서 최소값을 찾습니다.

5. AVL 트리에서 최대값을 찾습니다.

6. AVL 트리에서 주어진 값의 선행 항목을 찾습니다.

7. AVL 트리에서 주어진 값의 후속 항목을 찾습니다.

8. AVL 트리에서 값을 삭제합니다.

9. AVL 트리의 사전 순회를 수행합니다.

10. AVL 트리의 순회를 수행합니다.

11. AVL 트리의 사후 순회를 수행합니다.