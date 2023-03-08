---
title: [Lenguaje C] 027: árbol de expansión mínimo
description: 
published: true
date: 2023-02-13T08:34:03.591Z
tags: 
editor: markdown
dateCreated: 2023-02-13T08:34:01.918Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 027: Minimum Spanning Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-027-minimum-spanning-tree)
{.links-list}


# 027: Árbol de expansión mínimo

Un árbol de expansión mínimo (MST) de un gráfico no dirigido es un árbol de expansión que tiene asignado el peso mínimo posible. Más generalmente, MST es cualquier subconjunto de los bordes de un gráfico que forma un árbol que incluye todos los vértices del gráfico.

El peso de un MST es la suma de los pesos de los bordes en el MST. El problema de encontrar un MST es un problema clásico en informática y, a menudo, se usa como un subproblema en otros algoritmos.

Hay una serie de algoritmos para encontrar un MST, incluido el algoritmo de Kruskal y el algoritmo de Prim.

## Algoritmo de Kruskal

El algoritmo de Kruskal es un algoritmo codicioso que encuentra un MST comenzando con los bordes con los pesos más bajos y agregando bordes hasta que todos los vértices estén conectados.

El algoritmo funciona de la siguiente manera:

1. Clasifique los bordes por peso.
2. Elija el borde con el peso más bajo y agréguelo al MST.
3. Elija el siguiente borde con el peso más bajo y agréguelo al MST, a menos que cree un ciclo.
4. Repite el paso 3 hasta que todos los vértices estén conectados.

## Algoritmo de Prim

El algoritmo de Prim es otro algoritmo codicioso que encuentra un MST comenzando con un solo vértice y agregando bordes hasta que todos los vértices estén conectados.

El algoritmo funciona de la siguiente manera:

1. Elija un vértice inicial.
2. Elija el borde con el peso más bajo que conecta el vértice inicial con otro vértice y agréguelo al MST.
3. Elija el siguiente borde con el peso más bajo que conecta el MST con otro vértice y agréguelo al MST.
4. Repite el paso 3 hasta que todos los vértices estén conectados.

## Ejemplo de código

Aquí hay una implementación simple del algoritmo de Kruskal en C. El algoritmo utiliza una estructura de datos de conjunto disjunto para realizar un seguimiento de qué vértices están en el mismo componente conectado.

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

// a structure to represent an edge in the graph
struct Edge
{
    int src, dest, weight;
};

// a structure to represent a graph
struct Graph
{
    // V-> Number of vertices, E-> Number of edges
    int V, E;

    // graph is represented as an array of edges.
    struct Edge* edge;
};

// Creates a graph with V vertices and E edges
struct Graph* createGraph(int V, int E)
{
    struct Graph* graph = (struct Graph*) malloc( sizeof(struct Graph) );
    graph->V = V;
    graph->E = E;

    graph->edge = (struct Edge*) malloc( graph->E * sizeof( struct Edge ) );

    return graph;
}

// A structure to represent a subset for union-find
struct subset
{
    int parent;
    int rank;
};

// A utility function to find set of an element i
// (uses path compression technique)
int find(struct subset subsets[], int i)
{
    // find root and make root as parent of i (path compression)
    if (subsets[i].parent != i)
        subsets[i].parent = find(subsets, subsets[i].parent);

    return subsets[i].parent;
}

// A function that does union of two sets of x and y
// (uses union by rank)
void Union(struct subset subsets[], int x, int y)
{
    int xroot = find(subsets, x);
    int yroot = find(subsets, y);

    // Attach smaller rank tree under root of high rank tree
    // (Union by Rank)
    if (subsets[xroot].rank < subsets[yroot].rank)
        subsets[xroot].parent = yroot;
    else if (subsets[xroot].rank > subsets[yroot].rank)
        subsets[yroot].parent = xroot;

    // If ranks are same, then make one as root and increment
    // its rank by one
    else
    {
        subsets[yroot].parent = xroot;
        subsets[xroot].rank++;
    }
}

// Compare two edges according to their weights.
// Used in qsort() for sorting an array of edges
int myComp(const void* a, const void* b)
{
    struct Edge* a1 = (struct Edge*)a;
    struct Edge* b1 = (struct Edge*)b;
    return a1->weight > b1->weight;
}

// The main function to construct MST using Kruskal's algorithm
void KruskalMST(struct Graph* graph)
{
    int V = graph->V;
    struct Edge result[V];  // Tnis will store the resultant MST
    int e = 0;  // An index variable, used for result[]
    int i = 0;  // An index variable, used for sorted edges

    // Step 1:  Sort all the edges in non-decreasing order of their weight
    // If we are not allowed to change the given graph, we can create a copy of
    // array of edges
    qsort(graph->edge, graph->E, sizeof(graph->edge[0]), myComp);

    // Allocate memory for creating V ssubsets
    struct subset *subsets =
        (struct subset*) malloc( V * sizeof(struct subset) );

    // Create V subsets with single elements
    for (int v = 0; v < V; ++v)
    {
        subsets[v].parent = v;
        subsets[v].rank = 0;
    }

    // Number of edges to be taken is equal to V-1
    while (e < V - 1)
    {
        // Step 2: Pick the smallest edge. And increment the index
        // for next iteration
        struct Edge next_edge = graph->edge[i++];

        int x = find(subsets, next_edge.src);
        int y = find(subsets, next_edge.dest);

        // If including this edge does't cause cycle, include it
        // in result and increment the index of result for next edge
        if (x != y)
        {
            result[e++] = next_edge;
            Union(subsets, x, y);
        }
        // Else discard the next_edge
    }

    // print the contents of result[] to display the built MST
    printf("Following are the edges in the constructed MST\n");
    for (i = 0; i < e; ++i)
        printf("%d -- %d == %d\n", result[i].src, result[i].dest,
                                                   result[i].weight);
    return;
}

