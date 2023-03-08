---
title: [Lenguaje C] 033: Clasificación rápida
description: 
published: true
date: 2023-02-13T13:32:35.930Z
tags: 
editor: markdown
dateCreated: 2023-02-13T13:32:34.306Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 033: Quick Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-033-quick-sort)
{.links-list}


# 033: Clasificación Rápida

La clasificación rápida es un algoritmo de clasificación que clasifica una matriz dividiendo la matriz en dos subarreglos y luego ordenando los subarreglos de forma recursiva.

El algoritmo funciona seleccionando un elemento pivote de la matriz, luego dividiendo la matriz alrededor del pivote de modo que todos los elementos menores que el pivote estén antes y todos los elementos mayores que el pivote estén después. Luego, los dos subarreglos se ordenan recursivamente.

La ordenación rápida es un algoritmo de divide y vencerás, lo que significa que divide el problema en subproblemas más pequeños que luego resuelve recursivamente.

La complejidad temporal de la ordenación rápida depende de la implementación, pero el peor de los casos es O(n^2) y el mejor de los casos es O(n log n).

## Ejemplo de código

Aquí hay un algoritmo de clasificación rápida implementado en C.

```C
void quick_sort(int *arr, int left, int right)
{
    int i, j, pivot, tmp;

    if (left < right) {
        pivot = left;
        i = left;
        j = right;

        while (i < j) {
            while (arr[i] <= arr[pivot] && i <= right) {
                i++;
            }
            while (arr[j] > arr[pivot]) {
                j--;
            }
            if (i <= j) {
                tmp = arr[i];
                arr[i] = arr[j];
                arr[j] = tmp;
                i++;
                j--;
            }
        }

        tmp = arr[pivot];
        arr[pivot] = arr[j];
        arr[j] = tmp;

        quick_sort(arr, left, j - 1);
        quick_sort(arr, j + 1, right);
    }
}
```

## Explicación

El algoritmo de clasificación rápida funciona seleccionando un elemento pivote de la matriz, luego dividiendo la matriz alrededor del pivote de modo que todos los elementos menores que el pivote estén antes y todos los elementos mayores que el pivote estén después. Luego, los dos subarreglos se ordenan recursivamente.

La complejidad temporal de la ordenación rápida depende de la implementación, pero el peor de los casos es O(n^2) y el mejor de los casos es O(n log n).

## Ejercicios relacionados

1. Implemente la ordenación rápida en su lenguaje de programación favorito.

2. Compare el tiempo de ejecución de la ordenación rápida y la ordenación combinada en varias entradas.