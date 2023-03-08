---
title: [Aprendizaje en JavaScript] 002: Complejidad del tiempo
description: 
published: true
date: 2023-02-09T04:33:10.827Z
tags: 
editor: markdown
dateCreated: 2023-02-09T04:33:09.141Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[Learning in JavaScript] 002: Time Complexity***English** document is available*](/en/Knowledge-base/Algorithm/learning-in-javascript-002-time-complexity)
{.links-list}


# Aprendizaje en JavaScript: 002 Complejidad del tiempo

En informática, la complejidad temporal de un algoritmo es la cantidad de tiempo que tarda en ejecutarse, medida en el número de operaciones realizadas. La complejidad del tiempo generalmente se expresa como una función del tamaño de entrada, n. Por ejemplo, un algoritmo que tarda unos segundos en ejecutarse en una entrada de tamaño n tendría una complejidad de tiempo de O(n^2).

Hay dos tipos de complejidad de tiempo: el peor de los casos y el caso promedio. La complejidad del tiempo en el peor de los casos es la cantidad de tiempo que tarda el algoritmo en ejecutarse en la entrada del peor de los casos, que es la entrada de tamaño n que tarda más tiempo en ejecutarse. La complejidad del tiempo de caso promedio es la cantidad de tiempo que tarda el algoritmo en ejecutarse en las entradas de caso promedio, que son entradas de tamaño n que tardan una cantidad de tiempo promedio en ejecutarse.

La complejidad temporal de un algoritmo puede verse afectada por la elección de estructuras de datos, el orden en que se realizan las operaciones y el patrón de diseño algorítmico utilizado.

## Estructuras de datos

