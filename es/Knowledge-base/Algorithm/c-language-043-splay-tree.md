---
title: [Lenguaje C] 043: árbol de reproducción
description: 
published: true
date: 2023-02-10T07:55:35.713Z
tags: 
editor: markdown
dateCreated: 2023-02-10T07:55:34.092Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 043: Splay Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-043-splay-tree)
{.links-list}


# Árbol de juego

Un árbol splay es un árbol de búsqueda binaria autoequilibrado con la propiedad adicional de que los elementos a los que se ha accedido recientemente se vuelven a acceder rápidamente. Realiza operaciones básicas como inserción, búsqueda y eliminación en tiempo logarítmico.

Un árbol splay es un árbol binario que satisface el siguiente invariante:

* El árbol está vacío o
* El árbol consta de un nodo raíz y dos subárboles, izquierdo y derecho, y
* El valor del nodo raíz es mayor que todos los valores en el subárbol izquierdo, y
* El valor del nodo raíz es menor que todos los valores del subárbol derecho.

La siguiente figura muestra un ejemplo de un árbol splay:

![Árbol de reproducción](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Splay_tree_animation.gif/250px-Splay_tree_animation.gif)

Los árboles de distribución se autoequilibran, lo que significa que el árbol se ajusta a sí mismo para que los elementos a los que se accedió más recientemente se vuelvan a acceder rápidamente. Esto se hace moviendo el elemento accedido a la raíz del árbol.

Las siguientes operaciones son compatibles con los árboles de distribución:

* Inserción
* Buscar
* Eliminación

Todas estas operaciones se realizan en tiempo logarítmico.

## Inserción

La inserción en un árbol de distribución es similar a la inserción en un árbol de búsqueda binaria. Primero, encontramos la posición correcta para el nuevo elemento recorriendo el árbol. Luego, insertamos el nuevo elemento en el árbol.

Sin embargo, después de la inserción, debemos distribuir el nuevo elemento hasta la raíz. Esto se hace mediante una serie de rotaciones de árboles.

La siguiente figura muestra un ejemplo de inserción en un árbol splay:

![Inserción en un Splay Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b0/Splay-tree-insert.gif/250px-Splay-tree-insert.gif)

## Buscar

La búsqueda en un árbol de distribución es similar a la búsqueda en un árbol de búsqueda binaria. Primero, encontramos el elemento que estamos buscando atravesando el árbol. Luego, devolvemos el elemento.

Sin embargo, después de la búsqueda, necesitamos distribuir el elemento hasta la raíz. Esto se hace mediante una serie de rotaciones de árboles.

La siguiente figura muestra un ejemplo de búsqueda en un árbol de distribución:

![Buscar en un Splay Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Splay-tree-lookup.gif/250px-Splay-tree-lookup.gif)

## Eliminación

La eliminación de un árbol de distribución es similar a la eliminación de un árbol de búsqueda binaria. Primero, encontramos el elemento que queremos eliminar recorriendo el árbol. Luego, eliminamos el elemento.

Sin embargo, después de la eliminación, debemos distribuir el padre del elemento eliminado en la raíz. Esto se hace mediante una serie de rotaciones de árboles.

La siguiente figura muestra un ejemplo de eliminación de un árbol de distribución:

![Eliminación de un Splay Tree](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Splay-tree-delete.gif/250px-Splay-tree-delete.gif)

## Implementación

Un árbol splay se puede implementar como un árbol de búsqueda binaria. El siguiente pseudocódigo muestra un ejemplo de cómo insertar un elemento en un árbol de distribución:

```
insert(x, t)
  if t is empty
    return new node with value x
  if x < t.value
    t.left = insert(x, t.left)
  else
    t.right = insert(x, t.right)
  return t
```

El siguiente pseudocódigo muestra un ejemplo de cómo buscar un elemento en un árbol de distribución:

```
lookup(x, t)
  if t is empty
    return null
  if x < t.value
    return lookup(x, t.left)
  else if x > t.value
    return lookup(x, t.right)
  else
    return t
```

El siguiente pseudocódigo muestra un ejemplo de cómo eliminar un elemento de un árbol de distribución:

```
remove(x, t)
  if t is empty
    return null
  if x < t.value
    t.left = remove(x, t.left)
  else if x > t.value
    t.right = remove(x, t.right)
  else
    t = remove(t)
  return t

remove(t)
  if t.left is empty and t.right is empty
    return null
  if t.left is empty
    return t.right
  if t.right is empty
    return t.left
  y = t.right
  while y.left is not empty
    y = y.left
  t.right = remove(y.value, t.right)
  y.left = t.left
  y.right = t.right
  return y
```

## Complejidad

La complejidad temporal de las operaciones soportadas por los árboles splay es la siguiente:

* Inserción: O(log n)
* Búsqueda: O (registro n)
* Eliminación: O(log n)

La complejidad espacial de un árbol splay es O(n), donde n es el número de elementos en el árbol.