---
title: [Lenguaje C] 004: Divide y vencerás Algoritmos
description: 
published: true
date: 2023-02-12T15:32:19.134Z
tags: 
editor: markdown
dateCreated: 2023-02-12T15:32:17.491Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 004: Divide and Conquer Algorithms***English** document is available*](/en/Knowledge-base/Algorithm/c-language-004-divide-and-conquer-algorithms)
{.links-list}


# Lenguaje C] 004: Divide y vencerás Algoritmos

Los algoritmos de divide y vencerás son una poderosa herramienta para resolver problemas. Al dividir un problema en subproblemas más pequeños, podemos resolver el problema de manera más eficiente.

Hay muchos algoritmos de divide y vencerás, pero nos centraremos en dos de los más populares: el ordenamiento por combinación y el ordenamiento rápido.

## El tipo de combinación

El ordenamiento por fusión es un algoritmo recursivo que funciona dividiendo un problema en subproblemas más pequeños y luego combinando las soluciones a esos subproblemas.

La ordenación por combinación funciona dividiendo una matriz por la mitad, ordenando cada mitad y luego fusionando las dos mitades. El paso de fusión es la clave para la ordenación por fusión. Para fusionar las dos mitades, necesitamos comparar los elementos de cada mitad y luego ponerlos en el orden correcto.

Aquí hay una implementación de pseudocódigo del tipo de fusión:

```
def merge_sort(array):
    if len(array) <= 1:
        return array
    
    # split the array in half
    mid = len(array) // 2
    left = array[:mid]
    right = array[mid:]
    
    # sort each half
    left = merge_sort(left)
    right = merge_sort(right)
    
    # merge the halves together
    return merge(left, right)
    
def merge(left, right):
    result = []
    
    while len(left) > 0 and len(right) > 0:
        if left[0] <= right[0]:
            result.append(left[0])
            left = left[1:]
        else:
            result.append(right[0])
            right = right[1:]
            
    # either left or right may have elements left
    while len(left) > 0:
        result.append(left[0])
        left = left[1:]
        
    while len(right) > 0:
        result.append(right[0])
        right = right[1:]
        
    return result
```

La ordenación por fusión es un poderoso algoritmo de ordenación con una complejidad de tiempo de O(n log n). Sin embargo, no es el algoritmo de clasificación más rápido.

## La ordenación rápida

La ordenación rápida es otro algoritmo popular de divide y vencerás. La ordenación rápida funciona seleccionando un elemento pivote y luego dividiendo la matriz alrededor del pivote. Los elementos menores que el pivote se colocan en una matriz y los elementos mayores que el pivote se colocan en otra matriz. La ordenación rápida luego ordena recursivamente las dos matrices.

Aquí hay una implementación de pseudocódigo del tipo rápido:

```
def quick_sort(array):
    if len(array) <= 1:
        return array
    
    # select a pivot element
    pivot = array[len(array) // 2]
    
    # partition the array around the pivot
    left = []
    right = []
    
    for element in array:
        if element < pivot:
            left.append(element)
        elif element > pivot:
            right.append(element)
        else:
            # element is equal to the pivot, so we can leave it in the array
            pass
    
    # sort the left and right arrays
    left = quick_sort(left)
    right = quick_sort(right)
    
    # merge the arrays back together
    return left + [pivot] + right
```

La ordenación rápida es un algoritmo de ordenación rápida con una complejidad de tiempo de O(n log n).

## Conclusión

Los algoritmos de divide y vencerás son una poderosa herramienta para resolver problemas. La ordenación por combinación y la ordenación rápida son dos de los algoritmos de divide y vencerás más populares.