// Driver program to test above functions
int main()
{
    /* Let us create following weighted graph
             10
        0--------1
        |  \     |
       6|   5\   |15
        |      \ |
        2--------3
            4       */
    int V = 4;  // Number of vertices in graph
    int E = 5;  // Number of edges in graph
    struct Graph* graph = createGraph(V, E);


    // add edge 0-1
    graph->edge[0].src = 0;
    graph->edge[0].dest = 1;
    graph->edge[0].weight = 10;

    // add edge 0-2
    graph->edge[1].src = 0;
    graph->edge[1].dest = 2;
    graph->edge[1].weight = 6;

    // add edge 0-3
    graph->edge[2].src = 0;
    graph->edge[2].dest = 3;
    graph->edge[2].weight = 5;

    // add edge 1-3
    graph->edge[3].src = 1;
    graph->edge[3].dest = 3;
    graph->edge[3].weight = 15;

    // add edge 2-3
    graph->edge[4].src = 2;
    graph->edge[4].dest = 3;
    graph->edge[4].weight = 4;

    KruskalMST(graph);

    return 0;
}
```

## Ejercicio

1. Implemente el algoritmo de Prim para encontrar un MST.

## Respuestas

1.

```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

// a structure to represent a node in the graph
struct Node
{
    int vertex;
    int weight;
};

// a structure to represent a graph
struct Graph
{
    int V;
    struct Node* array;
};

// a utility function to create a new node
struct Node* newNode(int v, int w)
{
    struct Node* node = (struct Node*)malloc(sizeof(struct Node));
    node->vertex = v;
    node->weight = w;

    return node;
}

// a utility function to create a new graph
struct Graph* createGraph(int V)
{
    struct Graph* graph = (struct Graph*)malloc(sizeof(struct Graph));
    graph->V = V;

    // create an array of pointers for adjacency lists
    graph->array = (struct Node**)malloc(V * sizeof(struct Node*));

    // initialize each adjacency list as empty by setting the head as NULL
    for (int i = 0; i < V; ++i)
        graph->array[i] = NULL;

    return graph;
}

// a utility function to add an edge to an undirected graph
void addEdge(struct Graph* graph, int src, int dest, int weight)
{
    // Add an edge from src to dest.  A new node is added to the adjacency
    // list of src.  The node is added at the begining
    struct Node* node = newNode(dest, weight);
    node->next = graph->array[src];
    graph->array[src] = node;

    // Since graph is undirected, add an edge from dest to src also
    node = newNode(src, weight);
    node->next = graph->array[dest];
    graph->array[dest] = node;
}

// a utility function to find the vertex with minimum distance value, from
// the set of vertices not yet included in shortest path tree
int minDistance(int dist[], bool sptSet[], int V)
{
    // Initialize min value
    int min = INT_MAX, min_index;

    for (int v = 0; v < V; v++)
        if (sptSet[v] == false && dist[v] <= min)
            min = dist[v], min_index = v;

    return min_index;
}

// A utility function to print the constructed distance array
void printSolution(int dist[], int V)
{
    printf("Vertex   Distance from Source\n");
    for (int i = 0; i < V; ++i)
        printf("%d \t\t %d\n", i, dist[i]);
}

// Funtion that implements Dijkstra's single source shortest path algorithm
// for a graph represented using adjacency matrix representation
void dijkstra(struct Graph* graph, int src)
{
    int V = graph->V;
    int dist[V];     // The output array.  dist[i] will hold the shortest
                    // distance from src to i

    bool sptSet[V]; // sptSet[i] will true if vertex i is included in shortest
                    // path tree or shortest distance from src to i is finalized

    // Initialize all distances as INFINITE and stpSet[] as false
    for (int i = 0; i < V; i++)
        dist[i] = INT_MAX, sptSet[i] = false;

    // Distance of source vertex from itself is always 0
    dist[src] = 0;

    // Find shortest path for all vertices
    for (int count = 0; count < V-1; count++)
    {
        // Pick the minimum distance vertex from the set of vertices not
        // yet processed. u is always equal to src in first iteration.
        int u = minDistance(dist, sptSet, V);

        // Mark the picked vertex as processed
        sptSet[u] = true;

        // Update dist value of the adjacent vertices of the picked vertex.
        struct Node* node = graph->array[u];
        while (node != NULL)
        {
            // Update dist[v] only if is not in sptSet, there is an edge from
            // u to v, and total weight of path from src to  v through u is
            // smaller than current value of dist[v]
            int v = node->vertex;
            if (!sptSet[v] && node->weight &&
                dist[u] != INT_MAX &&
                dist[u]+node->weight < dist[v])
                dist[v] = dist[u] + node->weight;
            node = node->next;
        }
    }

    // print the constructed distance array
    printSolution(dist, V);
}

// Driver program to test above functions
int main()
{
    // create the graph given in above fugure
    int V = 9;
    struct Graph* graph = createGraph(V);
    addEdge(graph, 0, 1, 4);
    addEdge(graph, 0, 7, 8);
    addEdge(graph, 1, 2, 8);
    addEdge(graph, 1, 7, 11);
    addEdge(graph, 2, 3, 7);
    addEdge(graph, 2, 8, 2);
    addEdge(graph, 2, 5, 4);
    addEdge(graph, 3, 4, 9);
    addEdge(graph, 3, 5, 14);
    addEdge(graph, 4, 5, 10);
    addEdge(graph, 5, 6, 2);
    addEdge(graph, 6, 7, 1);
    addEdge(graph, 6, 8, 6);
    addEdge(graph, 7, 8, 7);

    dijkstra(graph, 0);

    return 0;
}
```