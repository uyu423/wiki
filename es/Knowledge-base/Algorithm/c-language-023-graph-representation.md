---
title: [Lenguaje C] 023: Representación gráfica
description: 
published: true
date: 2023-02-09T19:56:10.990Z
tags: 
editor: markdown
dateCreated: 2023-02-09T19:56:09.312Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 023: Graph Representation***English** document is available*](/en/Knowledge-base/Algorithm/c-language-023-graph-representation)
{.links-list}


# 023: Representación gráfica

Un grafo es una colección de nodos, también llamados vértices, y las conexiones entre ellos, también llamadas aristas. Los gráficos se pueden representar de varias formas, dependiendo de la aplicación.

Una forma de representar un gráfico es con una matriz de adyacencia. Una matriz de adyacencia es una matriz bidimensional en la que cada elemento es un 0 o un 1 para indicar si hay un borde entre los dos vértices correspondientes a la fila y la columna de ese elemento.

Por ejemplo, considere el siguiente gráfico:

![gráfico](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph.png)

Este gráfico se puede representar mediante la siguiente matriz de adyacencia:

```
    A  B  C  D  E
A   0  1  1  0  0
B   1  0  1  0  0
C   1  1  0  1  0
D   0  0  1  0  1
E   0  0  0  1  0
```

La complejidad temporal de las operaciones en matrices de adyacencia es `O(V^2)`, donde `V` es el número de vértices en el gráfico. Esto se debe a que tenemos que recorrer cada fila y columna para verificar los bordes.

Otra forma de representar un gráfico es con una lista de adyacencia. Una lista de adyacencia es una lista de vértices, donde cada vértice tiene una lista de los vértices a los que está conectado.

Por ejemplo, el siguiente gráfico:

![gráfico](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph.png)

Se puede representar mediante la siguiente lista de adyacencia:

```
A: B, C
B: A, C
C: A, B, D
D: C, E
E: D
```

La complejidad temporal de las operaciones en las listas de adyacencia es `O(V + E)`, donde `V` es el número de vértices y `E` es el número de aristas. Esto se debe a que tenemos que recorrer todos los vértices y todos los bordes.

Qué representación es mejor depende de la aplicación. Si el gráfico es denso, lo que significa que hay muchos bordes, entonces es mejor una matriz de adyacencia. Si el gráfico es escaso, lo que significa que hay pocos bordes, entonces es mejor una lista de adyacencia.

## Ejemplo de código

El siguiente es un ejemplo de cómo representar un gráfico con una matriz de adyacencia en C:

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

Producción:

```
0 1 1 0 0 
1 0 1 0 0 
1 1 0 1 0 
0 0 1 0 1 
0 0 0 1 0
```

## Ejemplo de código

El siguiente es un ejemplo de cómo representar un gráfico con una lista de adyacencia en C:

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

Producción:

```
0: 1 2 
1: 0 2 
2: 0 1 3 
3: 2 4 
4: 3
```

## Ejercicios

1. Representa el siguiente gráfico con una matriz de adyacencia:

![graph1](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph1.png)

2. Representa el siguiente gráfico con una lista de adyacencia:

![graph2](https://github.com/Bergel/Coursera-Data-Structures-Algorithms/raw/master/1.%20Fundamentals/week2/graph2.png)

## Respuestas

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