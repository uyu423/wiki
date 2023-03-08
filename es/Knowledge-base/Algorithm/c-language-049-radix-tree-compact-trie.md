---
title: [Lenguaje C] 049: Árbol Radix (Trie compacto)
description: 
published: true
date: 2023-02-10T12:55:21.027Z
tags: 
editor: markdown
dateCreated: 2023-02-10T12:55:19.358Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 049: Radix Tree (Compact Trie)***English** document is available*](/en/Knowledge-base/Algorithm/c-language-049-radix-tree-compact-trie)
{.links-list}


# 049: Árbol Radix (Trie Compacto)

## 1. Introducción

Un árbol radix, también conocido como trie compacto, es una estructura de datos eficiente en el espacio que se utiliza para almacenar cadenas. Es similar a un árbol binario, pero cada nodo tiene solo dos hijos, en lugar de dos hijos por nodo.

## 2. Algoritmo

El algoritmo de árbol radix es una forma eficiente de espacio para almacenar cadenas. Es similar a un árbol binario, pero cada nodo tiene solo dos hijos, en lugar de dos hijos por nodo.

El algoritmo de árbol radix es una forma eficiente de espacio para almacenar cadenas. Es similar a un árbol binario, pero cada nodo tiene solo dos hijos, en lugar de dos hijos por nodo.

Para insertar una cadena en un árbol radix, primero buscamos el prefijo común más largo entre la cadena y el nodo raíz. Si el prefijo común más largo es el mismo que la cadena, insertamos la cadena en el árbol en el nodo raíz. De lo contrario, insertamos la cadena en el árbol en el nodo que corresponde al prefijo común más largo.

Para buscar una cadena en un árbol radix, primero buscamos el prefijo común más largo entre la cadena y el nodo raíz. Si el prefijo común más largo es el mismo que la cadena, devolvemos el nodo raíz. De lo contrario, buscamos la cadena en el subárbol que corresponde al prefijo común más largo.

## 3. Ejemplos de código

### 3.1 Insertar

```c
void insert(Node* root, char* str) {
  int i, j, k;
  Node* cur = root;
  for (i = 0; str[i] != '\0'; i++) {
    for (j = 0; j < cur->n; j++) {
      if (cur->children[j]->c == str[i]) {
        cur = cur->children[j];
        break;
      }
    }
    if (j == cur->n) {
      Node* newNode = malloc(sizeof(Node));
      newNode->c = str[i];
      newNode->n = 1;
      cur->children[cur->n] = newNode;
      cur->n++;
    }
  }
}
```

### 3.2 Buscar

```c
Node* search(Node* root, char* str) {
  int i, j;
  Node* cur = root;
  for (i = 0; str[i] != '\0'; i++) {
    for (j = 0; j < cur->n; j++) {
      if (cur->children[j]->c == str[i]) {
        cur = cur->children[j];
        break;
      }
    }
    if (j == cur->n) {
      return NULL;
    }
  }
  return cur;
}
```

## 4. Ejercicios

1. Implemente el algoritmo del árbol radix en su lenguaje de programación favorito.

2. Use el algoritmo del árbol radix para almacenar una lista de palabras en inglés.

3. Use el algoritmo del árbol radix para almacenar una lista de cadenas de ADN.

## 5. Respuestas

1. Consulte los ejemplos de código anteriores.

2. Consulte el ejemplo de código 3.2.

3. Consulte el ejemplo de código 3.1.