---
title: [Lenguaje C] 021: Árbol B
description: 
published: true
date: 2023-02-13T05:33:45.741Z
tags: 
editor: markdown
dateCreated: 2023-02-13T05:33:44.100Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 021: B-Tree***English** document is available*](/en/Knowledge-base/Algorithm/c-language-021-b-tree)
{.links-list}


# 021: Árbol B

Un árbol B es una estructura de datos de árbol autoequilibrada que mantiene los datos ordenados y permite búsquedas, acceso secuencial, inserciones y eliminaciones en tiempo logarítmico. El árbol B es una generalización de un árbol de búsqueda binario en el que un nodo puede tener más de dos hijos.

## Concepto

Un árbol B es un árbol enraizado en el que cada nodo no tiene más de M hijos. Un árbol B se define por el término grado mínimo `t`. El nodo raíz puede tener menos de `t` hijos. Si un nodo no es el nodo raíz y no es un nodo hoja, debe tener al menos "t" hijos. Si un nodo es un nodo hoja, debe tener al menos claves `t-1`. Todas las hojas aparecen en el mismo nivel, y un nodo que no es una hoja con elementos secundarios `k` contiene claves `k-1`.

Definimos el índice `i` de un nodo como el número de hijos que tiene. Por ejemplo, el nodo raíz tiene el índice 0, el primer hijo del nodo raíz tiene el índice 1, y así sucesivamente.

La altura de un árbol B es el número de niveles en el camino más largo desde la raíz hasta una hoja.

El siguiente es un ejemplo de un árbol B de grado mínimo `t=2`:

