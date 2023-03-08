---
title: [JavaScript] 023: Representación gráfica
description: 
published: true
date: 2023-02-10T01:32:29.782Z
tags: 
editor: markdown
dateCreated: 2023-02-10T01:32:28.216Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 023: Graph Representation***English** document is available*](/en/Knowledge-base/Algorithm/javascript-023-graph-representation)
{.links-list}


# Representación gráfica

Un gráfico se puede representar de muchas maneras, pero hay dos formas principales: listas de adyacencia y matrices de adyacencia. En esta publicación, veremos estos dos métodos y veremos sus ventajas y desventajas.

## Listas de adyacencia

Una lista de adyacencia es simplemente una lista de todos los vértices adyacentes a un vértice dado. Por ejemplo, considere el siguiente gráfico:

![texto alternativo](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/adjacency_list_1.png)

La lista de adyacencia para este gráfico sería:

```
A: B, C
B: A, C, D
C: A, B, D
D: B, C
```

Como puede ver, se enumera cada vértice, junto con todos los vértices a los que está adyacente.

Las listas de adyacencia tienen la ventaja de ser simples y fáciles de implementar. También usan menos espacio que las matrices de adyacencia, ya que solo necesitamos almacenar los bordes de cada vértice, no todos los bordes del gráfico completo.

La desventaja de las listas de adyacencia es que pueden ser más lentas de consultar. Por ejemplo, si queremos saber si hay una arista entre los vértices A y D, tendríamos que mirar la lista de adyacencia de A y D para ver si alguno de ellos enumera al otro. Por el contrario, con una matriz de adyacencia, podemos mirar la entrada de A y D y ver si es distinta de cero.

## Matrices de adyacencia

Una matriz de adyacencia es una matriz (arreglo 2D) donde cada fila y columna representa un vértice, y el valor en cada intersección de fila/columna es el peso del borde entre esos dos vértices. Por ejemplo, considere el siguiente gráfico:

![texto alternativo](https://cdncontribute.geeksforgeeks.org/wp-content/uploads/adjacency_matrix_1.png)

La matriz de adyacencia para este gráfico sería:

```
  A B C D
A 0 1 1 0
B 1 0 1 1
C 1 1 0 1
D 0 1 1 0
```

Como puede ver, cada fila y columna representa un vértice, y el valor en cada intersección de fila/columna es el peso del borde entre esos dos vértices. Si no hay borde entre dos vértices, el peso es 0.

Las matrices de adyacencia tienen la ventaja de ser muy rápidas de consultar. Por ejemplo, si queremos saber si hay una arista entre los vértices A y D, podemos mirar la entrada de A y D y ver si es distinta de cero. Por el contrario, con una lista de adyacencia, necesitaríamos mirar la lista de adyacencia tanto para A como para D para ver si alguno de ellos enumera al otro.

La desventaja de las matrices de adyacencia es que pueden usar más espacio que las listas de adyacencia. Por ejemplo, en nuestro gráfico anterior, solo hay 16 aristas, pero la matriz de adyacencia tiene 16 * 4 = 64 entradas. En general, una matriz de adyacencia utilizará el espacio O(V^2), donde V es el número de vértices.

## ¿Cuál debo usar?

Las listas de adyacencia generalmente se usan cuando el gráfico es escaso, lo que significa que no hay muchos bordes. Las matrices de adyacencia generalmente se usan cuando el gráfico es denso, lo que significa que hay muchos bordes.

No hay una respuesta correcta o incorrecta y, a menudo, es posible utilizar cualquiera de las dos representaciones. En general, las listas de adyacencia son más fáciles de implementar, pero las matrices de adyacencia son más rápidas de consultar.