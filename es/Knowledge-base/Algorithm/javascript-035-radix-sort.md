---
title: [JavaScript] 035: Clasificación Radix
description: 
published: true
date: 2023-02-10T13:32:23.515Z
tags: 
editor: markdown
dateCreated: 2023-02-10T13:32:21.944Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 035: Radix Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-035-radix-sort)
{.links-list}


# Clasificación Radix

Radix sort es un algoritmo de clasificación que clasifica números procesando los dígitos uno a la vez. Es un algoritmo de clasificación no comparativo con complejidad asintótica O(kn), lo que lo hace adecuado para clasificar números grandes.

## Algoritmo

La idea básica detrás de la ordenación radix es tomar un número y ordenarlo según sus dígitos. Por ejemplo, dado el número `42`, podemos ordenarlo según el primer dígito (`4`), luego el segundo dígito (`2`).

Para hacer esto, primero necesitamos encontrar el dígito más grande en el número. En nuestro ejemplo, el dígito más grande es `4`. Luego podemos crear una matriz con 10 cubos, uno para cada dígito de `0` a `9`.

A continuación, revisamos cada número en la matriz de entrada y lo colocamos en el cubo correcto según su primer dígito. En nuestro ejemplo, `42` se colocaría en el depósito `4`.

Una vez que hayamos colocado todos los números en sus respectivos cubos, podemos revisar los cubos y volver a colocar los números en la matriz original en orden.

## Ejemplo de código

```javascript
function radixSort(arr) {
  // find the largest digit in the array
  let max = Math.max(...arr);

  // create an array of 10 buckets, one for each digit from 0 to 9
  let buckets = Array.from({ length: 10 }, () => []);

  // go through each number in the input array and place it in the
  // correct bucket based on its first digit
  for (let num of arr) {
    let digit = Math.floor(num / 10);
    buckets[digit].push(num);
  }

  // go through the buckets and put the numbers back into the original
  // array in sorted order
  let i = 0;
  for (let bucket of buckets) {
    for (let num of bucket) {
      arr[i++] = num;
    }
  }

  return arr;
}
```

## Complejidad

Radix sort tiene una complejidad de tiempo de O(kn), donde k es el número de dígitos en el número más grande y n es el tamaño de la matriz de entrada.