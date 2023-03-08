---
title: [JavaScript] 030: ordenación por inserción
description: 
published: true
date: 2023-02-10T08:32:39.348Z
tags: 
editor: markdown
dateCreated: 2023-02-10T08:32:37.750Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 030: Insertion Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-030-insertion-sort)
{.links-list}


# Tipo de inserción

La ordenación por inserción es un algoritmo de ordenación que crea una matriz ordenada elemento a elemento. Es mucho menos eficiente en listas grandes que otros algoritmos de ordenación, como la ordenación rápida, la ordenación en montón o la ordenación por fusión. Sin embargo, la ordenación por inserción ofrece varias ventajas:

Implementación simple: Jon Bentley muestra una versión C de tres líneas en Perlas de programación[2]
Eficiente para conjuntos de datos (bastante) pequeños, al igual que otros algoritmos de clasificación cuadrática
Más eficiente que la ordenación por selección o la ordenación por burbuja
Estable; es decir, no cambia el orden relativo de los elementos con claves iguales
En su lugar; es decir, solo requiere una cantidad constante O(1) de espacio de memoria adicional
En línea; es decir, puede ordenar una lista a medida que la recibe

## El Algoritmo

La ordenación por inserción itera, consume un elemento de entrada en cada repetición y crea una lista de salida ordenada. En cada iteración, la ordenación por inserción elimina un elemento de los datos de entrada, encuentra la ubicación a la que pertenece dentro de la lista ordenada y lo inserta allí. Se repite hasta que no quedan elementos de entrada.

La clasificación generalmente se realiza en el lugar, iterando la matriz, aumentando la lista ordenada detrás de ella. En cada posición de la matriz, verifica el valor allí con el valor más grande en la lista ordenada (que está al lado, en la posición de la matriz anterior verificada). Si es más grande, deja el elemento en su lugar y pasa al siguiente. Si es más pequeño, encuentra la posición correcta dentro de la lista ordenada, desplaza todos los valores más grandes hacia arriba para hacer un espacio y los inserta en esa posición correcta.

## Complejidad

### Peor de los casos

La entrada del peor de los casos es una matriz ordenada en orden inverso. Para ordenar una matriz de tamaño n en orden inverso, la ordenación por inserción deberá realizar n^2 comparaciones e intercambios. Por lo tanto, la complejidad temporal para el peor de los casos es O(n^2).

### Mejor caso

La entrada del mejor de los casos es una matriz que ya está ordenada. En este caso, la ordenación por inserción hará comparaciones n-1 pero no intercambios. Por lo tanto, la complejidad temporal para el mejor de los casos es O(n).

## Ejemplos de código

### Javascript

```javascript
function insertionSort(array) {
  for(let i = 1; i < array.length; i++) {
    let current = array[i];
    let j = i - 1;
    while(j >= 0 && array[j] > current) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = current;
  }
  return array;
}
```

### Pitón

```python
def insertion_sort(array):
  for i in range(1, len(array)):
    current = array[i]
    j = i - 1
    while j >= 0 and array[j] > current:
      array[j + 1] = array[j]
      j -= 1
    array[j + 1] = current
  return array
```

## Ejercicios relacionados

- [ ] Ejercicio 1: Implementar ordenación por inserción
- [ ] Ejercicio 2: ordenar una matriz de cadenas mediante ordenación por inserción

## Respuestas

- [ ] Respuesta 1:

```javascript
function insertionSort(array) {
  for(let i = 1; i < array.length; i++) {
    let current = array[i];
    let j = i - 1;
    while(j >= 0 && array[j] > current) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = current;
  }
  return array;
}
```

- [ ] Respuesta 2:

```javascript
function insertionSort(array) {
  for(let i = 1; i < array.length; i++) {
    let current = array[i];
    let j = i - 1;
    while(j >= 0 && array[j] > current) {
      array[j + 1] = array[j];
      j--;
    }
    array[j + 1] = current;
  }
  return array;
}
```