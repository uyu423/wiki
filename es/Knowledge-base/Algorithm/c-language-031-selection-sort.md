---
title: [Lenguaje C] 031: Clasificación de selección
description: 
published: true
date: 2023-02-13T11:32:12.453Z
tags: 
editor: markdown
dateCreated: 2023-02-13T11:32:10.886Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 031: Selection Sort***English** document is available*](/en/Knowledge-base/Algorithm/c-language-031-selection-sort)
{.links-list}


# 031: Clasificación de selección

El algoritmo de ordenación por selección ordena una matriz encontrando repetidamente el elemento mínimo (considerando el orden ascendente) de la parte no ordenada y colocándolo al principio. El algoritmo mantiene dos subarreglos en un arreglo dado.

1) El subarreglo que ya está ordenado.
2) Subarreglo restante que no está ordenado.

En cada iteración del ordenamiento por selección, el elemento mínimo (considerando el orden ascendente) del subarreglo no ordenado se selecciona y se mueve al subarreglo ordenado.

## pseudocódigo

```
procedure selectionSort( A : array of items )
   n = length(A)
   for i = 0 to n-1 do
      /* find the minimum element in the unsorted array */
       
      /* swap the found minimum element with the first element */
     
   done
```

## Complejidad

### Complejidad del tiempo

Mejor caso: Ω(n^2)

Caso promedio: Θ(n^2)

Peor caso: O(n^2)

### Complejidad espacial

Peor caso: O(1)