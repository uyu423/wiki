---
title: [JavaScript] 031: Clasificación de selección
description: 
published: true
date: 2023-02-10T09:32:32.013Z
tags: 
editor: markdown
dateCreated: 2023-02-10T09:32:30.419Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 031: Selection Sort***English** document is available*](/en/Knowledge-base/Algorithm/javascript-031-selection-sort)
{.links-list}


# JavaScript 031: Clasificación de selección

La ordenación por selección es un algoritmo de ordenación, específicamente una ordenación por comparación en el lugar. Tiene una complejidad de tiempo O(n2), lo que lo hace ineficiente en listas grandes y, en general, funciona peor que la ordenación por inserción similar. La ordenación por selección se destaca por su simplicidad y tiene ventajas de rendimiento sobre algoritmos más complicados en ciertas situaciones, particularmente donde la memoria auxiliar es limitada.

El algoritmo divide la lista de entrada en dos partes: la sublista de elementos ya ordenados, que se construye de izquierda a derecha al frente (izquierda) de la lista, y la sublista de elementos que quedan por ordenar que ocupan el resto de la lista. lista. Inicialmente, la sublista ordenada está vacía y la sublista no ordenada es la lista de entrada completa. El algoritmo procede encontrando el elemento más pequeño (o el más grande, según el orden de clasificación) en la sublista sin clasificar, intercambiándolo con el elemento sin clasificar más a la izquierda (poniéndolo en orden) y moviendo los límites de la sublista un elemento a la derecha. .

## Ejemplos de código

```javascript
function selectionSort(arr) {
  for (let i = 0; i < arr.length; i++) {
    let min = i;
    for (let j = i + 1; j < arr.length; j++) {
      if (arr[j] < arr[min]) {
        min = j;
      }
    }
    if (i !== min) {
      [arr[i], arr[min]] = [arr[min], arr[i]];
    }
  }
  return arr;
}
```

## Selección Ordenar Pseudocódigo

```
procedure selectionSort( A : list of sortable items )
   n = length(A)
   for i = 1 to n - 1
   /* set current element as minimum*/
      minIndex = i    
   /* check the element to be minimum */
 
      for j = i+1 to n      
         if A[j] < A[minIndex]   
            minIndex = j;
      end if
   end for
   /* swap the minimum element with the current element*/
   if indexMin != i  then
      swap A[minIndex] with A[i]
   end if
   end for
end procedure
```

## Visualización de clasificación de selección

![Visualización de clasificación de selección](https://upload.wikimedia.org/wikipedia/commons/9/94/Selection-Sort-Animation.gif)

## Complejidad de clasificación de selección

La ordenación por selección tiene una complejidad temporal de O(n2). Esto significa que, en el peor de los casos, el algoritmo tomará n2 pasos para ordenar una lista de n elementos.

## Ejercicios relacionados

- [Ejercicio 1](https://repl.it/@ezekielelin/Selection-Sort# index.js): Implementar ordenación por selección en JavaScript
- [Ejercicio 2](https://repl.it/@ezekielelin/Selection-Sort-Optimized# index.js): Optimizar la ordenación de selección para datos casi ordenados

## Respuestas

- [Respuesta 1](https://repl.it/@ezekielelin/Selection-Sort-Answer# index.js)
- [Respuesta 2](https://repl.it/@ezekielelin/Selection-Sort-Optimized-Answer# index.js)