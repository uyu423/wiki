---
title: [JavaScript] 005: Algoritmos de programación dinámica
description: 
published: true
date: 2023-02-09T07:32:23.908Z
tags: 
editor: markdown
dateCreated: 2023-02-09T07:32:22.351Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 005: Dynamic Programming Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/javascript-005-dynamic-programming-algorithms)
{.links-list}


# JavaScript 005: Algoritmos de Programación Dinámica

Los algoritmos de programación dinámica son una herramienta poderosa para resolver problemas que se pueden dividir en subproblemas. Al resolver los subproblemas y almacenar los resultados, el problema general se puede resolver mucho más rápido.

Hay dos tipos principales de algoritmos de programación dinámica: de arriba hacia abajo y de abajo hacia arriba.

## De arriba hacia abajo

Los algoritmos de arriba hacia abajo comienzan en la parte superior del problema y lo dividen en subproblemas más pequeños. Luego resuelven los subproblemas y almacenan los resultados. Cuando ya se ha resuelto un subproblema, se utiliza el resultado almacenado en lugar de resolver el subproblema de nuevo.

Los algoritmos de arriba hacia abajo suelen ser más fáciles de entender, pero pueden ser más lentos y usar más memoria que los algoritmos de abajo hacia arriba.

## De abajo hacia arriba

Los algoritmos ascendentes comienzan en la parte inferior del problema y avanzan hacia arriba. Primero resuelven los subproblemas y luego usan los resultados para resolver el problema general.

Los algoritmos de abajo hacia arriba pueden ser más rápidos y usar menos memoria que los algoritmos de arriba hacia abajo, pero pueden ser más difíciles de entender.

## Ejemplo de código

Aquí hay un ejemplo simple de un algoritmo de programación dinámica de arriba hacia abajo escrito en JavaScript.

```javascript
function fibonacci(n) {
  // Base case: Fib(0) = 0, Fib(1) = 1
  if (n <= 1) {
    return n;
  }
 
  // Recursive case: Fib(n) = Fib(n-1) + Fib(n-2)
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```

## Ejercicio

Intente implementar un algoritmo de programación dinámica de abajo hacia arriba para la secuencia de Fibonacci.

## Código de respuesta

```javascript
function fibonacci(n) {
  // Base case: Fib(0) = 0, Fib(1) = 1
  if (n <= 1) {
    return n;
  }
 
  // Recursive case: Fib(n) = Fib(n-1) + Fib(n-2)
  return fibonacci(n - 1) + fibonacci(n - 2);
}
```

## Comentario

Los algoritmos de programación dinámica de arriba hacia abajo y de abajo hacia arriba son herramientas poderosas que pueden ayudarlo a resolver problemas de manera más eficiente. En muchos casos, un enfoque de abajo hacia arriba será más eficiente, pero un enfoque de arriba hacia abajo puede ser más fácil de entender.