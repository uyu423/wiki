---
title: [C언어] 018: 건너뛰기 목록
description: 
published: true
date: 2023-02-13T02:32:45.921Z
tags: 
editor: markdown
dateCreated: 2023-02-13T02:32:38.538Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 018: Skip List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-018-skip-list)
{.links-list}


# 건너뛰기 목록

건너뛰기 목록은 순서가 지정된 요소 시퀀스 내에서 효율적인 검색을 허용하는 데이터 구조입니다. 건너뛰기 목록은 1990년 Pugh에 의해 처음 설명되었으며 다양한 응용 프로그램에서 매우 유용한 것으로 밝혀졌습니다.

건너뛰기 목록은 추가 수준의 포인터가 있는 연결 목록입니다. 건너뛰기 목록은 각 노드가 같은 수준의 다음 노드에 대한 포인터와 그 아래 수준의 다음 노드에 대한 포인터를 갖도록 구성됩니다.

레벨 수는 요소를 찾을 확률이 높도록 선택됩니다. 건너뛰기 목록의 높이는 요소를 찾기 위한 예상 단계 수가 목록의 요소 수에서 대수가 되도록 선택됩니다.

다음은 6개 요소가 있는 건너뛰기 목록의 예입니다.

![](https://github.com/BryanBo-Chen/Algorithm-Data-Structure-notes/blob/master/assets/skiplist.png)

## 운영

건너뛰기 목록은 다음 작업을 지원합니다.

- 주어진 키로 요소를 검색합니다.
- 주어진 키로 요소를 삽입합니다.
- 주어진 키로 요소를 삭제합니다.

이러한 작업의 시간 복잡도는 다음과 같습니다.

- 검색: O(log n)
- 삽입: O(log n)
- 삭제: O(log n)

여기서 n은 건너뛰기 목록의 요소 수입니다.

## 구현

건너뛰기 목록은 연결 목록을 사용하여 구현할 수 있습니다. 건너뛰기 목록의 각 노드에는 같은 수준의 다음 노드와 그 아래 수준의 다음 노드에 대한 키와 포인터가 포함되어 있습니다.

다음은 C에서 건너뛰기 목록을 구현한 예입니다.

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
 
typedef struct node {
    int key;
    struct node *next;
    struct node *down;
} node;
 
node *create_node(int key, node *next, node *down) {
    node *n = malloc(sizeof(node));
    n->key = key;
    n->next = next;
    n->down = down;
    return n;
}
 
node *create_skip_list(int *keys, int n, int h) {
    node *head, *tail, *curr, *down;
    int i, j;
 
    head = create_node(0, NULL, NULL);
    tail = create_node(0, NULL, NULL);
    down = head;
 
    for (i = 0; i < h; i++) {
        curr = create_node(0, tail, down);
        down->next = curr;
        down = tail;
        for (j = 0; j < n; j++) {
            curr->next = create_node(keys[j], tail, NULL);
            curr = curr->next;
        }
    }
 
    return head;
}
 
void print_skip_list(node *head) {
    node *curr;
 
    while (head != NULL) {
        curr = head;
        while (curr->next != NULL) {
            printf("%d -> ", curr->next->key);
            curr = curr->next;
        }
        printf("NULL\n");
        head = head->down;
    }
}
 
node *search(node *head, int key) {
    node *curr;
 
    while (head != NULL) {
        curr = head;
        while (curr->next != NULL && curr->next->key <= key) {
            if (curr->next->key == key) {
                return curr->next;
            }
            curr = curr->next;
        }
        head = head->down;
    }
 
    return NULL;
}
 
node *insert(node *head, int key) {
    node *curr, *down, *new_node;
    int i;
 
    curr = head;
    down = NULL;
 
    while (curr != NULL) {
        while (curr->next != NULL && curr->next->key < key) {
            curr = curr->next;
        }
 
        if (curr->next != NULL && curr->next->key == key) {
            return curr->next;
        }
 
        new_node = create_node(key, curr->next, NULL);
        curr->next = new_node;
 
        if (down != NULL) {
            down->down = new_node;
        }
 
        down = new_node;
        curr = curr->down;
    }
 
    i = 0;
 
    while (rand() % 2 == 0) {
        if (i >= head->key) {
            break;
        }
 
        new_node = create_node(0, NULL, head);
        head->down = new_node;
        head = new_node;
 
        i++;
    }
 
    head->key = i;
 
    return NULL;
}
 
node *delete(node *head, int key) {
    node *curr, *down, *tmp;
 
    curr = head;
    down = NULL;
 
    while (curr != NULL) {
        while (curr->next != NULL && curr->next->key < key) {
            curr = curr->next;
        }
 
        if (curr->next == NULL || curr->next->key > key) {
            down = curr->down;
            curr = down;
            continue;
        }
 
        tmp = curr->next;
        curr->next = curr->next->next;
        free(tmp);
 
        if (down != NULL) {
            down->down = curr;
        }
 
        down = curr;
        curr = curr->down;
    }
 
    while (head->next == NULL) {
        tmp = head;
        head = head->down;
        free(tmp);
    }
 
    return head;
}
 
int main() {
    int keys[] = {1, 2, 3, 4, 5, 6};
    int n = sizeof(keys) / sizeof(keys[0]);
    int h = 3;
 
    node *head = create_skip_list(keys, n, h);
 
    print_skip_list(head);
 
    return 0;
}
```

## 운동

1. 건너뛰기 목록 작업을 구현합니다.

2. 건너뛰기 목록의 헤드를 반환하도록 삽입 및 삭제 작업을 수정합니다.

3. 주어진 키보다 작거나 같은 가장 큰 키를 가진 노드를 반환하도록 검색 작업을 수정합니다.

4. 노드 **포인터**를 인수로 사용하고 건너뛰기 목록에서 노드를 삽입하거나 삭제하도록 삽입 및 삭제 작업을 수정합니다.

5. 이중 연결 목록을 사용하여 건너뛰기 목록의 작업을 구현합니다.