---
title: [C语言]027：最小生成树
description: 
published: true
date: 2023-02-13T08:34:03.579Z
tags: 
editor: markdown
dateCreated: 2023-02-13T08:34:01.910Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 027: Minimum Spanning Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-027-minimum-spanning-tree)
{.links-list}


# 027：最小生成树

无向图的最小生成树 (MST) 是分配给它的最小可能权重的生成树。更一般地，MST 是图的边的任何子集，它形成包含图的所有顶点的树。

MST 的权重是 MST 中边的权重之和。寻找 MST 的问题是计算机科学中的一个经典问题，在其他算法中经常被用作子问题。

有许多算法可以找到 MST，包括 Kruskal 算法和 Prim 算法。

## Kruskal 算法

Kruskal 算法是一种贪婪算法，它通过从具有最低权重的边开始并添加边直到所有顶点都连接来找到 MST。

该算法的工作原理如下：

1.按权重对边进行排序。
2. 选择权重最小的边并将其添加到 MST。
3. 选择下一个权重最低的边并将其添加到 MST，除非它创建一个循环。
4. 重复步骤3，直到所有的顶点都连接起来。

## 普里姆算法

Prim 算法是另一种贪婪算法，它通过从单个顶点开始并添加边直到所有顶点都连接来找到 MST。

该算法的工作原理如下：

1. 选择一个起始顶点。
2. 选择连接起始顶点和另一个顶点的权重最小的边，并将其添加到 MST。
3. 选择连接 MST 和另一个顶点的具有最低权重的下一条边，并将其添加到 MST。
4. 重复步骤3，直到所有的顶点都连接起来。

## 代码示例

这是 Kruskal 算法在 C 中的简单实现。该算法使用不相交集数据结构来跟踪哪些顶点位于同一连通分量中。

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

## 锻炼

1. 实现 Prim 的算法来寻找 MST。

## 答案

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