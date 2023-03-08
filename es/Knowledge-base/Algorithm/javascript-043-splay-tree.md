---
title: [JavaScript] 043: Árbol Splay
description: 
published: true
date: 2023-02-10T21:33:27.650Z
tags: 
editor: markdown
dateCreated: 2023-02-10T21:33:25.928Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 043: Splay Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-043-splay-tree)
{.links-list}


# Árbol de juego

Un árbol splay es un árbol de búsqueda binaria autoequilibrado con la propiedad de que los elementos a los que se accedió recientemente se vuelven a acceder rápidamente. Realiza operaciones básicas como inserción, búsqueda y eliminación en tiempo O(log(n)).

Un árbol splay es un árbol binario que satisface el siguiente invariante:

```
After each operation, the node that was accessed is moved to the root of the tree.
```

Esto significa que el nodo al que se accede con más frecuencia terminará cerca de la raíz del árbol, lo que facilita el acceso.

## Operaciones

Las operaciones básicas que se pueden realizar en un árbol splay son la inserción, la búsqueda y la eliminación.

### Inserción

Para insertar un nuevo nodo en el árbol, primero debemos encontrar la posición correcta para él. Hacemos esto comenzando en la raíz y recorriendo el árbol hasta encontrar el nodo que es mayor que el que estamos insertando. Luego insertamos el nuevo nodo como hijo de ese nodo.

Una vez que se ha insertado el nuevo nodo, debemos distribuirlo hasta la raíz. Para hacer esto, primero hacemos que el nuevo nodo sea la raíz del árbol. Luego, hacemos un seguimiento del nodo que anteriormente era la raíz (ahora el padre del nuevo nodo) y lo convertimos en el hijo izquierdo del nuevo nodo. Finalmente, hacemos que el hijo derecho del nuevo nodo sea la raíz anterior.

```javascript
function insert(value) {
    if (root === null) {
        root = new Node(value);
        return;
    }
 
    var curr = root;
    var parent = null;
    while (curr !== null) {
        if (value < curr.value) {
            parent = curr;
            curr = curr.left;
        } else if (value > curr.value) {
            parent = curr;
            curr = curr.right;
        } else {
            // value already exists in tree
            return;
        }
    }
 
    var newNode = new Node(value);
    if (value < parent.value) {
        parent.left = newNode;
    } else {
        parent.right = newNode;
    }
 
    // splay newNode to the root
    splay(newNode);
}
```

### Buscar

Para buscar un valor en el árbol, comenzamos en la raíz y recorremos el árbol hasta que encontramos el valor o llegamos a un nodo donde estaría el valor si estuviera en el árbol.

Una vez que encontramos el nodo, lo extendemos hasta la raíz. Si el valor no está en el árbol, el nodo que terminamos extendiendo a la raíz será el nodo donde estaría el valor si estuviera en el árbol.

```javascript
function lookup(value) {
    if (root === null) {
        return null;
    }
 
    var curr = root;
    while (curr !== null) {
        if (value < curr.value) {
            curr = curr.left;
        } else if (value > curr.value) {
            curr = curr.right;
        } else {
            // value found
            break;
        }
    }
 
    splay(curr);
    return curr;
}
```

### Eliminación

Para eliminar un valor del árbol, primero debemos encontrar el nodo que contiene el valor. Hacemos esto comenzando en la raíz y recorriendo el árbol hasta que encontramos el valor o llegamos a un nodo donde estaría el valor si estuviera en el árbol.

Si el valor está en el árbol, eliminamos el nodo y extendemos su padre hasta la raíz. Si el valor no está en el árbol, desplegamos el nodo donde estaría el valor si estuviera en el árbol hasta la raíz.

```javascript
function remove(value) {
    if (root === null) {
        return;
    }
 
    var curr = root;
    while (curr !== null) {
        if (value < curr.value) {
            curr = curr.left;
        } else if (value > curr.value) {
            curr = curr.right;
        } else {
            // value found
            break;
        }
    }
 
    if (curr === null) {
        // value not in tree
        return;
    }
 
    // remove curr
    if (curr.left === null && curr.right === null) {
        // curr is a leaf
        if (curr === root) {
            root = null;
        } else {
            var parent = curr.parent;
            if (parent.left === curr) {
                parent.left = null;
            } else {
                parent.right = null;
            }
 
            splay(parent);
        }
    } else if (curr.left === null) {
        // curr has only right child
        if (curr === root) {
            root = curr.right;
            root.parent = null;
        } else {
            var parent = curr.parent;
            curr.right.parent = parent;
            if (parent.left === curr) {
                parent.left = curr.right;
            } else {
                parent.right = curr.right;
            }
 
            splay(parent);
        }
    } else if (curr.right === null) {
        // curr has only left child
        if (curr === root) {
            root = curr.left;
            root.parent = null;
        } else {
            var parent = curr.parent;
            curr.left.parent = parent;
            if (parent.left === curr) {
                parent.left = curr.left;
            } else {
                parent.right = curr.left;
            }
 
            splay(parent);
        }
    } else {
        // curr has both left and right child
        var next = curr.right;
        while (next.left !== null) {
            next = next.left;
        }
 
        // next is the successor of curr (the smallest node in curr's right subtree)
        // remove next from its current position and replace it with its right child
        var parent = next.parent;
        if (parent.left === next) {
            parent.left = next.right;
        } else {
            parent.right = next.right;
        }
        if (next.right !== null) {
            next.right.parent = parent;
        }
 
        // replace curr with next
        next.left = curr.left;
        next.right = curr.right;
        next.parent = curr.parent;
        curr.left.parent = next;
        curr.right.parent = next;
        if (curr === root) {
            root = next;
        } else {
            if (curr.parent.left === curr) {
                curr.parent.left = next;
            } else {
                curr.parent.right = next;
            }
        }
 
        splay(next);
    }
}
```

