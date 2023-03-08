---
title: [Lenguaje C] 042: árbol rojo-negro
description: 
published: true
date: 2023-02-12T10:18:19.335Z
tags: 
editor: markdown
dateCreated: 2023-02-12T10:18:17.675Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 042: Red-Black Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-042-red-black-tree)
{.links-list}


# 042: Árbol Rojo-Negro

Un árbol rojo-negro es un árbol de búsqueda binario autoequilibrado en el que cada nodo tiene un atributo de color, cuyo valor es "rojo" o "negro". La siguiente es una representación visual de un árbol rojo-negro:

![Árbol negro rojo](https://upload.wikimedia.org/wikipedia/commons/thumb/6/66/Red-black_tree_example.svg/250px-Red-black_tree_example.svg.png)

Cada nodo de un Árbol Rojo-Negro tiene los siguientes atributos:

- **Clave**: Una clave es un valor que se utiliza para identificar un nodo. En el ejemplo anterior, las teclas son los números del 1 al 7.
- **Color**: un nodo puede ser "rojo" o "negro". El nodo raíz siempre es negro.
- **Hijo izquierdo**: Una referencia al nodo hijo izquierdo.
- **Secundario derecho**: una referencia al nodo secundario derecho.
- **Padre**: Una referencia al nodo padre.

Un árbol rojo-negro tiene las siguientes propiedades:

- **Propiedad 1 (Nodos rojos):** Un nodo es rojo si y solo si sus dos hijos son negros.
- **Propiedad 2 (Nodos negros):** Cada nodo es rojo o negro.
- **Propiedad 3 (Nodo raíz):** El nodo raíz es negro.
- **Propiedad 4 (Nodos hoja):** Todos los nodos hoja (nodos sin hijos) son negros.
- **Propiedad 5 (Propiedad rojo-negro):** Si un nodo es rojo, entonces sus dos hijos son negros.
- **Propiedad 6 (Rutas):** Todas las rutas simples desde un nodo hasta sus hojas descendientes contienen el mismo número de nodos negros.

El siguiente es un ejemplo de un Árbol Rojo-Negro que no cumple con la Propiedad 5 (Propiedad Rojo-Negro):

![Árbol negro rojo no válido](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5f/Invalid_red_black_tree.svg/200px-Invalid_red_black_tree.svg.png)

Como puede ver, el nodo con la clave 4 es rojo, pero su hijo izquierdo también es rojo. Esto viola la Propiedad 5.

Ahora que hemos visto qué es un árbol rojo-negro, echemos un vistazo a cómo se usan.

## Aplicaciones

Los árboles rojo-negro se utilizan en una variedad de aplicaciones, tales como:

- **Índices de bases de datos**: Los árboles rojo-negro se utilizan a menudo como índices en las bases de datos. Esto se debe a que se pueden buscar, insertar y eliminar rápidamente.
- **Sistemas operativos**: los árboles rojo-negro se utilizan en el kernel de Linux para almacenar información de procesos.
- **Procesadores de texto**: los árboles rojos y negros se utilizan en los procesadores de texto para almacenar información sobre las posiciones de las palabras en un documento.

## Implementación

Ahora que hemos visto qué es un árbol rojo-negro y algunas de las aplicaciones en las que se utilizan, echemos un vistazo a cómo se implementan.

### Nodo

Primero, necesitamos crear una clase de Nodo. Esta clase almacenará la clave, el color, el hijo izquierdo, el hijo derecho y el padre de un nodo.

```java
public class Node {
    int key;
    boolean color;
    Node leftChild;
    Node rightChild;
    Node parent;

    public Node(int key, boolean color, Node leftChild, Node rightChild, Node parent) {
        this.key = key;
        this.color = color;
        this.leftChild = leftChild;
        this.rightChild = rightChild;
        this.parent = parent;
    }
}
```

### Árbol

A continuación, necesitamos crear una clase de árbol. Esta clase almacenará el nodo raíz del árbol.

```java
public class Tree {
    Node root;

    public Tree() {
        this.root = null;
    }
}
```

### Insertar

Ahora que tenemos una clase de Nodo y una clase de Árbol, podemos comenzar a implementar el Árbol Rojo-Negro. La primera operación que implementaremos es la operación de inserción.

Para insertar un nodo en un árbol rojo-negro, primero debemos encontrar el lugar correcto para insertarlo. Hacemos esto usando el algoritmo de inserción de árbol de búsqueda binaria. Una vez que hayamos encontrado el lugar correcto para insertar el nodo, debemos establecer el color del nodo en rojo. Luego, debemos verificar si el árbol aún es válido. Si el árbol no es válido, tenemos que arreglarlo.

El siguiente es el algoritmo de inserción:

```java
public void insert(int key) {
    // Create a new node with the given key and color it red
    Node newNode = new Node(key, true, null, null, null);

    // Find the correct place to insert the new node
    Node currentNode = root;
    Node parentNode = null;
    while (currentNode != null) {
        parentNode = currentNode;
        if (key < currentNode.key) {
            currentNode = currentNode.leftChild;
        } else {
            currentNode = currentNode.rightChild;
        }
    }

    // Set the new node's parent
    newNode.parent = parentNode;

    // Insert the new node into the tree
    if (parentNode == null) {
        // The new node is the root node
        root = newNode;
    } else if (key < parentNode.key) {
        // The new node is the left child of the parent node
        parentNode.leftChild = newNode;
    } else {
        // The new node is the right child of the parent node
        parentNode.rightChild = newNode;
    }

    // Fix the tree
    fixTree(newNode);
}
```

### Arreglar árbol

Ahora que hemos visto cómo insertar un nodo en un árbol rojo-negro, echemos un vistazo a cómo arreglar el árbol.

Hay cuatro casos que debemos considerar al arreglar un árbol rojo-negro:

- Caso 1 (el nodo es el nodo raíz): si el nodo es el nodo raíz, simplemente debemos establecer su color en negro.
- Caso 2 (El nodo es un nodo rojo con un padre negro): Si el nodo es un nodo rojo con un padre negro, entonces no hacemos nada.
- Caso 3 (el nodo es un nodo rojo con un padre rojo): si el nodo es un nodo rojo con un padre rojo, entonces debemos considerar los colores del tío y el abuelo del nodo. Si el tío también es rojo, entonces simplemente necesitamos establecer los colores del nodo, el padre y el tío en negro y el color del abuelo en rojo. Luego, necesitamos llamar recursivamente al método fixTree() en el nodo abuelo.

Si el tío es negro, entonces debemos considerar la orientación del padre y el nodo. Si el padre y el nodo son ambos hijos izquierdos o ambos hijos derechos, simplemente debemos establecer el color del padre en negro y el color del abuelo en rojo. Luego, necesitamos llamar recursivamente al método fixTree() en el nodo abuelo.

Si el padre y el nodo no son ambos hijos izquierdos o derechos, entonces necesitamos realizar una rotación a la izquierda o una rotación a la derecha. Después de la rotación, debemos establecer el color del nodo en negro y el color del abuelo en rojo. Luego, necesitamos llamar recursivamente al método fixTree() en el nodo abuelo.

- Caso 4 (el nodo es un nodo negro con un padre rojo): si el nodo es un nodo negro con un padre rojo, entonces debemos considerar los colores del tío y el abuelo del nodo. Si el tío también es rojo, simplemente tenemos que establecer los colores del padre y del tío en negro y el color del abuelo en rojo. Luego, necesitamos llamar recursivamente al método fixTree() en el nodo abuelo.

Si el tío es negro, entonces debemos considerar la orientación del padre y el nodo. Si el padre y el nodo son ambos hijos izquierdos o ambos hijos derechos, entonces debemos establecer el color del padre en negro. Luego, debemos llamar recursivamente al método fixTree() en el nodo principal.

Si el padre y el nodo no son ambos hijos izquierdos o derechos, entonces necesitamos realizar una rotación a la izquierda o una rotación a la derecha. Después de la rotación, debemos establecer el color del abuelo en rojo. Luego, necesitamos llamar recursivamente al método fixTree() en el nodo abuelo.

El siguiente es el algoritmo fixTree():

```java
public void fixTree(Node node) {
    // Case 1 (Node is the root node)
    if (node.parent == null) {
        node.color = false;
        return;
    }

    // Case 2 (Node is a red node with a black parent)
    if (node.color && !node.parent.color) {
        return;
    }

    // Case 3 (Node is a red node with a red parent)
    if (node.color && node.parent.color) {
        Node uncle = getUncle(node);

        if (uncle != null && uncle.color) {
            // Set the colors of the node, parent, and uncle to black and the color of the grandparent to red
            node.parent.color = false;
            uncle.color = false;
            getGrandparent(node).color = true;

            // Recursively call the fixTree() method on the grandparent node
            fixTree(getGrandparent(node));
        } else {
            // Perform a left rotation or right rotation
            if (node == node.parent.rightChild && node.parent == getGrandparent(node).leftChild) {
                // Perform a left rotation
                leftRotate(node.parent);

                // Set the colors of the node and parent to black and the color of the grandparent to red
                node.color = false;
                node.leftChild.color = true;
            } else if (node == node.parent.leftChild && node.parent == getGrandparent(node).rightChild) {
                // Perform a right rotation
                rightRotate(node.parent);

                // Set the colors of the node and parent to black and the color of the grandparent to red
                node.color = false;
                node.rightChild.color = true;
            }

            // Case 4 (Node is a black node with a red parent)
            if (node == node.parent.leftChild) {
                // Perform a right rotation
                rightRotate(getGrandparent(node));
            } else {
                // Perform a left rotation
                leftRotate(getGrandparent(node));
            }

            // Set the color of the grandparent to red
            getGrandparent(node).color = true;

            // Set the color of the parent to black
            node.parent.color = false;
        }
    }
}
```

### Girar a la izquierda

Ahora que hemos visto cómo arreglar un árbol rojo-negro, echemos un vistazo a cómo realizar una rotación a la izquierda.

Una rotación a la izquierda se usa para equilibrar un árbol cuando el hijo derecho de un nodo es más pesado que el hijo izquierdo. El siguiente es un ejemplo de una rotación a la izquierda:

![Rotación a la izquierda](https://upload.wikimedia.org/wikipedia/commons/2/2d/Left-rotation.svg)

Como puede ver, el nodo que se está girando es el nodo con clave 3. El hijo izquierdo de este nodo es el nodo con clave 2 y el hijo derecho es el nodo con clave 4. Después de la rotación, el nodo con clave 3 es el hijo izquierdo del nodo con clave 4 y el nodo con clave 2 es el hijo derecho del nodo con clave 3.

El siguiente es el algoritmo leftRotate():

```java
public void leftRotate(Node node) {
    // Check if the node has a right child
    if (node.rightChild == null) {
        return;
    }

    // Set the right child of the node to be the new root of the subtree
    Node newRoot = node.rightChild;

    // Set the left child of the new root to be the node's right child
    newRoot.leftChild = node;

    // Set the node's right child to be the new root's left child
    node.rightChild = newRoot.leftChild;

    // Set the new root's parent to be the node's parent
    newRoot.parent = node.parent;

    // Check if the node is the root node
    if (node.parent == null) {
        // Set the new root to be the root node
        root = newRoot;
    } else if (node == node.parent.leftChild) {
        // Set the new root to be the node's left child
        node.parent.leftChild = newRoot;
    } else {
        // Set the new root to be the node's right child
        node.parent.rightChild = newRoot;
    }

    // Set the node's parent to be the new root
    node.parent = newRoot;
}
```

### Girar a la derecha

Ahora que hemos visto cómo realizar una rotación a la izquierda, echemos un vistazo a cómo realizar una rotación a la derecha.

Se usa una rotación a la derecha para equilibrar un árbol cuando el hijo izquierdo de un nodo es más pesado que el hijo derecho. El siguiente es un ejemplo de una rotación a la derecha:

![Rotación derecha](https://upload.wikimedia.org/wikipedia/commons/d/d4/Right-rotation.svg)

Como puede ver, el nodo que se está girando es el nodo con clave 3. El hijo izquierdo de este nodo es el nodo con clave 2 y el hijo derecho es el nodo con clave 4. Después de la rotación, el nodo con clave 3 es el hijo derecho del nodo con clave 2 y el nodo con clave 4 es el hijo izquierdo del nodo con clave 3.

El siguiente es el algoritmo rightRotate():

```java
public void rightRotate(Node node) {
    // Check if the node has a left child
    if (node.leftChild == null) {
        return;
    }

    // Set the left child of the node to be the new root of the subtree
    Node newRoot = node.leftChild;

    // Set the right child of the new root to be the node's left child
    newRoot.rightChild = node;

    // Set the node's left child to be the new root's right child
    node.leftChild = newRoot.rightChild;

    // Set the new root's parent to be the node's parent
    newRoot.parent = node.parent;

    // Check if the node is the root node
    if (node.parent == null) {
        // Set the new root to be the root node
        root = newRoot;
    } else if (node == node.parent.rightChild) {
        // Set the new root to be the node's right child
        node.parent.rightChild = newRoot;
    } else {
        // Set the new root to be the node's left child
        node.parent.leftChild = newRoot;
    }

    // Set the node's parent to be the new root
    node.parent = newRoot;
}
```

### Borrar

Ahora que hemos visto cómo realizar una rotación a la derecha, echemos un vistazo a cómo eliminar un nodo de un árbol rojo-negro.

Para eliminar un nodo de un árbol rojo-negro, primero debemos encontrar el nodo que desea eliminar. Hacemos esto usando el algoritmo de eliminación del árbol de búsqueda binaria. Una vez que hayamos encontrado el nodo para eliminar, debemos verificar si el árbol aún es válido. Si el árbol no es válido, tenemos que arreglarlo.

El siguiente es el algoritmo de eliminación:

```java
public void delete(int key) {
    // Find the node to delete
    Node node = find(key);

    // Check if the node was found
    if (node == null) {
        return;
    }

    // Delete the node
    deleteNode(node);
}
```

### Eliminar nodo

Ahora que hemos visto cómo eliminar un nodo de un árbol rojo-negro, echemos un vistazo a cómo eliminar un nodo.

Hay tres casos que debemos considerar al eliminar un nodo de un Red-Black