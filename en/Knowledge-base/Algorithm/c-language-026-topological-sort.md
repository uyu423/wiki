---
title: [C Language] 026: Topological Sort
description: 
published: true
date: 2023-02-13T07:33:01.299Z
tags: 
editor: markdown
dateCreated: 2023-02-13T07:32:54.498Z
---

- [[Lenguaje C] 026: Clasificación topológica***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-026-topological-sort)
{.links-list}
- [[C语言]026：拓扑排序***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-026-topological-sort)
{.links-list}
- [[C언어] 026: 위상정렬***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-026-topological-sort)
{.links-list}


# 026: Topological Sort

In computer science, a topological sort or topological ordering of a directed graph is a linear ordering of its vertices such that for every directed edge uv from vertex u to vertex v, u comes before v in the ordering. For instance, the vertices of the graph may represent tasks to be performed, and the edges may represent constraints that one task must be performed before another; in this application, a topological ordering is just a valid sequence for the tasks. A topological ordering is possible if and only if the graph has no directed cycles, that is, if it is a directed acyclic graph (DAG). Any DAG has at least one topological ordering, and algorithms are known for constructing a topological ordering of any DAG in linear time.

Topological sorting has the advantage of allowing tasks to be processed in an order that is consistent with the dependencies between them, without having to worry about cycles. It is often used in situations where it is necessary to resolve dependencies, such as in the installation of software packages on a computer.

## Algorithm

There are multiple algorithms that can be used to perform a topological sort. One of the most common is Kahn's algorithm, which is outlined below:

1. Choose any vertex v as the starting vertex.
2. Find all the vertices that have no incoming edges and add them to a queue.
3. While the queue is not empty:
    - Remove a vertex from the queue.
    - Find all the vertices that have an edge from the removed vertex to them and add them to the queue.
    - Output the removed vertex.
4. If there are any vertices left in the graph that have not been output, then the graph must have a cycle and therefore a topological sort is not possible.

## Implementation

Below is an implementation of Kahn's algorithm in the C programming language:

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

## Complexity Analysis

The time complexity of Kahn's algorithm is O(V + E), where V is the number of vertices and E is the number of edges. The space complexity is also O(V + E), since we need to store the adjacency list and in-degree of each vertex.