---
title: [JavaScript] 042: Árbol rojo-negro
description: 
published: true
date: 2023-02-10T20:33:21.418Z
tags: 
editor: markdown
dateCreated: 2023-02-10T20:33:19.815Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 042: Red-Black Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-042-red-black-tree)
{.links-list}


# Árbol rojo-negro

Un árbol rojo-negro es una especie de árbol de búsqueda binario autoequilibrado en el que cada nodo tiene un bit adicional, y ese bit a menudo se interpreta como el color (rojo o negro) del nodo. Estos árboles se utilizan para implementar matrices asociativas, que se pueden asignar a un conjunto de pares clave-valor.

La propiedad de equilibrio de este árbol se utiliza para mantener un árbol de búsqueda aproximadamente equilibrado a medida que se agregan y eliminan elementos. El equilibrio del árbol no es perfecto, pero es lo suficientemente bueno como para garantizar que el árbol no esté significativamente desequilibrado.

La idea básica detrás de un árbol rojo-negro es colorear los nodos del árbol de rojo o negro de tal manera que se cumplan las siguientes propiedades:

1. Cada nodo es rojo o negro.
2. La raíz es negra.
3. Cada hoja (NIL) es negra.
4. Si un nodo es rojo, entonces sus dos hijos son negros.
5. Para cada nodo, todos los caminos simples desde el nodo hasta las hojas descendientes contienen el mismo número de nodos negros.

Estas propiedades aseguran que el árbol esté equilibrado, de modo que la altura del árbol sea O (log n).

## Ejemplos de código

Aquí hay una implementación simple de un árbol rojo-negro en JavaScript. Comenzamos definiendo una clase de Nodo, que tiene un valor, un color y nodos secundarios izquierdo y derecho.

```javascript
class Node {
  constructor(value, color, left, right) {
    this.value = value;
    this.color = color;
    this.left = left;
    this.right = right;
  }
}
```

También necesitamos una forma de comparar dos nodos, de modo que podamos insertarlos en el árbol en el orden correcto. Podemos hacer esto con una función de comparación, que toma dos nodos y devuelve un número que indica si el primer nodo es menor, igual o mayor que el segundo nodo.

```javascript
function compare(a, b) {
  if (a.value < b.value) {
    return -1;
  }
  if (a.value > b.value) {
    return 1;
  }
  return 0;
}
```

Ahora podemos definir nuestra clase de árbol rojo-negro. Comenzaremos con una función constructora, que toma una función de comparación como argumento. También inicializaremos un nodo raíz en nulo.

```javascript
class RedBlackTree {
  constructor(compare) {
    this.compare = compare;
    this.root = null;
  }
}
```

Ahora podemos implementar la función de inserción. Esta función toma un valor como argumento y lo inserta en el árbol en la posición correcta. Si el valor ya está en el árbol, no se volverá a insertar.

```javascript
RedBlackTree.prototype.insert = function(value) {
  //create a new node
  let node = new Node(value, "red", null, null);

  //insert the node into the tree in the correct position
  if (this.root === null) {
    this.root = node;
  } else {
    let current = this.root;
    let parent;
    while (true) {
      parent = current;
      if (this.compare(node, current) < 0) {
        current = current.left;
        if (current === null) {
          parent.left = node;
          break;
        }
      } else if (this.compare(node, current) > 0) {
        current = current.right;
        if (current === null) {
          parent.right = node;
          break;
        }
      } else {
        //the value is already in the tree, so we don't insert it
        break;
      }
    }
  }

  //fix any violations of the red-black properties
  this.fixViolations(node);
};
```

Tenga en cuenta que no necesitamos establecer explícitamente el color del nuevo nodo en rojo, ya que ya está configurado en rojo de forma predeterminada.

También necesitamos implementar una función fixViolations, que toma un nodo como argumento y corrige cualquier violación de las propiedades rojo-negro.

```javascript
RedBlackTree.prototype.fixViolations = function(node) {
  let current = node;
  let parent = current.parent;
  let grandParent = parent.parent;

  while (parent && parent.color === "red") {
    if (grandParent.left === parent) {
      //we are on the left side of the tree
      let uncle = grandParent.right;
      if (uncle && uncle.color === "red") {
        //case 1: the parent and uncle are both red
        parent.color = "black";
        uncle.color = "black";
        grandParent.color = "red";
        current = grandParent;
      } else {
        if (current === parent.right) {
          //case 2: the parent is red and the current node is on the right side
          //of the tree
          this.rotateLeft(parent);
          current = parent;
          parent = current.parent;
        }
        //case 3: the parent is red and the current node is on the left side
        //of the tree
        parent.color = "black";
        grandParent.color = "red";
        this.rotateRight(grandParent);
      }
    } else {
      //we are on the right side of the tree
      let uncle = grandParent.left;
      if (uncle && uncle.color === "red") {
        //case 1: the parent and uncle are both red
        parent.color = "black";
        uncle.color = "black";
        grandParent.color = "red";
        current = grandParent;
      } else {
        if (current === parent.left) {
          //case 2: the parent is red and the current node is on the left side
          //of the tree
          this.rotateRight(parent);
          current = parent;
          parent = current.parent;
        }
        //case 3: the parent is red and the current node is on the right side
        //of the tree
        parent.color = "black";
        grandParent.color = "red";
        this.rotateLeft(grandParent);
      }
    }
    parent = current.parent;
    grandParent = parent.parent;
  }

  //make sure the root node is black
  this.root.color = "black";
};
```

