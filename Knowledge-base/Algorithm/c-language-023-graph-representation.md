---
title: [C언어] 023: 그래프 표현
description: 
published: true
date: 2023-02-09T19:56:10.871Z
tags: 
editor: markdown
dateCreated: 2023-02-09T19:56:09.262Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [[C Language] 023: Graph Representation***English** document is available*](/en/Knowledge-base/Algorithm/c-language-023-graph-representation)
{.links-list}


# 023: 그래프 표현

그래프는 꼭짓점이라고도 하는 노드 모음과 가장자리라고도 하는 이들 사이의 연결입니다. 그래프는 응용 프로그램에 따라 여러 가지 방법으로 나타낼 수 있습니다.

그래프를 나타내는 한 가지 방법은 인접 행렬을 사용하는 것입니다. 인접 행렬은 각 요소가 0 또는 1인 2차원 배열로 해당 요소의 행과 열에 해당하는 두 정점 사이에 가장자리가 있는지 여부를 나타냅니다.

예를 들어 다음 그래프를 고려하십시오.

![그래프](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph.png)

이 그래프는 다음과 같은 인접 행렬로 나타낼 수 있습니다.

```
    A  B  C  D  E
A   0  1  1  0  0
B   1  0  1  0  0
C   1  1  0  1  0
D   0  0  1  0  1
E   0  0  0  1  0
```

인접 행렬에 대한 작업의 시간 복잡도는 'O(V^2)'이며, 여기서 'V'는 그래프의 정점 수입니다. 가장자리를 확인하기 위해 모든 행과 열을 반복해야 하기 때문입니다.

그래프를 나타내는 또 다른 방법은 인접 목록을 사용하는 것입니다. 인접 목록은 정점 목록이며 각 정점에는 연결된 정점 목록이 있습니다.

예를 들어, 다음 그래프:

![그래프](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph.png)

다음 인접 목록으로 나타낼 수 있습니다.

```
A: B, C
B: A, C
C: A, B, D
D: C, E
E: D
```

인접 리스트 연산의 시간 복잡도는 'O(V + E)'이며, 여기서 'V'는 정점의 개수이고 'E'는 에지의 개수입니다. 모든 꼭짓점과 모든 가장자리를 반복해야 하기 때문입니다.

어떤 표현이 더 나은지는 애플리케이션에 따라 다릅니다. 그래프가 밀도가 높으면(에지가 많다는 의미) 인접 행렬이 더 좋습니다. 그래프가 드문 경우(에지 수가 적다는 의미) 인접 목록이 더 좋습니다.

## 코드 예

다음은 C에서 인접 행렬을 사용하여 그래프를 나타내는 방법의 예입니다.

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

산출:

```
0 1 1 0 0 
1 0 1 0 0 
1 1 0 1 0 
0 0 1 0 1 
0 0 0 1 0
```

## 코드 예

다음은 C에서 인접 목록이 있는 그래프를 나타내는 방법의 예입니다.

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

산출:

```
0: 1 2 
1: 0 2 
2: 0 1 3 
3: 2 4 
4: 3
```

## 운동

1. 인접 행렬을 사용하여 다음 그래프를 나타냅니다.

![그래프1](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph1.png)

2. 인접 목록으로 다음 그래프를 나타냅니다.

![그래프2](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph2.png)

## 답변

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