La elección de estructuras de datos puede afectar la complejidad temporal de un algoritmo. Por ejemplo, considere el problema de buscar un elemento en una matriz. Si la matriz no está ordenada, la complejidad temporal del algoritmo de búsqueda en el peor de los casos es O(n), porque se debe buscar en toda la matriz. Sin embargo, si se ordena la matriz, la complejidad temporal del algoritmo de búsqueda en el peor de los casos es O (log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

## Orden de operaciones

El orden en que se realizan las operaciones también puede afectar la complejidad temporal de un algoritmo. Por ejemplo, considere el problema de ordenar una matriz. La complejidad de tiempo del peor de los casos del algoritmo de clasificación es O (n log n), porque la matriz debe dividirse en n log n particiones, y cada partición debe clasificarse. Sin embargo, si la matriz ya está ordenada, la complejidad temporal del algoritmo de clasificación en el peor de los casos es O(n), porque no es necesario dividir la matriz en particiones y cada elemento se puede comparar con el siguiente elemento de la matriz.

## Patrones de diseño algorítmico

Hay una serie de patrones de diseño algorítmico que se pueden utilizar para mejorar la complejidad temporal de un algoritmo. Estos patrones de diseño incluyen:

- Divide y vencerás: este patrón de diseño se usa para dividir el problema en subproblemas más pequeños, resolver los subproblemas y combinar las soluciones a los subproblemas para resolver el problema original.

- Greedy: este patrón de diseño se utiliza para hacer una elección localmente óptima en cada paso con la esperanza de encontrar un óptimo global.

- Programación dinámica: este patrón de diseño se utiliza para dividir el problema en subproblemas más pequeños, resolver los subproblemas y almacenar las soluciones a los subproblemas en una tabla. Las soluciones a los subproblemas se pueden reutilizar para resolver el problema original.

- Fuerza bruta: Este patrón de diseño se utiliza para probar todas las posibles soluciones al problema y seleccionar la mejor.

## Ejemplos de código

Aquí hay un ejemplo de código de un algoritmo de clasificación con una complejidad de tiempo de O (n log n):

```javascript
function sort(array) {
  if (array.length <= 1) {
    return array;
  }

  const pivot = array[0];
  const left = [];
  const right = [];

  for (let i = 1; i < array.length; i++) {
    const element = array[i];

    if (element <= pivot) {
      left.push(element);
    } else {
      right.push(element);
    }
  }

  return [...sort(left), pivot, ...sort(right)];
}
```

Y aquí hay un ejemplo de código de un algoritmo de clasificación con una complejidad de tiempo de O(n):

```javascript
function sort(array) {
  for (let i = 0; i < array.length - 1; i++) {
    for (let j = i + 1; j < array.length; j++) {
      if (array[i] > array[j]) {
        const temp = array[i];
        array[i] = array[j];
        array[j] = temp;
      }
    }
  }

  return array;
}
```

## Ejercicios

1. Escriba una función que tome una matriz de enteros y devuelva la suma de los elementos de la matriz. ¿Cuál es la complejidad temporal de la función?

2. Escribe una función que tome una matriz de enteros y devuelva el entero más grande de la matriz. ¿Cuál es la complejidad temporal de la función?

3. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva el índice del entero objetivo en la matriz. ¿Cuál es la complejidad temporal de la función?

4. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?

5. Escriba una función que tome una matriz de enteros y devuelva la matriz ordenada en orden ascendente. ¿Cuál es la complejidad temporal de la función?

6. Escriba una función que tome una matriz de enteros y un entero de destino y devuelva el índice del entero de destino en la matriz, o -1 si el entero de destino no está en la matriz. ¿Cuál es la complejidad temporal de la función?

7. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?

8. Escriba una función que tome una matriz de enteros y devuelva la matriz ordenada en orden ascendente. ¿Cuál es la complejidad temporal de la función?

9. Escriba una función que tome una matriz de enteros y un entero de destino y devuelva el índice del entero de destino en la matriz, o -1 si el entero de destino no está en la matriz. ¿Cuál es la complejidad temporal de la función?

10. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?

11. Escriba una función que tome una matriz de enteros y un entero de destino y devuelva el índice del entero de destino en la matriz, o -1 si el entero de destino no está en la matriz. ¿Cuál es la complejidad temporal de la función?

12. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?

13. Escriba una función que tome una matriz de enteros y devuelva la matriz ordenada en orden ascendente. ¿Cuál es la complejidad temporal de la función?

14. Escriba una función que tome una matriz de enteros y un entero de destino y devuelva el índice del entero de destino en la matriz, o -1 si el entero de destino no está en la matriz. ¿Cuál es la complejidad temporal de la función?

15. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?

16. Escriba una función que tome una matriz de enteros y un entero de destino y devuelva el índice del entero de destino en la matriz, o -1 si el entero de destino no está en la matriz. ¿Cuál es la complejidad temporal de la función?

17. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?

18. Escriba una función que tome una matriz de enteros y un entero de destino y devuelva el índice del entero de destino en la matriz, o -1 si el entero de destino no está en la matriz. ¿Cuál es la complejidad temporal de la función?

19. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?

20. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva el índice del entero objetivo en la matriz, o -1 si el entero objetivo no está en la matriz. ¿Cuál es la complejidad temporal de la función?

21. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?

22. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva el índice del entero objetivo en la matriz, o -1 si el entero objetivo no está en la matriz. ¿Cuál es la complejidad temporal de la función?

23. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?

24. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva el índice del entero objetivo en la matriz, o -1 si el entero objetivo no está en la matriz. ¿Cuál es la complejidad temporal de la función?

25. Escriba una función que tome una matriz de enteros y un entero objetivo y devuelva verdadero si el entero objetivo está en la matriz y falso si no lo está. ¿Cuál es la complejidad temporal de la función?

## Respuestas

1. La complejidad temporal de la función es O(n), porque se debe recorrer todo el arreglo para calcular la suma.

2. La complejidad temporal de la función es O(n), porque se debe recorrer todo el arreglo para encontrar el entero más grande.

3. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

4. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

5. La complejidad temporal de la función es O(n log n), porque la matriz debe dividirse en n log n particiones, y cada partición debe ordenarse.

6. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

7. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

8. La complejidad temporal de la función es O(n log n), porque la matriz debe dividirse en n log n particiones, y cada partición debe ordenarse.

9. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

10. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

11. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

12. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

13. La complejidad temporal de la función es O(n log n), porque el arreglo debe dividirse en n log n particiones, y cada partición debe ordenarse.

14. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

15. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

16. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

17. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

18. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

19. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

20. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

21. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

22. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

23. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

24. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.

25. La complejidad temporal de la función es O(log n), porque la matriz se puede buscar mediante una búsqueda binaria, que reduce a la mitad el espacio de búsqueda en cada paso.