---
title: [Lenguaje C] 044: Árbol K-D
description: 
published: true
date: 2023-02-13T22:32:20.068Z
tags: 
editor: markdown
dateCreated: 2023-02-13T22:32:18.235Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 044: K-D Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-044-k-d-tree)
{.links-list}


# 044: Árbol K-D

Un árbol k-d (abreviatura de árbol k-dimensional) es una estructura de datos de partición espacial para organizar puntos en un espacio k-dimensional. Los árboles k-d son una estructura de datos útil para varias aplicaciones, como búsquedas que involucran una clave de búsqueda multidimensional (por ejemplo, búsquedas de rango y búsquedas de vecinos más cercanos).

Un árbol k-d es un árbol binario en el que cada nodo es un punto k-dimensional. El árbol se construye de forma recursiva, de arriba hacia abajo, dividiendo los puntos en dos conjuntos a lo largo de un hiperplano que pasa por el punto con la mayor varianza. Este proceso se repite recursivamente en cada conjunto, hasta alcanzar el nivel de granularidad deseado.

## Concepto

El árbol k-d es una generalización de la estructura de datos del árbol de búsqueda binaria. En un árbol de búsqueda binario, los puntos se dividen a lo largo de una sola dimensión (por ejemplo, el eje x), lo que da como resultado un espacio bidimensional. En un árbol k-d, los puntos se dividen en múltiples dimensiones, lo que da como resultado un espacio k-dimensional.

La partición de puntos en un árbol k-d se realiza de forma recursiva, de arriba hacia abajo. El árbol se construye comenzando con un nodo raíz que contiene todos los puntos. Luego, el nodo raíz se divide a lo largo de la dimensión con la varianza más grande y los puntos se dividen en dos conjuntos: un conjunto que contiene todos los puntos que son menores que el punto de pivote y el otro conjunto que contiene todos los puntos que son mayores que o igual al punto de pivote.

Luego, este proceso se repite recursivamente en cada uno de los dos conjuntos, hasta alcanzar el nivel deseado de granularidad.

## Ejemplo de código

Aquí hay un ejemplo simple de cómo construir un árbol k-d en pseudocódigo:

```
function kdtree(points, depth)
   if points is empty
      return

   select a pivot point, p, using some heuristic (e.g. median of points)
   partition points into two sets, S1 and S2, using p as the pivot
   create a new node, n, with p as the key
   n.left = kdtree(S1, depth + 1)
   n.right = kdtree(S2, depth + 1)
   return n
```

## Ejercicios relacionados

- [ ] Implemente un árbol k-d en su lenguaje de programación favorito.
- [ ] Dado un conjunto de puntos, construye un árbol k-d y consulta sobre el vecino más cercano de un punto dado.
- [ ] Dado un conjunto de puntos, construye un árbol k-d y consulta todos los puntos dentro de un rango dado.