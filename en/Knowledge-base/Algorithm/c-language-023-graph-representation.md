---
title: [C Language] 023: Graph Representation
description: 
published: true
date: 2023-02-09T19:56:15.714Z
tags: 
editor: markdown
dateCreated: 2023-02-09T19:56:09.270Z
---

- [[Lenguaje C] 023: Representación gráfica***Spanish** document is available*](/es/Knowledge-base/Algorithm/c-language-023-graph-representation)
{.links-list}
- [[C语言]023：图形表示***Chinese Simplified** document is available*](/zh/Knowledge-base/Algorithm/c-language-023-graph-representation)
{.links-list}
- [[C언어] 023: 그래프 표현***Korean** document is available*](/ko/Knowledge-base/Algorithm/c-language-023-graph-representation)
{.links-list}


# 023: Graph Representation

A graph is a collection of nodes, also called vertices, and the connections between them, also called edges. Graphs can be represented in several ways, depending on the application.

One way to represent a graph is with an adjacency matrix. An adjacency matrix is a two-dimensional array in which each element is a 0 or 1 to indicate whether there is an edge between the two vertices corresponding to the row and column of that element.

For example, consider the following graph:

![graph](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph.png)

This graph can be represented by the following adjacency matrix:

```
    A  B  C  D  E
A   0  1  1  0  0
B   1  0  1  0  0
C   1  1  0  1  0
D   0  0  1  0  1
E   0  0  0  1  0
```

The time complexity of operations on adjacency matrices is `O(V^2)`, where `V` is the number of vertices in the graph. This is because we have to loop through every row and column to check for edges.

Another way to represent a graph is with an adjacency list. An adjacency list is a list of vertices, where each vertex has a list of the vertices it is connected to.

For example, the following graph:

![graph](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph.png)

Can be represented by the following adjacency list:

```
A: B, C
B: A, C
C: A, B, D
D: C, E
E: D
```

The time complexity of operations on adjacency lists is `O(V + E)`, where `V` is the number of vertices and `E` is the number of edges. This is because we have to loop through all of the vertices and all of the edges.

Which representation is better depends on the application. If the graph is dense, meaning there are a lot of edges, then an adjacency matrix is better. If the graph is sparse, meaning there are few edges, then an adjacency list is better.

## Code Example

The following is an example of how to represent a graph with an adjacency matrix in C:

```C
#include <stdio.h>

int main()
{
    int i, j;
    int graph[5][5] =
    {
        {0, 1, 1, 0, 0},
        {1, 0, 1, 0, 0},
        {1, 1, 0, 1, 0},
        {0, 0, 1, 0, 1},
        {0, 0, 0, 1, 0}
    };

    for (i = 0; i < 5; i++)
    {
        for (j = 0; j < 5; j++)
        {
            printf("%d ", graph[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```

Output:

```
0 1 1 0 0 
1 0 1 0 0 
1 1 0 1 0 
0 0 1 0 1 
0 0 0 1 0
```

## Code Example

The following is an example of how to represent a graph with an adjacency list in C:

```C
#include <stdio.h>
#include <stdlib.h>

typedef struct node
{
    int vertex;
    struct node *next;
} node;

node *adj[5];

void addEdge(int v1, int v2)
{
    node *newNode1 = (node*)malloc(sizeof(node));
    newNode1->vertex = v1;
    newNode1->next = adj[v2];
    adj[v2] = newNode1;

    node *newNode2 = (node*)malloc(sizeof(node));
    newNode2->vertex = v2;
    newNode2->next = adj[v1];
    adj[v1] = newNode2;
}

void printGraph()
{
    int i;
    for (i = 0; i < 5; i++)
    {
        node *tmp = adj[i];
        printf("%d: ", i);
        while (tmp)
        {
            printf("%d ", tmp->vertex);
            tmp = tmp->next;
        }
        printf("\n");
    }
}

int main()
{
    int i;
    for (i = 0; i < 5; i++)
    {
        adj[i] = NULL;
    }

    addEdge(0, 1);
    addEdge(0, 2);
    addEdge(1, 2);
    addEdge(2, 3);
    addEdge(3, 4);

    printGraph();

    return 0;
}
```

Output:

```
0: 1 2 
1: 0 2 
2: 0 1 3 
3: 2 4 
4: 3
```

## Exercises

1. Represent the following graph with an adjacency matrix:

![graph1](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph1.png)

2. Represent the following graph with an adjacency list:

![graph2](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph2.png)

## Answers

1. 

```
    A  B  C  D  E  F  G  H  I
A   0  1  1  0  0  0  0  0  0
B   1  0  0  1  0  0  0  0  0
C   1  0  0  0  1  0  0  0  0
D   0  1  0  0  1  0  0  0  0
E   0  0  1  1  0  0  0  0  0
F   0  0  0  0  0  0  1  1  0
G   0  0  0  0  0  1  0  1  0
H   0  0  0  0  0  1  1  0  1
I   0  0  0  0  0  0  0  1  0
```

2. 

```
A: B, C, D, E
B: A, F, G
C: A, E, H
D: A, E, I
E: A, C, D
F: B
G: B
H: C, I
I: D, H
```