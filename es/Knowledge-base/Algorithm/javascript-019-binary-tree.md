---
title: [JavaScript] 019: árbol binario
description: 
published: true
date: 2023-02-09T21:32:36.343Z
tags: 
editor: markdown
dateCreated: 2023-02-09T21:32:34.692Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 019: Binary Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-019-binary-tree)
{.links-list}


# Árbol binario

En informática, un árbol binario es una estructura de datos de árbol en la que cada nodo tiene como máximo dos hijos, a los que se hace referencia como el hijo izquierdo y el hijo derecho.

Un árbol binario es una estructura que permite dos operaciones:

- Encontrar el elemento máximo en el árbol.
- Encontrar el elemento mínimo en el árbol.

La complejidad temporal de ambas operaciones es O(log n), donde n es el número de nodos en el árbol.

Los árboles binarios se utilizan para implementar montones y árboles de búsqueda binarios.

## Ejemplo de código

Aquí hay un ejemplo de un árbol binario en JavaScript:

```javascript
var tree = {
  value: 10,
  left: {
    value: 5,
    left: {
      value: 2,
      left: null,
      right: null
    },
    right: {
      value: 7,
      left: null,
      right: null
    }
  },
  right: {
    value: 15,
    left: {
      value: 12,
      left: null,
      right: null
    },
    right: {
      value: 17,
      left: null,
      right: null
    }
  }
};
```

## Encontrar el elemento máximo

Para encontrar el elemento máximo en un árbol binario, podemos usar un algoritmo recursivo.

La idea es comparar el nodo raíz con sus nodos secundarios izquierdo y derecho. Si el nodo raíz es mayor que sus dos nodos secundarios, entonces es el elemento máximo. De lo contrario, el elemento máximo será el mayor de los dos nodos secundarios.

Luego podemos llamar recursivamente al mismo algoritmo en los nodos secundarios izquierdo y derecho.

Aquí está el pseudocódigo para el algoritmo:

```
function findMax(node) {
  if (node is null) {
    return null;
  }
 
  var max = node.value;
  var leftMax = findMax(node.left);
  var rightMax = findMax(node.right);
 
  if (leftMax > max) {
    max = leftMax;
  }
 
  if (rightMax > max) {
    max = rightMax;
  }
 
  return max;
}
```

## Encontrar el elemento mínimo

Para encontrar el elemento mínimo en un árbol binario, podemos usar un algoritmo recursivo.

La idea es comparar el nodo raíz con sus nodos secundarios izquierdo y derecho. Si el nodo raíz es menor que sus dos nodos secundarios, entonces es el elemento mínimo. De lo contrario, el elemento mínimo será el menor de los dos nodos secundarios.

Luego podemos llamar recursivamente al mismo algoritmo en los nodos secundarios izquierdo y derecho.

Aquí está el pseudocódigo para el algoritmo:

```
function findMin(node) {
  if (node is null) {
    return null;
  }
 
  var min = node.value;
  var leftMin = findMin(node.left);
  var rightMin = findMin(node.right);
 
  if (leftMin < min) {
    min = leftMin;
  }
 
  if (rightMin < min) {
    min = rightMin;
  }
 
  return min;
}
```

## Ejercicios relacionados

- [Profundidad máxima de un árbol binario](https://leetcode.com/problems/maximum- depth-of-binary-tree/)
- [Profundidad mínima de un árbol binario](https://leetcode.com/problems/minimum- depth-of-binary-tree/)
- [Árbol simétrico](https://leetcode.com/problems/simétrico-árbol/)
- [Recorrido en orden de árbol binario] (https://leetcode.com/problems/binary-tree-inorder-traversal/)
- [Recorrido del postorden del árbol binario](https://leetcode.com/problems/binary-tree-postorder-traversal/)
- [Recorrido de pedido anticipado de árbol binario] (https://leetcode.com/problems/binary-tree-preorder-traversal/)