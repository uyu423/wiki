---
title: [C언어] 016: 이중 연결 리스트
description: 
published: true
date: 2023-02-11T21:18:16.259Z
tags: 
editor: markdown
dateCreated: 2023-02-11T21:18:14.575Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 016: Doubly Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-016-doubly-linked-list)
{.links-list}


# 이중 연결 리스트

이중 연결 리스트는 각 노드가 하나가 아닌 두 개의 다른 노드에 연결된 연결 리스트 유형입니다. 이를 통해 목록의 양방향 순회가 가능합니다.

## 개념

이중 연결 리스트는 링크로 연결된 노드 집합으로 구성된 데이터 구조입니다. 각 노드에는 두 개의 필드가 있습니다.

- 노드와 관련된 정보를 저장하는 **data** 필드.
- 목록의 다음 노드에 대한 참조를 저장하는 **next** 필드.
- 목록의 이전 노드에 대한 참조를 저장하는 **prev** 필드.

이중 연결 목록의 첫 번째 노드와 마지막 노드는 각각 **head** 및 **tail** 노드라고 합니다. 헤드 노드는 목록의 첫 번째 노드이고 꼬리 노드는 목록의 마지막 노드입니다.

테일 노드의 **next** 필드에는 헤드 노드에 대한 참조가 포함되고 헤드 노드의 **prev** 필드에는 테일 노드에 대한 참조가 포함됩니다. 이를 통해 목록의 양방향 순회가 가능합니다.

## 코드 예

다음은 C 프로그래밍 언어의 이중 연결 목록의 예입니다.

```c
struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(int data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(int data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(curr_node->data == data) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%d ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

int main() {
    insert_node(1);
    insert_node(2);
    insert_node(3);
    insert_node(4);
    insert_node(5);

    print_list();

    delete_node(3);

    print_list();

    return 0;
}
```

## 운동

1. C 프로그래밍 언어로 이중 연결 목록을 구현합니다.

2. 이중 연결 목록에서 다음 작업을 구현합니다.

- 목록의 맨 위에 노드를 삽입합니다.
- 목록의 끝에 노드를 삽입합니다.
- 목록에서 노드를 삭제합니다.
- 목록에서 노드를 검색합니다.
- 목록의 순서를 반대로 합니다.

3. 이중 연결 목록을 사용하여 정수 목록을 저장하는 프로그램을 작성하십시오. 프로그램은 사용자가 다음 작업을 수행할 수 있도록 허용해야 합니다.

- 목록의 맨 앞에 새 정수를 삽입합니다.
- 목록의 끝에 새 정수를 삽입합니다.
- 목록에서 정수를 삭제합니다.
- 목록에서 정수를 검색합니다.
- 목록의 내용을 인쇄합니다.

4. 이중 연결 목록을 사용하여 문자열 목록을 저장하는 프로그램을 작성하십시오. 프로그램은 사용자가 다음 작업을 수행할 수 있도록 허용해야 합니다.

- 목록의 맨 앞에 새 문자열을 삽입합니다.
- 목록의 끝에 새 문자열을 삽입합니다.
- 목록에서 문자열을 삭제합니다.
- 목록에서 문자열을 검색합니다.
- 목록의 내용을 인쇄합니다.

## 답변

1. 다음은 이중 연결 목록의 C 구현입니다.

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(int data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(int data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(curr_node->data == data) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%d ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

int main() {
    insert_node(1);
    insert_node(2);
    insert_node(3);
    insert_node(4);
    insert_node(5);

    print_list();

    delete_node(3);

    print_list();

    return 0;
}
```

2. 다음은 이중 연결 목록 작업의 C 구현입니다.

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(int data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(int data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(curr_node->data == data) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%d ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

void reverse_list() {
    struct node* curr_node = head;
    struct node* temp_node = NULL;

    while(curr_node != NULL) {
        temp_node = curr_node->prev;
        curr_node->prev = curr_node->next;
        curr_node->next = temp_node;

        curr_node = curr_node->prev;
    }

    if(temp_node != NULL) {
        head = temp_node->prev;
    }
}

int main() {
    insert_node(1);
    insert_node(2);
    insert_node(3);
    insert_node(4);
    insert_node(5);

    print_list();

    delete_node(3);

    print_list();

    reverse_list();

    print_list();

    return 0;
}
```

3. 다음은 이중 연결 목록을 사용하여 정수 목록을 저장하는 프로그램의 C 구현입니다.

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(int data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(int data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(curr_node->data == data) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%d ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

int main() {
    int data;

    while(1) {
        printf("Enter an integer (Enter -1 to exit): ");
        scanf("%d", &data);

        if(data == -1) {
            break;
        }

        insert_node(data);
    }

    print_list();

    while(1) {
        printf("Enter an integer to delete (Enter -1 to exit): ");
        scanf("%d", &data);

        if(data == -1) {
            break;
        }

        delete_node(data);
    }

    print_list();

    return 0;
}
```

4. 다음은 이중 연결 목록을 사용하여 문자열 목록을 저장하는 프로그램의 C 구현입니다.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct node {
    char data[100];
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(char* data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    strcpy(new_node->data, data);
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(char* data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(strcmp(curr_node->data, data) == 0) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%s ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

int main() {
    char data[100];

    while(1) {
        printf("Enter a string (Enter -1 to exit): ");
        scanf("%s", data);

        if(strcmp(data, "-1") == 0) {
            break;
        }

        insert_node(data);
    }

    print_list();

    while(1) {
        printf("Enter a string to delete (Enter -1 to exit): ");
        scanf("%s", data);

        if(strcmp(data, "-1") == 0) {
            break;
        }

        delete_node(data);
    }

    print_list();

    return 0;
}
```