---
title: [Lenguaje C] 003: Complejidad espacial
description: 
published: true
date: 2023-02-12T14:32:26.254Z
tags: 
editor: markdown
dateCreated: 2023-02-12T14:32:19.506Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 003: Space Complexity***English** document is available*](/en/Knowledge-base/Algorithm/c-language-003-space-complexity)
{.links-list}



¿Qué es la Complejidad Espacial?

La complejidad del espacio es la cantidad de memoria requerida por un algoritmo para ejecutarse hasta su finalización. Tiene que ver con la cantidad de memoria que utiliza un algoritmo a medida que aumenta el tamaño de los datos de entrada.

Hay dos tipos de complejidad espacial: estática y dinámica. La complejidad del espacio estático es la cantidad de memoria requerida por un algoritmo para un tamaño de entrada específico. La complejidad del espacio dinámico es la cantidad de memoria requerida por un algoritmo a medida que aumenta el tamaño de entrada.

La complejidad del espacio estático suele ser fácil de calcular. Por ejemplo, si un algoritmo requiere una matriz de tamaño n, entonces la complejidad del espacio estático es O(n).

La complejidad del espacio dinámico suele ser más difícil de calcular. Por ejemplo, si un algoritmo requiere una matriz de tamaño ny el tamaño de la matriz aumenta en 1 cada vez que se ejecuta el algoritmo, entonces la complejidad del espacio dinámico es O(n).

Para calcular la complejidad espacial de un algoritmo, necesitamos saber lo siguiente:

- La cantidad de memoria requerida por el algoritmo para un tamaño de entrada específico
- El tamaño de los datos de entrada.
- La cantidad de memoria requerida por el algoritmo a medida que aumenta el tamaño de entrada

Por ejemplo, digamos que tenemos un algoritmo que requiere una matriz de tamaño n. Si el tamaño de la matriz aumenta en 1 cada vez que se ejecuta el algoritmo, entonces la complejidad del espacio dinámico es O(n).

Para calcular la complejidad espacial de un algoritmo, necesitamos saber lo siguiente:

- La cantidad de memoria requerida por el algoritmo para un tamaño de entrada específico
- El tamaño de los datos de entrada.
- La cantidad de memoria requerida por el algoritmo a medida que aumenta el tamaño de entrada

Por ejemplo, digamos que tenemos un algoritmo que requiere una matriz de tamaño n. Si el tamaño de la matriz aumenta en 1 cada vez que se ejecuta el algoritmo, entonces la complejidad del espacio dinámico es O(n).

Para calcular la complejidad espacial de un algoritmo, necesitamos saber lo siguiente:

- La cantidad de memoria requerida por el algoritmo para un tamaño de entrada específico
- El tamaño de los datos de entrada.
- La cantidad de memoria requerida por el algoritmo a medida que aumenta el tamaño de entrada

Por ejemplo, digamos que tenemos un algoritmo que requiere una matriz de tamaño n. Si el tamaño de la matriz aumenta en 1 cada vez que se ejecuta el algoritmo, entonces la complejidad del espacio dinámico es O(n).

Echemos un vistazo a un ejemplo.

Considere el siguiente algoritmo:

```
int findMax(int array[], int n) {
   int max = array[0];
   for (int i = 1; i < n; i++) {
      if (array[i] > max) {
         max = array[i];
      }
   }
   return max;
}
```

Este algoritmo tiene una complejidad de espacio estático de O(1), porque solo requiere una variable para almacenar el valor máximo.

Ahora, digamos que tenemos un algoritmo que requiere una matriz de tamaño n y el tamaño de la matriz aumenta en 1 cada vez que se ejecuta el algoritmo. En este caso, la complejidad del espacio dinámico es O(n).

Para calcular la complejidad espacial de un algoritmo, necesitamos saber lo siguiente:

- La cantidad de memoria requerida por el algoritmo para un tamaño de entrada específico
- El tamaño de los datos de entrada.
- La cantidad de memoria requerida por el algoritmo a medida que aumenta el tamaño de entrada

Por ejemplo, digamos que tenemos un algoritmo que requiere una matriz de tamaño n. Si el tamaño de la matriz aumenta en 1 cada vez que se ejecuta el algoritmo, entonces la complejidad del espacio dinámico es O(n).