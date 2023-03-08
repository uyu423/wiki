---
title: [JavaScript] 034: Ordenar montón
description: 
published: true
date: 2023-02-10T12:32:35.101Z
tags: 
editor: markdown
dateCreated: 2023-02-10T12:32:33.491Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 034: Heap Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-034-heap-sort)
{.links-list}


# Clasificación de montón

Heap sort es un algoritmo de clasificación basado en la comparación. Heap sort puede considerarse como una ordenación por selección mejorada: al igual que la ordenación por selección, heapsort divide su entrada en una región ordenada y otra sin ordenar, y reduce iterativamente la región sin ordenar extrayendo el elemento más grande de ella e insertándolo en la región ordenada. La mejora consiste en el uso de una estructura de datos de montón en lugar de una búsqueda de tiempo lineal para encontrar el máximo.

Heapsort es un algoritmo en el lugar, pero no es una ordenación estable.

## Algoritmo

Un montón es una estructura de datos similar a un árbol en la que los nodos secundarios tienen un orden de clasificación con respecto al nodo principal. Hay dos tipos de montones: montón mínimo y montón máximo. En un montón mínimo, el valor del nodo raíz es menor o igual que los valores de los nodos secundarios. En un montón máximo, el valor del nodo raíz es mayor o igual que los valores de los nodos secundarios.

El algoritmo de ordenación del montón se puede dividir en dos partes:

1. La primera parte consiste en construir un montón a partir de la matriz de entrada. Este paso también se conoce como heapify.
2. La segunda parte implica extraer los elementos del montón uno por uno e insertarlos en la matriz ordenada.

La primera parte se puede hacer usando un montón mínimo o un montón máximo. En este artículo, usaremos un montón máximo.

El algoritmo heapify comienza en el nodo raíz y se mueve hacia abajo en el árbol, comparando el valor del nodo actual con los valores de sus nodos secundarios. Si el valor del nodo actual es menor que el valor de un nodo secundario, los dos nodos se intercambian. Este proceso se repite hasta que el nodo actual sea mayor o igual que sus dos nodos secundarios (o hasta que se alcance la parte inferior del árbol).

La segunda parte del algoritmo implica extraer repetidamente el elemento máximo del montón e insertarlo en la matriz ordenada. Esto se hace intercambiando el nodo raíz del montón con el último elemento de la matriz y luego acumulando el árbol. Este proceso se repite hasta que el montón está vacío.

## Complejidad

La complejidad de tiempo de heapify es O(log n) y la complejidad de tiempo del algoritmo general de clasificación de montón es O(n log n).

## Ejemplo de código

La siguiente es una implementación en C++ del algoritmo de ordenación en montón.

```C++
#include <iostream>
#include <vector>

using namespace std;

void heapify(vector<int>& A, int n, int i)
{
    int largest = i;
    int l = 2*i + 1;
    int r = 2*i + 2;

    if (l < n && A[l] > A[largest])
        largest = l;

    if (r < n && A[r] > A[largest])
        largest = r;

    if (largest != i)
    {
        swap(A[i], A[largest]);
        heapify(A, n, largest);
    }
}

void heapSort(vector<int>& A, int n)
{
    for (int i = n / 2 - 1; i >= 0; i--)
        heapify(A, n, i);

    for (int i=n-1; i>=0; i--)
    {
        swap(A[0], A[i]);
        heapify(A, i, 0);
    }
}

int main()
{
    vector<int> A = {4, 10, 3, 5, 1};
    int n = A.size();

    heapSort(A, n);

    for (int i=0; i<n; ++i)
        cout << A[i] << " ";

    return 0;
}
```

## Ejercicios

1. Implemente los algoritmos heapify y heapSort en el lenguaje de programación elegido.

2. Use el algoritmo heapify para construir un montón máximo a partir de la siguiente matriz:

```
[4, 10, 3, 5, 1]
```

3. Use el algoritmo heapSort para ordenar la siguiente matriz:

```
[4, 10, 3, 5, 1]
```

4. ¿Cuál es la complejidad temporal de los algoritmos heapify y heapSort?

5. ¿Cuál es la complejidad espacial de los algoritmos heapify y heapSort?