Tenga en cuenta que debemos realizar un seguimiento del padre, el abuelo y el tío del nodo actual, así como del propio nodo actual.

También necesitamos implementar funciones de rotar a la izquierda y rotar a la derecha. Estas funciones toman un nodo como argumento y giran el árbol alrededor de ese nodo.

```javascript
RedBlackTree.prototype.rotateLeft = function(node) {
  let rightChild = node.right;
  node.right = rightChild.left;

  if (rightChild.left !== null) {
    rightChild.left.parent = node;
  }

  rightChild.parent = node.parent;

  if (node.parent === null) {
    this.root = rightChild;
  } else if (node === node.parent.left) {
    node.parent.left = rightChild;
  } else {
    node.parent.right = rightChild;
  }

  rightChild.left = node;
  node.parent = rightChild;
};

RedBlackTree.prototype.rotateRight = function(node) {
  let leftChild = node.left;
  node.left = leftChild.right;

  if (leftChild.right !== null) {
    leftChild.right.parent = node;
  }

  leftChild.parent = node.parent;

  if (node.parent === null) {
    this.root = leftChild;
  } else if (node === node.parent.right) {
    node.parent.right = leftChild;
  } else {
    node.parent.left = leftChild;
  }

  leftChild.right = node;
  node.parent = leftChild;
};
```

Estas funciones son bastante simples. Solo necesitamos realizar un seguimiento del padre, hijo y nieto del nodo que se está rotando.

También podemos implementar una función de eliminación, que toma un valor como argumento y elimina el nodo con ese valor del árbol.

```javascript
RedBlackTree.prototype.remove = function(value) {
  //find the node to be removed
  let current = this.root;
  let parent = current;
  let isLeftChild = true;
  while (current.value !== value) {
    parent = current;
    if (this.compare(value, current) < 0) {
      //the value is less than the current node, so go to the left child
      isLeftChild = true;
      current = current.left;
    } else {
      //the value is greater than the current node, so go to the right child
      isLeftChild = false;
      current = current.right;
    }
    if (current === null) {
      //the value is not in the tree
      return false;
    }
  }

  //case 1: the node to be removed is a leaf
  if (current.left === null && current.right === null) {
    if (current === this.root) {
      //the tree is empty
      this.root = null;
    } else if (isLeftChild) {
      //the node is a left child
      parent.left = null;
    } else {
      //the node is a right child
      parent.right = null;
    }
  }
  //case 2: the node to be removed has one child
  else if (current.right === null) {
    //the node is a left child
    if (current === this.root) {
      this.root = current.left;
    } else if (isLeftChild) {
      parent.left = current.left;
    } else {
      parent.right = current.left;
    }
  } else if (current.left === null) {
    //the node is a right child
    if (current === this.root) {
      this.root = current.right;
    } else if (isLeftChild) {
      parent.left = current.right;
    } else {
      parent.right = current.right;
    }
  }
  //case 3: the node to be removed has two children
  else {
    //find the successor of the node to be removed
    let successor = this.getSuccessor(current);

    //connect the parent of the current node to the successor
    if (current === this.root) {
      this.root = successor;
    } else if (isLeftChild) {
      parent.left = successor;
    } else {
      parent.right = successor;
    }

    //connect the left child of the current node to the successor
    successor.left = current.left;
  }

  //fix any violations of the red-black properties
  this.fixViolations(node);

  //return true to indicate that the node was removed
  return true;
};
```

Esta función es similar a la función de inserción. Solo necesitamos realizar un seguimiento del padre, hijo y nieto del nodo que se está eliminando.

También necesitamos implementar una función getSuccessor, que toma un nodo como argumento y devuelve el sucesor de ese nodo.

```javascript
RedBlackTree.prototype.getSuccessor = function(node) {
  let current = node.right;
  let parent = node;
  while (current.left !== null) {
    parent = current;
    current = current.left;
  }
  if (current !== node.right) {
    parent.left = current.right;
    current.right = node.right;
  }
  return current;
};
```

Esta función es similar a la función de eliminación. Solo necesitamos realizar un seguimiento del padre, hijo y nieto del nodo que se está eliminando.

## Ejercicios relacionados

- [ ] Implementar una función para comprobar si un árbol binario es un árbol de búsqueda binaria.
- [ ] Implementar una función para encontrar el k-ésimo elemento más pequeño en un árbol de búsqueda binaria.