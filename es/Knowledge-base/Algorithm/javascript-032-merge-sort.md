---
title: [JavaScript] 032: Clasificación por combinación
description: 
published: true
date: 2023-02-10T10:32:29.108Z
tags: 
editor: markdown
dateCreated: 2023-02-10T10:32:27.485Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 032: Merge Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-032-merge-sort)
{.links-list}


# JavaScript 032: Clasificación por combinación

Merge sort es un algoritmo de clasificación que utiliza una estrategia de divide y vencerás. Es un algoritmo recursivo que funciona dividiendo una matriz en subarreglos más pequeños, luego ordenando y fusionando esos subarreglos nuevamente.

El algoritmo de clasificación por fusión se puede escribir en pseudocódigo de la siguiente manera:

```
function mergeSort(array)
  if array.length <= 1
    return array
  end
 
  middle = array.length / 2
  left = array.slice(0, middle)
  right = array.slice(middle)
 
  return merge(
    mergeSort(left),
    mergeSort(right)
  )
end
 
function merge(left, right)
  result = []
 
  while left.length && right.length
    if left[0] <= right[0]
      result.push(left.shift())
    else
      result.push(right.shift())
    end
  end
 
  return result.concat(left, right)
end
```

El algoritmo de ordenación por fusión tiene una complejidad de tiempo de O(n log n). Esto se debe a que la matriz se divide por la mitad en cada paso y hay pasos O (log n). Cada paso también implica una operación de fusión, que tiene una complejidad de tiempo de O(n).

La complejidad espacial del algoritmo de clasificación por fusión es O(n). Esto se debe a que, en cada paso, se crea un nuevo arreglo para almacenar el subarreglo ordenado.

## Ejemplo de código

Aquí hay un ejemplo del algoritmo de clasificación por fusión escrito en JavaScript:

```javascript
function mergeSort(array) {
  if (array.length <= 1) {
    return array;
  }
 
  const middle = Math.floor(array.length / 2);
  const left = array.slice(0, middle);
  const right = array.slice(middle);
 
  return merge(
    mergeSort(left),
    mergeSort(right)
  );
}
 
function merge(left, right) {
  const result = [];
 
  while (left.length && right.length) {
    if (left[0] <= right[0]) {
      result.push(left.shift());
    } else {
      result.push(right.shift());
    }
  }
 
  return result.concat(left, right);
}
 
const array = [5, 3, 2, 1, 4];
console.log(mergeSort(array)); // [1, 2, 3, 4, 5]
```

## Explicación

El algoritmo de clasificación por combinación funciona dividiendo una matriz en subarreglos más pequeños, luego ordenando y fusionando esos subarreglos nuevamente.

El algoritmo comienza verificando si la matriz está vacía o tiene solo un elemento. Si es así, devuelve la matriz.

De lo contrario, la matriz se divide por la mitad en cada paso y hay pasos O (log n). Cada paso también implica una operación de fusión, que tiene una complejidad de tiempo de O(n).

La complejidad espacial del algoritmo de clasificación por fusión es O(n). Esto se debe a que, en cada paso, se crea un nuevo arreglo para almacenar el subarreglo ordenado.

## Análisis de complejidad

La complejidad temporal del algoritmo de clasificación por fusión es O(n log n). Esto se debe a que la matriz se divide por la mitad en cada paso y hay pasos O (log n). Cada paso también implica una operación de fusión, que tiene una complejidad de tiempo de O(n).

La complejidad espacial del algoritmo de clasificación por fusión es O(n). Esto se debe a que, en cada paso, se crea un nuevo arreglo para almacenar el subarreglo ordenado.