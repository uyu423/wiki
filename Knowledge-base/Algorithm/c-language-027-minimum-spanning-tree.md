---
title: [C언어] 027: 최소 스패닝 트리
description: 
published: true
date: 2023-02-13T08:34:03.586Z
tags: 
editor: markdown
dateCreated: 2023-02-13T08:34:01.909Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 027: Minimum Spanning Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-027-minimum-spanning-tree)
{.links-list}


# 027: 최소 스패닝 트리

무향 그래프의 최소 스패닝 트리(MST)는 가능한 최소 가중치가 할당된 스패닝 트리입니다. 보다 일반적으로 MST는 그래프의 모든 정점을 포함하는 트리를 형성하는 그래프 가장자리의 하위 집합입니다.

MST의 가중치는 MST의 에지 가중치의 합입니다. MST를 찾는 문제는 컴퓨터 과학의 고전적인 문제이며 종종 다른 알고리즘에서 하위 문제로 사용됩니다.

Kruskal의 알고리즘과 Prim의 알고리즘을 포함하여 MST를 찾기 위한 많은 알고리즘이 있습니다.

## 크루스칼 알고리즘

Kruskal 알고리즘은 가중치가 가장 낮은 에지부터 시작하여 모든 정점이 연결될 때까지 에지를 추가하여 MST를 찾는 그리디 알고리즘입니다.

알고리즘은 다음과 같이 작동합니다.

1. 가장자리를 무게별로 정렬합니다.
2. 가중치가 가장 낮은 에지를 선택하여 MST에 추가합니다.
3. 가중치가 가장 낮은 다음 에지를 선택하고 주기를 생성하지 않는 한 MST에 추가합니다.
4. 모든 정점이 연결될 때까지 3단계를 반복합니다.

## 프림의 알고리즘

Prim의 알고리즘은 단일 꼭짓점에서 시작하여 모든 꼭짓점이 연결될 때까지 가장자리를 추가하여 MST를 찾는 또 다른 탐욕적인 알고리즘입니다.

알고리즘은 다음과 같이 작동합니다.

1. 시작 정점을 선택합니다.
2. 시작 정점을 다른 정점에 연결하는 가중치가 가장 낮은 에지를 선택하고 MST에 추가합니다.
3. MST를 다른 정점에 연결하는 가중치가 가장 낮은 다음 가장자리를 선택하여 MST에 추가합니다.
4. 모든 정점이 연결될 때까지 3단계를 반복합니다.

## 코드 예시

다음은 C에서 Kruskal의 알고리즘을 간단하게 구현한 것입니다. 이 알고리즘은 연결 해제된 데이터 구조를 사용하여 어떤 정점이 동일한 연결 구성 요소에 있는지 추적합니다.

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

## 운동

1. MST를 찾는 Prim의 알고리즘을 구현합니다.

## 답변

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