---
title: [Lenguaje C] 034: Ordenar montón
description: 
published: true
date: 2023-02-13T14:33:07.492Z
tags: 
editor: markdown
dateCreated: 2023-02-13T14:33:05.786Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 034: Heap Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-034-heap-sort)
{.links-list}


# 034: Clasificación de montón

Heap sort es un algoritmo de clasificación basado en la comparación. La ordenación de pila se puede considerar como una ordenación de selección mejorada: al igual que ese algoritmo, divide su entrada en una región ordenada y otra no ordenada, y reduce iterativamente la región no ordenada extrayendo el elemento más grande y moviéndolo a la región ordenada. La mejora consiste en el uso de una estructura de datos de montón en lugar de una búsqueda de tiempo lineal para encontrar el máximo.

Heapsort fue inventado por J. W. J. Williams en 1964.[1] Heapsort es un algoritmo en el lugar, pero no es una ordenación estable.

## Algoritmo

Un montón binario es una estructura de datos de montón que toma la forma de un árbol binario. Los montones binarios son una forma común de implementar colas de prioridad.

El montón binario se define como un árbol binario con dos restricciones adicionales:

* Propiedad de forma: el árbol es un árbol binario completo; es decir, todos los niveles del árbol, excepto posiblemente el último (el más profundo), se llenan por completo y, si el último nivel del árbol no está completo, los nodos de ese nivel se llenan de izquierda a derecha.
* Propiedad del montón: cada nodo es mayor o igual que cada uno de sus hijos según un predicado de comparación definido para el montón.

La propiedad heap permite acceder rápidamente al nodo raíz; se garantiza que sea el elemento más grande (o más pequeño) del árbol.

El algoritmo tiene dos fases: construcción de montón y clasificación.

### Construcción de montones

La fase de construcción del montón comienza con una matriz desordenada de números y la transforma en un montón binario. La matriz se puede representar como un árbol binario, donde cada nodo corresponde a un elemento de la matriz, y los hijos de cada nodo son los elementos de la matriz que son más grandes (o más pequeños) que el elemento del nodo.

El primer paso es crear un montón a partir de la matriz. El algoritmo de construcción del montón es el siguiente:

1. Comience con un montón vacío.

2. Inserte cada elemento de la matriz en el montón, en cualquier orden.

3. Mientras el montón no esté vacío:

    a. Retire el elemento superior del montón.

    b. Inserte el elemento en la matriz ordenada.

4. Devuelva la matriz ordenada.

La complejidad temporal de la fase de construcción del montón es O(n), donde n es el número de elementos de la matriz.

### Clasificación

La fase de clasificación comienza con un montón binario y lo transforma en una matriz ordenada. El algoritmo de clasificación es el siguiente:

1. Mientras que el montón no está vacío:

    a. Retire el elemento superior del montón.

    b. Inserte el elemento en la matriz ordenada.

2. Devuelva la matriz ordenada.

La complejidad temporal de la fase de clasificación es O(nlog(n)), donde n es el número de elementos de la matriz. Esto se debe a que, en cada iteración del bucle while, se elimina el elemento superior del montón y se realiza la operación heapify. La operación heapify toma un tiempo O(log(n)), y hay n iteraciones del bucle while, por lo que la complejidad total del tiempo es O(nlog(n)).

## Ejemplo de código

La siguiente es una implementación de clasificación de heap en el lenguaje de programación C:

```c
#include <stdio.h>
#include <stdlib.h>

void heapify(int* array, int size, int i)
{
    int largest = i;
    int left = 2*i + 1;
    int right = 2*i + 2;

    if (left < size && array[left] > array[largest])
        largest = left;

    if (right < size && array[right] > array[largest])
        largest = right;

    if (largest != i)
    {
        int temp = array[i];
        array[i] = array[largest];
        array[largest] = temp;

        heapify(array, size, largest);
    }
}

void heap_sort(int* array, int size)
{
    for (int i = size / 2 - 1; i >= 0; i--)
        heapify(array, size, i);

    for (int i = size - 1; i >= 0; i--)
    {
        int temp = array[0];
        array[0] = array[i];
        array[i] = temp;

        heapify(array, i, 0);
    }
}

int main()
{
    int array[] = {3, 2, 1, 5, 4};
    int size = sizeof(array) / sizeof(array[0]);

    heap_sort(array, size);

    for (int i = 0; i < size; i++)
        printf("%d ", array[i]);
    printf("\n");

    return 0;
}
```

## Ejercicios

1. Implemente la operación heapify en el algoritmo de clasificación de almacenamiento dinámico.

2. Implemente el algoritmo de clasificación de almacenamiento dinámico.

3. Compare el tiempo de ejecución del algoritmo de clasificación de almacenamiento dinámico con el algoritmo de clasificación de selección.

## Respuestas

1. La operación heapify se puede implementar de la siguiente manera:

```c
void heapify(int* array, int size, int i)
{
    int largest = i;
    int left = 2*i + 1;
    int right = 2*i + 2;

    if (left < size && array[left] > array[largest])
        largest = left;

    if (right < size && array[right] > array[largest])
        largest = right;

    if (largest != i)
    {
        int temp = array[i];
        array[i] = array[largest];
        array[largest] = temp;

        heapify(array, size, largest);
    }
}
```

2. El algoritmo de clasificación de montón se puede implementar de la siguiente manera:

```c
void heap_sort(int* array, int size)
{
    for (int i = size / 2 - 1; i >= 0; i--)
        heapify(array, size, i);

    for (int i = size - 1; i >= 0; i--)
    {
        int temp = array[0];
        array[0] = array[i];
        array[i] = temp;

        heapify(array, i, 0);
    }
}
```

3. El tiempo de ejecución del algoritmo de clasificación de almacenamiento dinámico es O(nlog(n)), mientras que el tiempo de ejecución del algoritmo de clasificación de selección es O(n^2).