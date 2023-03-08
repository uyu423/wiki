---
title: [C언어] 026: 위상정렬
description: 
published: true
date: 2023-02-13T07:32:56.072Z
tags: 
editor: markdown
dateCreated: 2023-02-13T07:32:54.491Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 026: Topological Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-026-topological-sort)
{.links-list}


# 026: 토폴로지 정렬

컴퓨터 과학에서 유향 그래프의 토폴로지 정렬 또는 토폴로지 순서는 정점 u에서 정점 v까지의 모든 방향성 가장자리 uv에 대해 순서에서 u가 v보다 먼저 오는 정점의 선형 순서입니다. 예를 들어, 그래프의 정점은 수행할 작업을 나타낼 수 있으며 가장자리는 한 작업이 다른 작업보다 먼저 수행되어야 하는 제약 조건을 나타낼 수 있습니다. 이 애플리케이션에서 토폴로지 순서는 작업에 대한 유효한 순서일 뿐입니다. 토폴로지 순서 지정은 그래프에 방향성 주기가 없는 경우, 즉 DAG(방향성 비순환 그래프)인 경우에만 가능합니다. 모든 DAG에는 적어도 하나의 토폴로지 순서가 있으며 알고리즘은 선형 시간에서 모든 DAG의 토폴로지 순서를 구성하는 것으로 알려져 있습니다.

위상 정렬은 주기에 대해 걱정할 필요 없이 작업 간의 종속성과 일치하는 순서로 작업을 처리할 수 있다는 장점이 있습니다. 컴퓨터에 소프트웨어 패키지를 설치하는 경우와 같이 종속성을 해결해야 하는 상황에서 자주 사용됩니다.

## 알고리즘

토폴로지 정렬을 수행하는 데 사용할 수 있는 여러 알고리즘이 있습니다. 가장 일반적인 것 중 하나는 아래에 설명된 Kahn의 알고리즘입니다.

1. 임의의 정점 v를 시작 정점으로 선택합니다.
2. 들어오는 가장자리가 없는 모든 정점을 찾아 대기열에 추가합니다.
3. 대기열이 비어 있지 않은 동안:
    - 큐에서 정점을 제거합니다.
    - 제거된 꼭짓점에서 가장자리가 있는 모든 꼭짓점을 찾아 대기열에 추가합니다.
    - 제거된 정점을 출력합니다.
4. 그래프에 출력되지 않은 정점이 남아 있으면 그래프에 주기가 있어야 하므로 토폴로지 정렬이 불가능합니다.

## 구현

다음은 C 프로그래밍 언어로 Kahn의 알고리즘을 구현한 것입니다.

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct node {
    int vertex;
    struct node* next;
} node;
 
typedef struct queue {
    node* head;
    node* tail;
} queue;
 
typedef struct graph {
    int numVertices;
    int* inDegree;
    queue* adjLists;
} graph;
 
void createGraph(graph* g, int numVertices) {
    g->numVertices = numVertices;
    g->inDegree = (int*) calloc(numVertices, sizeof(int));
    g->adjLists = (queue*) malloc(numVertices * sizeof(queue));
 
    int i;
    for (i = 0; i < numVertices; i++) {
        g->adjLists[i].head = NULL;
        g->adjLists[i].tail = NULL;
    }
}
 
void addEdge(graph* g, int from, int to) {
    node* newNode = (node*)malloc(sizeof(node));
    newNode->vertex = to;
    newNode->next = NULL;
 
    if (g->adjLists[from].head == NULL)
        g->adjLists[from].head = newNode;
    else
        g->adjLists[from].tail->next = newNode;
 
    g->adjLists[from].tail = newNode;
 
    g->inDegree[to]++;
}
 
queue createQueue() {
    queue q;
    q.head = NULL;
    q.tail = NULL;
    return q;
}
 
void enqueue(queue* q, int vertex) {
    node* newNode = (node*)malloc(sizeof(node));
    newNode->vertex = vertex;
    newNode->next = NULL;
 
    if (q->head == NULL)
        q->head = newNode;
    else
        q->tail->next = newNode;
 
    q->tail = newNode;
}
 
int dequeue(queue* q) {
    if (q->head == NULL)
        return -1;
 
    node* temp = q->head;
    int vertex = temp->vertex;
    q->head = temp->next;
    free(temp);
    return vertex;
}
 
int isQueueEmpty(queue q) {
    return q.head == NULL;
}
 
void printQueue(queue q) {
    node* temp = q.head;
    while (temp != NULL) {
        printf("%d ", temp->vertex);
        temp = temp->next;
    }
}
 
void topologicalSort(graph* g) {
    int i;
    queue q = createQueue();
 
    for (i = 0; i < g->numVertices; i++) {
        if (g->inDegree[i] == 0)
            enqueue(&q, i);
    }
 
    int count = 0;
    int vertex;
    while (!isQueueEmpty(q)) {
        vertex = dequeue(&q);
        printf("%d ", vertex);
        count++;
 
        node* temp = g->adjLists[vertex].head;
        while (temp != NULL) {
            int adjVertex = temp->vertex;
            g->inDegree[adjVertex]--;
 
            if (g->inDegree[adjVertex] == 0)
                enqueue(&q, adjVertex);
 
            temp = temp->next;
        }
    }
 
    if (count != g->numVertices)
        printf("There exists a cycle in the graph\n");
}
 
int main() {
    int numVertices = 6;
    graph* g = (graph*)malloc(sizeof(graph));
    createGraph(g, numVertices);
    addEdge(g, 0, 1);
    addEdge(g, 0, 2);
    addEdge(g, 1, 3);
    addEdge(g, 2, 3);
    addEdge(g, 2, 4);
    addEdge(g, 3, 5);
    addEdge(g, 4, 5);
    topologicalSort(g);
    return 0;
}
```

## 복잡성 분석

Kahn 알고리즘의 시간 복잡도는 O(V + E)입니다. 여기서 V는 정점의 수이고 E는 모서리의 수입니다. 공간 복잡도도 O(V + E)입니다. 인접 목록과 각 정점의 차수를 저장해야 하기 때문입니다.