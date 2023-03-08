---
title: [Lenguaje C] 001: Análisis asintótico
description: 
published: true
date: 2023-02-12T13:32:23.273Z
tags: 
editor: markdown
dateCreated: 2023-02-12T13:32:21.620Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 001: Asymptotic Analysis***English** document is available*](/en/Knowledge-base/Algorithm/c-language-001-asymptotic-analysis)
{.links-list}


# [Lenguaje C] 001: Análisis asintótico

El análisis asintótico es una herramienta matemática utilizada para comprender el comportamiento de una función a medida que la entrada crece. Nos permite hacer declaraciones sobre el tiempo de ejecución de un algoritmo sin tener que ejecutar el algoritmo en entradas grandes.

Hay dos tipos principales de análisis asintótico: análisis del peor de los casos y análisis del caso promedio.

## Análisis del peor de los casos

El análisis del peor de los casos es la forma más simple de análisis asintótico. Simplemente busca la peor entrada posible para un algoritmo y analiza el tiempo de ejecución en ese caso.

Por ejemplo, digamos que tenemos un algoritmo que ordena una matriz de n números. La entrada del peor de los casos para este algoritmo es una matriz que ya está ordenada en orden inverso. En este caso, el tiempo de ejecución del algoritmo sería O(n^2).

## Análisis de casos promedio

El análisis del caso promedio es un poco más complicado que el análisis del peor caso. Examina todas las entradas posibles de un algoritmo y calcula el tiempo de ejecución medio.

Para nuestro ejemplo de algoritmo de clasificación, el tiempo de ejecución de caso promedio sería O (n log n). Esto se debe a que hay n! posibles entradas al algoritmo, y el tiempo de ejecución para cada entrada es diferente. Para calcular el tiempo de ejecución promedio, simplemente tomamos la suma de todos los tiempos de ejecución y lo dividimos por n!.

## Notación asintótica

La notación asintótica es una notación matemática utilizada para describir el tiempo de ejecución de un algoritmo. Las tres notaciones más comunes son O(n), Ω(n) y Θ(n).

La notación O(n) se utiliza para describir el peor tiempo de ejecución de un algoritmo. Para nuestro ejemplo de algoritmo de clasificación, el peor tiempo de ejecución es O(n^2).

La notación Ω(n) se utiliza para describir el mejor tiempo de ejecución de un algoritmo. Para nuestro ejemplo de algoritmo de clasificación, el tiempo de ejecución del mejor caso es Ω(n log n).

La notación Θ(n) se utiliza para describir el tiempo de ejecución de caso promedio de un algoritmo. Para nuestro ejemplo de algoritmo de clasificación, el tiempo de ejecución de caso promedio es Θ(n log n).

## Ejercicios

1. Dado el siguiente código, ¿cuál es el tiempo de ejecución asintótico?

```C
int sum(int n) {
    int i;
    int s = 0;
    for (i = 1; i <= n; i++) {
        s = s + i;
    }
    return s;
}
```

El tiempo de ejecución asintótico de este código es O(n).

2. Dado el siguiente código, ¿cuál es el tiempo de ejecución asintótico?

```C
int sum(int n) {
    int i;
    int s = 0;
    for (i = 1; i <= n; i++) {
        s = s + i;
        if (s > 100) {
            break;
        }
    }
    return s;
}
```

El tiempo de ejecución asintótico de este código es O(n).