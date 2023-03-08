---
title: [C语言]026：拓扑排序
description: 
published: true
date: 2023-02-13T07:32:56.114Z
tags: 
editor: markdown
dateCreated: 2023-02-13T07:32:54.494Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 026: Topological Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-026-topological-sort)
{.links-list}


# 026：拓扑排序

在计算机科学中，有向图的拓扑排序或拓扑排序是其顶点的线性排序，使得对于从顶点 u 到顶点 v 的每条有向边 uv，u 在排序中排在 v 之前。例如，图的顶点可能代表要执行的任务，而边可能代表一个任务必须在另一个任务之前执行的约束；在此应用程序中，拓扑排序只是任务的有效序列。当且仅当图没有有向环时，即如果它是有向无环图 (DAG)，拓扑排序是可能的。任何 DAG 都有至少一个拓扑排序，并且已知算法可以在线性时间内构造任何 DAG 的拓扑排序。

拓扑排序的好处是可以让任务按照与它们之间的依赖关系一致的顺序进行处理，而不必担心循环。常用于需要解决依赖关系的场合，比如在电脑上安装软件包。

## 算法

有多种算法可用于执行拓扑排序。最常见的算法之一是 Kahn 算法，概述如下：

1.选择任意一个顶点v作为起始顶点。
2. 找到所有没有传入边的顶点并将它们添加到队列中。
3. 当队列不为空时：
    - 从队列中删除一个顶点。
    - 找到所有从删除的顶点到它们有边的顶点并将它们添加到队列中。
    - 输出移除的顶点。
4. 如果图中还有未输出的顶点，则该图必然存在环，因此无法进行拓扑排序。

## 执行

下面是 Kahn 算法的 C 语言实现：

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

## 复杂度分析

Kahn 算法的时间复杂度为 O(V + E)，其中 V 是顶点数，E 是边数。空间复杂度也是 O(V + E)，因为我们需要存储每个顶点的邻接表和入度。