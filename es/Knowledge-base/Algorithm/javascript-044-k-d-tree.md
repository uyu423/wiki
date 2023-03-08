---
title: [JavaScript] 044: Árbol K-D
description: 
published: true
date: 2023-02-10T22:32:18.439Z
tags: 
editor: markdown
dateCreated: 2023-02-10T22:32:16.870Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 044: K-D Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-044-k-d-tree)
{.links-list}


# JavaScript 044: Árbol K-D

Un árbol K-D (abreviatura de árbol k-dimensional) es una estructura de datos de partición espacial para organizar puntos en un espacio k-dimensional. Los árboles K-D son una estructura de datos útil para varias aplicaciones, como búsquedas que involucran una clave de búsqueda multidimensional (por ejemplo, búsquedas de rango y búsquedas de vecinos más cercanos).

Un árbol K-D es un árbol binario en el que cada nodo interno representa un punto en el espacio k-dimensional. El árbol se construye dividiendo recursivamente los puntos del espacio en dos mitades a lo largo del valor medio de una de las k dimensiones. Este proceso se repite recursivamente hasta que todos los puntos estén contenidos en las hojas del árbol.

## Construcción

El árbol K-D se puede construir en tiempo O(n log n), donde n es el número de puntos en el espacio.

El algoritmo de construcción comienza seleccionando una dimensión (dimensión k) al azar. Luego, los puntos se ordenan a lo largo de esta dimensión y el punto mediano se elige como la raíz del árbol. Los puntos a la izquierda de la mediana se dividen recursivamente en un subárbol izquierdo y los puntos a la derecha de la mediana se dividen recursivamente en un subárbol derecho. Este proceso se repite hasta que todos los puntos estén contenidos en las hojas del árbol.

## Buscar

Dado un punto de consulta q, el vecino más cercano de q se puede encontrar en el tiempo O (log n) al atravesar el árbol. La búsqueda comienza en la raíz del árbol y procede de la siguiente manera:

- Si q es menor que el valor en el nodo actual, busque en el subárbol izquierdo.
- Si q es mayor que el valor en el nodo actual, busque el subárbol derecho.
- Si q es igual al valor en el nodo actual, devuelve el nodo.

La búsqueda termina cuando se alcanza un nodo hoja. En este punto, el vecino más cercano de q es el punto del nodo hoja más cercano a q.

## Aplicaciones

Los árboles K-D se usan comúnmente para la búsqueda del vecino más cercano, un tipo de búsqueda que se usa para encontrar el punto en un espacio que está más cerca de un punto de consulta determinado. La búsqueda del vecino más cercano se usa a menudo en aplicaciones como reconocimiento de patrones y gráficos por computadora.

Los árboles K-D también se usan para la búsqueda de rango, un tipo de búsqueda que se usa para encontrar todos los puntos en un espacio que se encuentran dentro de una distancia determinada de un punto de consulta. La búsqueda de rango se usa a menudo en aplicaciones como la visualización científica y los sistemas de información geográfica.