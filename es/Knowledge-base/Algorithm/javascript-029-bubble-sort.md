---
title: [JavaScript] 029: Clasificación de burbujas
description: 
published: true
date: 2023-02-10T07:32:37.190Z
tags: 
editor: markdown
dateCreated: 2023-02-10T07:32:30.684Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 029: Bubble Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-029-bubble-sort)
{.links-list}


# Ordenamiento de burbuja

Bubble sort es un algoritmo de clasificación simple que funciona recorriendo repetidamente la lista para ordenar, comparando cada par de elementos adyacentes e intercambiándolos si están en el orden incorrecto. El paso por la lista se repite hasta que no se necesitan intercambios, lo que indica que la lista está ordenada. El algoritmo recibe su nombre de la forma en que los elementos más pequeños o más grandes "burbujean" en la parte superior de la lista.

La clasificación de burbujas generalmente se considera el algoritmo de clasificación más simple. Sin embargo, también es relativamente ineficiente para listas grandes. Sin embargo, funciona bien para listas relativamente pequeñas.

## Concepto

La ordenación de burbujas funciona comparando cada elemento de la lista con el elemento al lado e intercambiándolos si están en el orden incorrecto. El proceso se repite hasta que se ordenan todos los elementos.

Por ejemplo, digamos que tenemos la siguiente lista:

```
[5, 1, 4, 2, 8]
```

Primero compararíamos los dos primeros elementos, `5` y `1`, y los intercambiaríamos porque `5` es mayor que `1`. La lista entonces se vería así:

```
[1, 5, 4, 2, 8]
```

Entonces compararíamos los siguientes dos elementos, `5` y `4`, y los dejaríamos en el mismo orden porque `5` no es mayor que `4`. La lista entonces se vería así:

```
[1, 5, 4, 2, 8]
```

Luego compararíamos los siguientes dos elementos, `4` y `2`, y los intercambiaríamos porque `4` es mayor que `2`. La lista entonces se vería así:

```
[1, 5, 2, 4, 8]
```

Finalmente, compararíamos los dos últimos elementos, `4` y `8`, y los dejaríamos en el mismo orden porque `4` no es mayor que `8`. La lista entonces se vería así:

```
[1, 5, 2, 4, 8]
```

Dado que no necesitábamos realizar ningún intercambio en la última pasada, podemos concluir que la lista ahora está ordenada.

## Ejemplo de código

Aquí hay una implementación simple de la ordenación de burbujas en JavaScript:

```javascript
function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        // swap
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```

## Complejidad

La complejidad temporal de la ordenación de burbujas es **O(n^2)** en el peor de los casos y **O(n)** en el mejor de los casos. El peor de los casos ocurre cuando la lista se ordena de forma inversa y el mejor de los casos ocurre cuando la lista ya está ordenada.

La complejidad del espacio de la ordenación de burbujas es **O(1)** porque solo se requiere un único espacio de memoria adicional.

## Cuándo usar la clasificación por burbujas

La ordenación por burbujas es una buena opción para ordenar listas relativamente pequeñas. También es una buena opción si necesita ordenar una lista que está casi ordenada.

## Cuándo no usar la clasificación por burbujas

La ordenación por burbujas no es una buena opción para ordenar listas grandes porque no es muy eficiente. Si necesita ordenar una lista grande, debe usar un algoritmo de ordenación diferente.

## Ejercicios

1. Implemente la ordenación de burbujas en el lenguaje de programación elegido.

2. Escriba una función que tome una lista y un número entero como argumentos y clasifique la lista usando la clasificación de burbujas. El entero debe especificar el número de veces que se debe ejecutar la ordenación.

3. Escriba una función que tome una lista como argumento y devuelva "verdadero" si la lista está ordenada y "falso" si no lo está.

4. Escribe una función que tome una lista y una función como argumentos y ordene la lista usando la función. La función debe tomar dos argumentos y devolver `-1` si el primer argumento es menor que el segundo, `0` si los dos argumentos son iguales y `1` si el primer argumento es mayor que el segundo.

## Respuestas

1.

```javascript
function bubbleSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (arr[j] > arr[j + 1]) {
        // swap
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```

2.

```javascript
function bubbleSortNTimes(arr, n) {
  for (let i = 0; i < n; i++) {
    bubbleSort(arr);
  }
  return arr;
}
```

3.

```javascript
function isSorted(arr) {
  for (let i = 0; i < arr.length - 1; i++) {
    if (arr[i] > arr[i + 1]) {
      return false;
    }
  }
  return true;
}
```

4.

```javascript
function bubbleSortWithComparator(arr, comparator) {
  for (let i = 0; i < arr.length; i++) {
    for (let j = 0; j < arr.length - i - 1; j++) {
      if (comparator(arr[j], arr[j + 1]) === 1) {
        // swap
        let temp = arr[j];
        arr[j] = arr[j + 1];
        arr[j + 1] = temp;
      }
    }
  }
  return arr;
}
```