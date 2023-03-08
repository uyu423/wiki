---
title: [C语言]023：图形表示
description: 
published: true
date: 2023-02-09T19:56:10.887Z
tags: 
editor: markdown
dateCreated: 2023-02-09T19:56:09.267Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [[C Language] 023: Graph Representation***English** document is available*](/en/Knowledge-base/Algorithm/c-language-023-graph-representation)
{.links-list}


# 023：图形表示

图是节点（也称为顶点）和它们之间的连接（也称为边）的集合。图形可以用多种方式表示，具体取决于应用程序。

表示图的一种方法是使用邻接矩阵。邻接矩阵是一个二维数组，其中每个元素为0或1，表示该元素的行和列对应的两个顶点之间是否有边。

例如，考虑下图：

![图表](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph.png)

该图可以由以下邻接矩阵表示：

```
    A  B  C  D  E
A   0  1  1  0  0
B   1  0  1  0  0
C   1  1  0  1  0
D   0  0  1  0  1
E   0  0  0  1  0
```

邻接矩阵运算的时间复杂度为“O(V^2)”，其中“V”是图中的顶点数。这是因为我们必须遍历每一行和每一列来检查边缘。

表示图的另一种方法是使用邻接表。邻接表是一个顶点列表，其中每个顶点都有一个它所连接的顶点列表。

例如，下图：

![图表](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph.png)

可以用下面的邻接表来表示：

```
A: B, C
B: A, C
C: A, B, D
D: C, E
E: D
```

邻接表操作的时间复杂度为 O(V + E)，其中 V 是顶点数，E 是边数。这是因为我们必须遍历所有顶点和所有边。

哪种表示更好取决于应用程序。如果图很密集，意味着有很多边，那么邻接矩阵会更好。如果图是稀疏的，意味着边很少，那么邻接表更好。

## 代码示例

以下是如何在 C 中用邻接矩阵表示图的示例：

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

输出：

```
0 1 1 0 0 
1 0 1 0 0 
1 1 0 1 0 
0 0 1 0 1 
0 0 0 1 0
```

## 代码示例

以下是如何在 C 中用邻接表表示图的示例：

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

输出：

```
0: 1 2 
1: 0 2 
2: 0 1 3 
3: 2 4 
4: 3
```

## 练习

1. 用邻接矩阵表示下图：

![graph1](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph1.png)

2. 用邻接表表示下图：

![graph2](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph2.png)

## 答案

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