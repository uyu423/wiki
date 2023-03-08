---
title: [JavaScript] 004: Divide y vencerás Algoritmos
description: 
published: true
date: 2023-02-09T06:32:32.024Z
tags: 
editor: markdown
dateCreated: 2023-02-09T06:32:30.427Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 004: Divide and Conquer Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/javascript-004-divide-and-conquer-algorithms)
{.links-list}


# Algoritmos divide y vencerás

Los algoritmos de divide y vencerás son una poderosa herramienta para resolver problemas. Al dividir un problema en partes más pequeñas, podemos resolverlo de manera más eficiente.

Hay muchos tipos diferentes de algoritmos de divide y vencerás, pero todos tienen una cosa en común: dividen el problema en subproblemas más pequeños, resuelven los subproblemas y luego combinan las soluciones de los subproblemas para resolver el problema original.

## Los basicos

Veamos un ejemplo sencillo. Digamos que tenemos el siguiente problema:

Dada una lista de números, encuentre el número más grande en la lista.

Podemos resolver este problema usando un algoritmo de divide y vencerás. Primero, dividimos el problema en subproblemas más pequeños. Podemos hacer esto mirando la primera mitad de la lista, luego la segunda mitad de la lista.

A continuación, resolvemos los subproblemas. En este caso, encontramos el número más grande en cada mitad de la lista.

Finalmente, combinamos las soluciones a los subproblemas para resolver el problema original. En este caso, comparamos los dos números más grandes que encontramos en cada mitad de la lista y devolvemos el mayor de los dos.

## Ejemplo de código

Ahora veamos un ejemplo más complejo. Digamos que tenemos el siguiente problema:

Dada una lista de números, encuentre la suma de todos los números en la lista.

Podemos resolver este problema usando un algoritmo de divide y vencerás. Primero, dividimos el problema en subproblemas más pequeños. Podemos hacer esto mirando la primera mitad de la lista, luego la segunda mitad de la lista.

A continuación, resolvemos los subproblemas. En este caso, encontramos la suma de todos los números en cada mitad de la lista.

Finalmente, combinamos las soluciones a los subproblemas para resolver el problema original. En este caso, sumamos las dos sumas que encontramos en cada mitad de la lista y devolvemos el resultado.

## Ejemplo de código

Aquí está el código para el algoritmo divide y vencerás que acabamos de ver:

```javascript
function findSum(list) {
  // Base case: if the list is empty, the sum is 0
  if (list.length === 0) {
    return 0;
  }
  // Divide the problem into smaller subproblems
  var mid = Math.floor(list.length / 2);
  var left = list.slice(0, mid);
  var right = list.slice(mid);
  // Solve the subproblems
  var leftSum = findSum(left);
  var rightSum = findSum(right);
  // Combine the solutions to the subproblems
  return leftSum + rightSum;
}
```

## Análisis de complejidad

La complejidad de tiempo de un algoritmo divide y vencerás depende del tamaño del problema, el número de subproblemas y la complejidad de tiempo para resolver los subproblemas.

En el peor de los casos, el tamaño del problema se reduce a la mitad en cada paso y el número de subproblemas se duplica. Si la complejidad temporal de resolver los subproblemas es constante, entonces la complejidad temporal del algoritmo divide y vencerás es O(n).

Sin embargo, si la complejidad temporal de resolver los subproblemas no es constante, la complejidad temporal del algoritmo divide y vencerás puede ser más compleja. Por ejemplo, si la complejidad temporal para resolver los subproblemas es O(n), entonces la complejidad temporal del algoritmo divide y vencerás es O(nlogn).

## Conclusión

Los algoritmos de divide y vencerás son una poderosa herramienta para resolver problemas. Al dividir un problema en partes más pequeñas, podemos resolverlo de manera más eficiente. Hay muchos tipos diferentes de algoritmos de divide y vencerás, pero todos tienen una cosa en común: dividen el problema en subproblemas más pequeños, resuelven los subproblemas y luego combinan las soluciones de los subproblemas para resolver el problema original.