![Árbol](https://upload.wikimedia.org/wikipedia/commons/thumb/d/df/B-tree_example.svg/300px-B-tree_example.svg.png)

## Operaciones

Un árbol B admite las siguientes operaciones:

- Buscar: Dada una clave `k`, encuentre el valor asociado con `k`.
- Insertar: dado un par clave-valor `(k,v)`, inserte `(k,v)` en el árbol B.
- Eliminar: Dada una clave `k`, elimine el par clave-valor `(k,v)` del árbol B.

Todas estas operaciones se realizan en tiempo logarítmico.

## Implementación

Un árbol B se puede implementar usando una matriz o una lista enlazada.

### Implementación de matrices

En una implementación de matriz, cada nodo del árbol B está representado por una matriz de tamaño `M`. El primer elemento de la matriz es el número de claves en el nodo, `n`. Los elementos `M-1` restantes son las claves `n` y los hijos `n+1` del nodo, en orden.

Por ejemplo, el nodo raíz de la figura anterior está representado por la matriz `[3, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120]`.

Las operaciones de búsqueda, inserción y eliminación se pueden realizar de forma similar a un árbol de búsqueda binario.

### Implementación de listas enlazadas

En una implementación de lista enlazada, cada nodo del árbol B está representado por una lista enlazada de tamaño `M`. El primer elemento de la lista enlazada es el número de claves en el nodo, `n`. Los elementos `M-1` restantes son las claves `n` y los hijos `n+1` del nodo, en orden.

Por ejemplo, el nodo raíz de la figura anterior está representado por la lista enlazada `[3, 10, 20, 30, 40, 50, 60, 70, 80, 90, 100, 110, 120]`.

Las operaciones de búsqueda, inserción y eliminación se pueden realizar de forma similar a un árbol de búsqueda binario.

## Ejemplos de código

### Implementación de matrices

```c
#include <stdio.h>
#include <stdlib.h>

#define M 4

typedef struct btreenode {
  int n;
  int keys[M-1];
  struct btreenode* children[M];
} btreenode;

btreenode* btree_create()
{
  btreenode* root = (btreenode*)malloc(sizeof(btreenode));
  root->n = 0;
  return root;
}

void btree_search(btreenode* root, int key, btreenode** out_node, int* out_index)
{
  int i = 0;
  while (i < root->n && key > root->keys[i]) {
    i++;
  }
  if (i < root->n && key == root->keys[i]) {
    *out_node = root;
    *out_index = i;
    return;
  }
  if (root->children[i] == NULL) {
    *out_node = NULL;
    return;
  }
  btree_search(root->children[i], key, out_node, out_index);
}

void btree_insert(btreenode* root, int key, int value)
{
  btreenode* node;
  int index;
  btree_search(root, key, &node, &index);
  if (node != NULL) {
    // key already exists, update value
    node->values[index] = value;
    return;
  }
  // key does not exist, insert key-value pair
  if (root->n < M-1) {
    // insert into node
    int i = root->n-1;
    while (i >= 0 && key < root->keys[i]) {
      root->keys[i+1] = root->keys[i];
      root->values[i+1] = root->values[i];
      i--;
    }
    root->keys[i+1] = key;
    root->values[i+1] = value;
    root->n++;
  } else {
    // node is full, split node
    btreenode* left = (btreenode*)malloc(sizeof(btreenode));
    btreenode* right = (btreenode*)malloc(sizeof(btreenode));
    int i, j, k;
    // copy keys and values to left and right nodes
    for (i = 0, j = 0, k = 0; i < root->n; i++) {
      if (i == j) {
        // copy key to left node
        left->keys[k] = root->keys[i];
        left->values[k] = root->values[i];
        k++;
      } else {
        // copy key to right node
        right->keys[j] = root->keys[i];
        right->values[j] = root->values[i];
        j++;
      }
      if (k == M/2) {
        // left node is full, copy remaining keys and values to right node
        while (i < root->n) {
          right->keys[j] = root->keys[i];
          right->values[j] = root->values[i];
          i++;
          j++;
        }
      }
    }
    // update root
    root->n = 1;
    root->keys[0] = left->keys[M/2];
    root->children[0] = left;
    root->children[1] = right;
    // insert key and value into appropriate node
    if (key < root->keys[0]) {
      btree_insert(left, key, value);
    } else {
      btree_insert(right, key, value);
    }
  }
}

void btree_delete(btreenode* root, int key)
{
  btreenode* node;
  int index;
  btree_search(root, key, &node, &index);
  if (node == NULL) {
    // key does not exist
    return;
  }
  // key exists, delete key-value pair
  if (node->children[index] == NULL) {
    // key is in leaf node, simply delete it
    int i;
    for (i = index; i < node->n-1; i++) {
      node->keys[i] = node->keys[i+1];
      node->values[i] = node->values[i+1];
    }
    node->n--;
  } else {
    // key is in an internal node, find predecessor (or successor)
    btreenode* pred = node->children[index];
    while (pred->children[pred->n] != NULL) {
      pred = pred->children[pred->n];
    }
    // replace key with predecessor's key
    node->keys[index] = pred->keys[pred->n-1];
    // recursively delete predecessor
    btree_delete(pred, pred->keys[pred->n-1]);
  }
}

void btree_destroy(btreenode* root)
{
  if (root == NULL) return;
  int i;
  for (i = 0; i <= root->n; i++) {
    btree_destroy(root->children[i]);
  }
  free(root);
}

int main()
{
  btreenode* root = btree_create();
  btree_insert(root, 10, 1);
  btree_insert(root, 20, 2);
  btree_insert(root, 30, 3);
  btree_insert(root, 40, 4);
  btree_insert(root, 50, 5);
  btree_insert(root, 60, 6);
  btree_insert(root, 70, 7);
  btree_insert(root, 80, 8);
  btree_insert(root, 90, 9);
  btree_insert(root, 100, 10);
  btree_insert(root, 110, 11);
  btree_insert(root, 120, 12);
  btree_destroy(root);
  return 0;
}
```

### Implementación de listas enlazadas

```c
# incluir <stdio.h>
# incluir <stdlib.h>

# definir M 4

typedef estructura btreenode {
  int n;
  teclas int[M-1];
  struct btreenode* niños[M];
} nodo de árbol;

btreenode* btree_create()
{
  btreenode* root = (btreenode*)malloc(sizeof(btreenode));
  raíz->n = 0;
  devolver raíz;
}

void btree_search(btreenode* root, int key, btreenode** out_node, int* out_index)
{
  int i = 0;
  while (i < raíz->n && clave > raíz->claves[i]) {
    yo++;
  }
  if (i < raíz->n && clave == raíz->claves[i]) {
    *out_node = root;
    *out_index = i;
    devolver;
  }
  if (raíz->hijos[i] == NULL) {
    *out_node = NULL;
    devolver;
  }
  btree_search(root->child[i], key, out_node, out_index);
}

void btree_insert(btreenode* raíz, clave int, valor int)
{
  btreenode* nodo;
  índice int;
  btree_search(raíz, clave, &nodo, &índice);
  si (nodo! = NULL) {
    // la clave ya existe, actualice el valor
    nodo->valores[índice] = valor;
    devolver;
  }
  // la clave no existe, inserte el par clave-valor
  si (raiz->n < M-1) {
    // insertar en el nodo
    int i = raíz->n-1;
    while (i >= 0 && clave <raíz->claves[i]) {
      raíz->claves[i+1] = raíz->claves[i];
      raíz->valores[i+1] = raíz->valores[i];
      i--;
    }
    raíz->claves[i+1] = clave;
    raíz->valores[i+1] = valor;
    raíz->n++;
  } demás {
    // el nodo está lleno, dividir el nodo
    btreenode* izquierda = (btreenode*)malloc(tamañode(btreenode));
    btreenode* derecha = (btreenode*)malloc(tamañode(btreenode));
    int i, j, k;
    // copia claves y valores a los nodos izquierdo y derecho
    para (i = 0, j = 0, k = 0; i < raíz->n; i++) {
      si (yo == j) {
        // copia la clave al nodo izquierdo
        izquierda->teclas[k] = raíz->teclas[i];
        izquierda->valores[k] = raíz->valores[i];
        k++;
      } demás {
        // copia la clave al nodo derecho
        derecha->teclas[j] = raíz->teclas[i];
        derecha->valores[j] = raíz->valores[i];
        j++;
      }
      si (k == M/2) {
        // el nodo izquierdo está lleno, copie las claves y los valores restantes en el nodo derecho
        while (i <raíz->n) {
          derecha->teclas[j] = raíz->teclas[i];
          derecha->valores[j] = raíz->valores[i];
          yo++;
          j++;
        }
      }
    }
    // actualizar raíz
    raíz->n = 1;
    raíz->teclas[0] = izquierda->teclas[M/2];
    raíz->hijos[0] = izquierda;
    raíz->hijos[1] = derecho;
    // inserta clave y valor en el nodo apropiado
    if (clave <raíz->claves[0]) {
      btree_insert(izquierda, clave, valor);
    } demás {
      btree_insert(derecha, clave, valor);
    }
  }
}

void btree_delete(btreenode* raíz, clave int)
{
  btreenode* nodo;
  índice int;
  btree_search(raíz, clave, &nodo, &índice);
  si (nodo == NULL) {
    // la clave no existe
    devolver;
  }
  // la clave existe, elimina el par clave-valor
  if (nodo->hijos[índice] == NULL) {
    // la clave está en el nodo hoja, simplemente elimínela
    ent yo;
    for (i = índice; i < nodo->n-1; i++) {
      nodo->claves[i] = nodo->claves[i+1];
      nodo->valores[i] = nodo->valores[i+1];
    }
    nodo->n--;
  } demás {
    // la clave está en un nodo interno, busca predecesor (o sucesor)
    btreenode* pred = nodo->hijos[índice];
    while (pred->niños[pred->n] != NULL) {
      pred = pred->hijos[pred->n];
    }
    // reemplaza la clave con la clave del predecesor
    nodo->claves[índice] = pred->claves[pred->n-1];
    // borra recursivamente el predecesor
    btree_delete(pred, pred->keys[pred->n-1]);
  }
}

void btree_destroy(btreenode* raíz)
{
  si (raíz == NULL) devuelve;
  ent i;
  para (i = 0; i <= raíz->n; i++) {
    btree_destroy(raíz->hijos[i]);
  }
  libre (raíz);
}

int principal()
{
  btreenode* root = btree_create();
  btree_insert(raíz, 10, 1);
  btree_insert(raíz, 20, 2);
  btree_insert(raíz, 30, 3);
  btree_insert(raíz, 40, 4);
  btree_insert(raíz, 50, 5);
  btree_insert(raíz, 60, 6);
  btree_insert(raíz, 70, 7);
  btree_insert(raíz, 80, 8);