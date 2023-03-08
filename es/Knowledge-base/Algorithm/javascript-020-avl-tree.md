---
title: [JavaScript] 020: Árbol AVL
description: 
published: true
date: 2023-02-09T22:32:19.238Z
tags: 
editor: markdown
dateCreated: 2023-02-09T22:32:17.614Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 020: AVL Tree***English** document is available*](/en/Knowledge-base/Algorithm/javascript-020-avl-tree)
{.links-list}


# JavaScript 020: Árbol AVL

Un árbol AVL es un tipo de árbol de búsqueda binario autoequilibrado, en el que los nodos se organizan de manera que las alturas de los dos subárboles secundarios de cualquier nodo difieren como máximo en uno. Este equilibrio del árbol le permite ser más eficiente al buscar valores, ya que es más probable que el árbol esté más cerca de un estado equilibrado.

La altura de un árbol AVL es el número de aristas en el camino más largo desde la raíz hasta una hoja. La altura de un árbol vacío se define como −1. Se dice que un árbol AVL está equilibrado si la altura de los subárboles izquierdo y derecho de la raíz difieren como máximo en 1, y los subárboles izquierdo y derecho son árboles AVL.

## Ejemplo de código

El siguiente es un ejemplo de cómo insertar un nodo en un árbol AVL en JavaScript.

```javascript
function insert(root, key) { 
    // Step 1 - Perform normal BST insertion 
    if (root == null) 
        return new Node(key); 
  
    if (key < root.key) 
        root.left = insert(root.left, key); 
    else if (key > root.key) 
        root.right = insert(root.right, key); 
    else // Equal keys are not allowed in BST 
        return root; 
  
    // Step 2 - Update the height of the  
             // ancestor node 
    root.height = 1 + Math.max(height(root.left), 
                              height(root.right)); 
  
    // Step 3 - Get the balance factor 
    let balance = getBalance(root); 
  
    // Step 4 - If the node is unbalanced,  
    // then there are 4 cases 
  
    // Left Left Case 
    if (balance > 1 && key < root.left.key) 
        return rightRotate(root); 
  
    // Right Right Case 
    if (balance < -1 && key > root.right.key) 
        return leftRotate(root); 
  
    // Left Right Case 
    if (balance > 1 && key > root.left.key) { 
        root.left = leftRotate(root.left); 
        return rightRotate(root); 
    } 
  
    // Right Left Case 
    if (balance < -1 && key < root.right.key) { 
        root.right = rightRotate(root.right); 
        return leftRotate(root); 
    } 
  
    /* return the (unchanged) node pointer */
    return root; 
} 
```

## Ejercicios

1. Implemente un árbol AVL en JavaScript.

2. Dada una lista de números, cree un árbol AVL de esos números.

3. Encuentra la altura de un árbol AVL.

4. Encuentre el valor mínimo en un árbol AVL.

5. Encuentre el valor máximo en un árbol AVL.

6. Encuentra el predecesor de un valor dado en un árbol AVL.

7. Encuentra el sucesor de un valor dado en un árbol AVL.

8. Eliminar un valor de un árbol AVL.

9. Realice un recorrido de preorden de un árbol AVL.

10. Realice un recorrido en orden de un árbol AVL.

11. Realice un recorrido posterior al pedido de un árbol AVL.