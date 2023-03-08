---
title: [Lenguaje C] 030: Clasificación por inserción
description: 
published: true
date: 2023-02-13T00:17:32.980Z
tags: 
editor: markdown
dateCreated: 2023-02-13T00:17:31.315Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 030: Insertion Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-030-insertion-sort)
{.links-list}


# 030: Clasificación por inserción

La clasificación por inserción es un algoritmo de clasificación simple que funciona tomando elementos nuevos uno a la vez e insertándolos en la posición correcta en la lista ya ordenada. Es mucho menos eficiente en listas grandes que los algoritmos más avanzados, como la ordenación rápida, la ordenación en montón o la ordenación por fusión. Sin embargo, es muy eficiente para listas pequeñas y, a menudo, se usa como parte de algoritmos más sofisticados. También es una clasificación estable, lo que significa que conserva el orden de los elementos con claves iguales.

Aquí hay un ejemplo simple de ordenación por inserción en acción. Comenzamos con una lista desordenada de números:

```
5, 2, 4, 6, 1, 3
```

Para ordenar esta lista, primero tomamos el segundo elemento (`2`) y lo insertamos en la posición correcta en la lista ya ordenada (`5, 2, 4, 6, 1, 3`). Luego tomamos el tercer elemento (`4`) y lo insertamos en la posición correcta en la lista ya ordenada (`2, 4, 5, 6, 1, 3`). Seguimos así hasta ordenar toda la lista:

```
1, 2, 3, 4, 5, 6
```

El algoritmo de clasificación por inserción se puede implementar en unas pocas líneas de código. Aquí hay una implementación simple en C:

```C
void insertion_sort(int array[], int n)
{
    int i, j, temp;
    
    for (i = 1; i < n; i++) {
        temp = array[i];
        j = i-1;
        while (j >= 0 && array[j] > temp) {
            array[j+1] = array[j];
            j--;
        }
        array[j+1] = temp;
    }
}
```

Esta implementación ordena la matriz en el lugar, lo que significa que ordena la matriz en el lugar sin crear una nueva matriz.

Para probar esta implementación, podemos crear una matriz de números aleatorios y ordenarlos usando el algoritmo de ordenación por inserción. Luego podemos imprimir la matriz ordenada para ver si realmente está ordenada:

```C
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

void insertion_sort(int array[], int n);

int main(void)
{
    int i, n = 10;
    int array[n];
    
    srand(time(NULL));
    
    for (i = 0; i < n; i++) {
        array[i] = rand() % 100;
    }
    
    insertion_sort(array, n);
    
    for (i = 0; i < n; i++) {
        printf("%d ", array[i]);
    }
    printf("\n");
    
    return 0;
}
```

Ejecutar este código nos da el siguiente resultado:

```
2 4 5 8 12 23 37 38 39 45 
```

Podemos ver que la matriz está ordenada.

## Complejidad

La complejidad de tiempo en el peor de los casos del ordenamiento por inserción es `O(n^2)`. Esto ocurre cuando la matriz se ordena en orden inverso. La complejidad de tiempo del mejor caso es `O(n)` y ocurre cuando la matriz ya está ordenada.

La ordenación por inserción es una ordenación estable, lo que significa que conserva el orden de los elementos con claves iguales. También es una ordenación en el lugar, lo que significa que ordena la matriz en el lugar sin crear una nueva matriz.

## Ejercicios

1. Implemente el algoritmo de clasificación por inserción en su lenguaje de programación favorito.

2. Modifique el algoritmo de ordenación por inserción para ordenar una lista enlazada individualmente.

3. Modifique el algoritmo de ordenación por inserción para ordenar una matriz de cadenas.