---
title: [JavaScript] 033: Clasificación rápida
description: 
published: true
date: 2023-02-10T11:32:29.325Z
tags: 
editor: markdown
dateCreated: 2023-02-10T11:32:27.719Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 033: Quick Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-033-quick-sort)
{.links-list}


# JavaScript 033: Clasificación rápida

El algoritmo de clasificación rápida es un algoritmo de clasificación que clasifica una matriz dividiendo la matriz en dos subarreglos y luego ordenando los subarreglos de forma recursiva. El algoritmo recibe su nombre de la forma en que ordena la matriz: divide la matriz en dos subarreglos, luego ordena los subarreglos "rápidamente" aplicando recursivamente el algoritmo de clasificación rápida.

El algoritmo de clasificación rápida generalmente se implementa mediante recursividad. El caso base de la recursividad es cuando la matriz a ordenar tiene una longitud de 1 o 0. En este caso, la matriz ya está ordenada. De lo contrario, la matriz se divide en dos subarreglos y el algoritmo de clasificación rápida se aplica recursivamente a cada subarreglo.

El algoritmo de clasificación rápida tiene una complejidad de tiempo de O (n log n) en promedio y una complejidad de espacio de O (log n). Sin embargo, la complejidad de tiempo del peor de los casos del algoritmo de clasificación rápida es O (n ^ 2).

## Ejemplo de código

El siguiente es un ejemplo de código del algoritmo de clasificación rápida en JavaScript:

```javascript
function quickSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const pivot = arr[arr.length - 1];
  const left = [];
  const right = [];

  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  return [...quickSort(left), pivot, ...quickSort(right)];
}
```

## Ejercicio

El siguiente es un ejercicio para evaluar su comprensión del algoritmo de clasificación rápida:

```javascript
// Write a function that sorts an array using the quick sort algorithm.

function quickSort(arr) {
  // Your code here
}
```

## Código de respuesta

El siguiente es el código de respuesta para el ejercicio:

```javascript
function quickSort(arr) {
  if (arr.length <= 1) {
    return arr;
  }

  const pivot = arr[arr.length - 1];
  const left = [];
  const right = [];

  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  return [...quickSort(left), pivot, ...quickSort(right)];
}
```

## Comentario

El algoritmo de clasificación rápida es un algoritmo de clasificación muy eficiente con una complejidad de tiempo de O (n log n) en promedio. Sin embargo, la complejidad de tiempo del peor de los casos del algoritmo de clasificación rápida es O (n ^ 2). Por lo tanto, el algoritmo de clasificación rápida no es el mejor algoritmo de clasificación para usar en todos los casos.