## Jugando

Splaying es el proceso de mover un nodo a la raíz del árbol. Esto se hace mediante una serie de rotaciones. El tipo de rotación realizada depende de la posición del nodo con respecto a la raíz.

Hay tres casos posibles:

- El nodo es la raíz: no se necesita rotación.
- El nodo es un hijo de la raíz: se necesita una sola rotación.
- El nodo no es hijo de la raíz: se necesita una doble rotación.

### Rotación simple

Se realiza una sola rotación cuando el nodo que se va a desplegar es un hijo de la raíz. Hay dos casos posibles, dependiendo de si el nodo es el hijo derecho o el hijo izquierdo de la raíz.

#### Rotación a la izquierda

```javascript
function leftRotate(node) {
    var rightChild = node.right;
    node.right = rightChild.left;
    if (rightChild.left !== null) {
        rightChild.left.parent = node;
    }
    rightChild.parent = node.parent;
    if (node.parent === null) {
        root = rightChild;
    } else if (node === node.parent.left) {
        node.parent.left = rightChild;
    } else {
        node.parent.right = rightChild;
    }
    rightChild.left = node;
    node.parent = rightChild;
}
```

#### Rotación a la derecha

```javascript
function rightRotate(node) {
    var leftChild = node.left;
    node.left = leftChild.right;
    if (leftChild.right !== null) {
        leftChild.right.parent = node;
    }
    leftChild.parent = node.parent;
    if (node.parent === null) {
        root = leftChild;
    } else if (node === node.parent.right) {
        node.parent.right = leftChild;
    } else {
        node.parent.left = leftChild;
    }
    leftChild.right = node;
    node.parent = leftChild;
}
```

### Rotación doble

Se realiza una doble rotación cuando el nodo a desplegar no es hijo de la raíz. Hay cuatro casos posibles, dependiendo de si el nodo es el hijo izquierdo o derecho de la raíz y si el padre del nodo es el hijo izquierdo o derecho de la raíz.

#### Rotación izquierda-derecha

```javascript
function leftRightRotate(node) {
    var leftChild = node.left;
    var leftRightChild = leftChild.right;
    leftChild.right = leftRightChild.left;
    if (leftRightChild.left !== null) {
        leftRightChild.left.parent = leftChild;
    }
    node.left = leftRightChild.right;
    if (leftRightChild.right !== null) {
        leftRightChild.right.parent = node;
    }
    leftRightChild.left = leftChild;
    leftRightChild.right = node;
    leftChild.parent = leftRightChild;
    node.parent = leftRightChild;
    leftRightChild.parent = node.parent;
    if (node.parent === null) {
        root = leftRightChild;
    } else if (node === node.parent.left) {
        node.parent.left = leftRightChild;
    } else {
        node.parent.right = leftRightChild;
    }
}
```

#### Rotación derecha-izquierda

```javascript
function rightLeftRotate(node) {
    var rightChild = node.right;
    var rightLeftChild = rightChild.left;
    rightChild.left = rightLeftChild.right;
    if (rightLeftChild.right !== null) {
        rightLeftChild.right.parent = rightChild;
    }
    node.right = rightLeftChild.left;
    if (rightLeftChild.left !== null) {
        rightLeftChild.left.parent = node;
    }
    rightLeftChild.right = rightChild;
    rightLeftChild.left = node;
    rightChild.parent = rightLeftChild;
    node.parent = rightLeftChild;
    rightLeftChild.parent = node.parent;
    if (node.parent === null) {
        root = rightLeftChild;
    } else if (node === node.parent.left) {
        node.parent.left = rightLeftChild;
    } else {
        node.parent.right = rightLeftChild;
    }
}
```

## Complejidad

La complejidad temporal de las operaciones en un árbol splay se amortiza O(log(n)). Esto significa que, en promedio, las operaciones tomarán un tiempo O(log(n)). Sin embargo, en el peor de los casos, pueden tomar tiempo O(n).

La complejidad espacial de un árbol splay es O(n), donde n es el número de nodos en el árbol.