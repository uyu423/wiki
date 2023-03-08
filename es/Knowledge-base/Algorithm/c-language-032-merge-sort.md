---
title: [Lenguaje C] 032: Clasificación por combinación
description: 
published: true
date: 2023-02-13T12:34:00.290Z
tags: 
editor: markdown
dateCreated: 2023-02-13T12:33:58.555Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 032: Merge Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-032-merge-sort)
{.links-list}


# 032: Clasificación por combinación

Merge sort es un algoritmo de clasificación que utiliza una estrategia de divide y vencerás. Es uno de los algoritmos de clasificación más eficientes con una complejidad de tiempo de O(n log n).

El algoritmo de ordenación por fusión funciona dividiendo la matriz en dos mitades, ordenando cada mitad y luego fusionando las dos mitades. El paso de fusión es la parte más importante del algoritmo de clasificación por fusión.

## ¿Cómo funciona el paso de fusión?

El paso de combinación funciona tomando dos matrices ordenadas y combinándolas en una única matriz ordenada. El paso de fusión es la parte más importante del algoritmo de clasificación por fusión.

Para fusionar dos matrices ordenadas, podemos usar un algoritmo simple llamado algoritmo de fusión. El algoritmo de fusión funciona tomando dos matrices ordenadas y combinándolas en una única matriz ordenada.

El algoritmo de fusión funciona comparando el primer elemento de cada matriz. Luego, el más pequeño de los dos elementos se agrega a la matriz fusionada. El algoritmo de combinación luego repite este proceso hasta que una de las matrices está vacía. Los elementos restantes de la otra matriz luego se agregan a la matriz fusionada.

## Ejemplo de código

Aquí hay una implementación simple del algoritmo de clasificación por fusión en C.

```c
#include <stdio.h>
#include <stdlib.h>
 
void merge(int *array, int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
 
    int L[n1], R[n2];
 
    for (i = 0; i < n1; i++)
        L[i] = array[l + i];
    for (j = 0; j < n2; j++)
        R[j] = array[m + 1+ j];
 
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            array[k] = L[i];
            i++;
        }
        else
        {
            array[k] = R[j];
            j++;
        }
        k++;
    }
 
    while (i < n1)
    {
        array[k] = L[i];
        i++;
        k++;
    }
 
    while (j < n2)
    {
        array[k] = R[j];
        j++;
        k++;
    }
}
 
void mergeSort(int *array, int l, int r)
{
    if (l < r)
    {
        int m = l+(r-l)/2;
 
        mergeSort(array, l, m);
        mergeSort(array, m+1, r);
 
        merge(array, l, m, r);
    }
}
 
int main()
{
    int array[] = {12, 11, 13, 5, 6, 7};
    int array_size = sizeof(array)/sizeof(array[0]);
 
    printf("Given array is \n");
    printArray(array, array_size);
 
    mergeSort(array, 0, array_size - 1);
 
    printf("\nSorted array is \n");
    printArray(array, array_size);
    return 0;
}
```

## Ejercicio

1. Implemente el algoritmo de clasificación por fusión en su lenguaje de programación favorito.

2. Utilice el algoritmo de clasificación por fusión para clasificar una matriz de enteros en orden ascendente.

3. Utilice el algoritmo de clasificación por combinación para clasificar una matriz de cadenas en orden alfabético.

## Respuestas

1.

```c
#include <stdio.h>
#include <stdlib.h>
 
void merge(int *array, int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
 
    int L[n1], R[n2];
 
    for (i = 0; i < n1; i++)
        L[i] = array[l + i];
    for (j = 0; j < n2; j++)
        R[j] = array[m + 1+ j];
 
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            array[k] = L[i];
            i++;
        }
        else
        {
            array[k] = R[j];
            j++;
        }
        k++;
    }
 
    while (i < n1)
    {
        array[k] = L[i];
        i++;
        k++;
    }
 
    while (j < n2)
    {
        array[k] = R[j];
        j++;
        k++;
    }
}
 
void mergeSort(int *array, int l, int r)
{
    if (l < r)
    {
        int m = l+(r-l)/2;
 
        mergeSort(array, l, m);
        mergeSort(array, m+1, r);
 
        merge(array, l, m, r);
    }
}
 
int main()
{
    int array[] = {12, 11, 13, 5, 6, 7};
    int array_size = sizeof(array)/sizeof(array[0]);
 
    printf("Given array is \n");
    printArray(array, array_size);
 
    mergeSort(array, 0, array_size - 1);
 
    printf("\nSorted array is \n");
    printArray(array, array_size);
    return 0;
}
```

2.

```c
#include <stdio.h>
#include <stdlib.h>
 
void merge(int *array, int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
 
    int L[n1], R[n2];
 
    for (i = 0; i < n1; i++)
        L[i] = array[l + i];
    for (j = 0; j < n2; j++)
        R[j] = array[m + 1+ j];
 
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (L[i] <= R[j])
        {
            array[k] = L[i];
            i++;
        }
        else
        {
            array[k] = R[j];
            j++;
        }
        k++;
    }
 
    while (i < n1)
    {
        array[k] = L[i];
        i++;
        k++;
    }
 
    while (j < n2)
    {
        array[k] = R[j];
        j++;
        k++;
    }
}
 
void mergeSort(int *array, int l, int r)
{
    if (l < r)
    {
        int m = l+(r-l)/2;
 
        mergeSort(array, l, m);
        mergeSort(array, m+1, r);
 
        merge(array, l, m, r);
    }
}
 
int main()
{
    int array[] = {12, 11, 13, 5, 6, 7};
    int array_size = sizeof(array)/sizeof(array[0]);
 
    printf("Given array is \n");
    printArray(array, array_size);
 
    mergeSort(array, 0, array_size - 1);
 
    printf("\nSorted array is \n");
    printArray(array, array_size);
    return 0;
}
```

3.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
 
void merge(char **array, int l, int m, int r)
{
    int i, j, k;
    int n1 = m - l + 1;
    int n2 =  r - m;
 
    char **L = malloc(sizeof(char*)*n1);
    char **R = malloc(sizeof(char*)*n2);
 
    for (i = 0; i < n1; i++)
        L[i] = array[l + i];
    for (j = 0; j < n2; j++)
        R[j] = array[m + 1+ j];
 
    i = 0;
    j = 0;
    k = l;
    while (i < n1 && j < n2)
    {
        if (strcmp(L[i], R[j]) <= 0)
        {
            array[k] = L[i];
            i++;
        }
        else
        {
            array[k] = R[j];
            j++;
        }
        k++;
    }
 
    while (i < n1)
    {
        array[k] = L[i];
        i++;
        k++;
    }
 
    while (j < n2)
    {
        array[k] = R[j];
        j++;
        k++;
    }
 
    free(L);
    free(R);
}
 
void mergeSort(char **array, int l, int r)
{
    if (l < r)
    {
        int m = l+(r-l)/2;
 
        mergeSort(array, l, m);
        mergeSort(array, m+1, r);
 
        merge(array, l, m, r);
    }
}
 
int main()
{
    char *array[] = {"c", "a", "e", "b", "d"};
    int array_size = sizeof(array)/sizeof(array[0]);
 
    printf("Given array is \n");
    printArray(array, array_size);
 
    mergeSort(array, 0, array_size - 1);
 
    printf("\nSorted array is \n");
    printArray(array, array_size);
    return 0;
}
```