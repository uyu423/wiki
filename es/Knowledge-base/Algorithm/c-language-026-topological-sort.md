---
title: [Lenguaje C] 026: Clasificación topológica
description: 
published: true
date: 2023-02-13T07:32:56.059Z
tags: 
editor: markdown
dateCreated: 2023-02-13T07:32:54.498Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 026: Topological Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-026-topological-sort)
{.links-list}


# 026: Clasificación topológica

En informática, una clasificación topológica u ordenación topológica de un gráfico dirigido es una ordenación lineal de sus vértices, de modo que para cada arista dirigida uv desde el vértice u hasta el vértice v, u viene antes que v en la ordenación. Por ejemplo, los vértices del gráfico pueden representar tareas a realizar y los bordes pueden representar restricciones de que una tarea debe realizarse antes que otra; en esta aplicación, un ordenamiento topológico es solo una secuencia válida para las tareas. Una ordenación topológica es posible si y solo si el grafo no tiene ciclos dirigidos, es decir, si es un grafo acíclico dirigido (DAG). Cualquier DAG tiene al menos un ordenamiento topológico y se conocen algoritmos para construir un ordenamiento topológico de cualquier DAG en tiempo lineal.

La clasificación topológica tiene la ventaja de permitir que las tareas se procesen en un orden coherente con las dependencias entre ellas, sin tener que preocuparse por los ciclos. A menudo se usa en situaciones en las que es necesario resolver dependencias, como en la instalación de paquetes de software en una computadora.

## Algoritmo

Hay varios algoritmos que se pueden utilizar para realizar una ordenación topológica. Uno de los más comunes es el algoritmo de Kahn, que se describe a continuación:

1. Elija cualquier vértice v como vértice inicial.
2. Encuentra todos los vértices que no tienen aristas entrantes y agrégalos a una cola.
3. Mientras la cola no esté vacía:
    - Eliminar un vértice de la cola.
    - Encuentra todos los vértices que tienen una arista desde el vértice eliminado y agrégalos a la cola.
    - Salida del vértice eliminado.
4. Si quedan vértices en el gráfico que no se han generado, entonces el gráfico debe tener un ciclo y, por lo tanto, no es posible una ordenación topológica.

## Implementación

A continuación se muestra una implementación del algoritmo de Kahn en el lenguaje de programación C:

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

## Análisis de complejidad

La complejidad temporal del algoritmo de Kahn es O(V + E), donde V es el número de vértices y E es el número de aristas. La complejidad del espacio también es O(V + E), ya que necesitamos almacenar la lista de adyacencia y el grado de entrada de cada vértice.