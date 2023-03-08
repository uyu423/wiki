---
title: [Lenguaje C] 025: Búsqueda en profundidad primero
description: 
published: true
date: 2023-02-10T13:55:50.463Z
tags: 
editor: markdown
dateCreated: 2023-02-10T13:55:44.199Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 025: Depth-First Search***English** document is available*](/en/Knowledge-base/Algorithm/c-language-025-depth-first-search)
{.links-list}


# 025: Búsqueda en profundidad primero

## Introducción

En esta publicación, analizaremos la búsqueda en profundidad (DFS), una técnica para atravesar árboles o gráficos. Cubriremos el concepto y la teoría detrás de DFS, ejemplos de código y ejercicios relacionados.

## Concepto y Teoría

DFS es una técnica para atravesar un árbol o gráfico. El algoritmo comienza en el nodo raíz y explora lo más lejos posible a lo largo de cada rama antes de retroceder.

La principal diferencia entre DFS y otros algoritmos transversales de árboles, como la búsqueda en amplitud (BFS), es el orden en que se visitan los nodos. En BFS, los nodos se visitan primero en amplitud, lo que significa que todos los nodos del mismo nivel se visitan antes de pasar al siguiente nivel. En DFS, los nodos se visitan primero en profundidad, lo que significa que el algoritmo explora en la medida de lo posible cada rama antes de pasar a la siguiente rama.

El siguiente es un ejemplo simple de DFS. Considere el siguiente árbol:

![árbol](https://raw.githubusercontent.com/Algorithm-DataStructure-Blog/Algorithm-DataStructure-Blog.github.io/master/img/tree.png)

Si usáramos DFS para atravesar este árbol, comenzaríamos en el nodo raíz (A) y exploraríamos la rama izquierda lo más lejos posible. Esto nos llevaría a los nodos D y E. Luego regresaríamos al nodo C y exploraríamos la rama derecha, lo que nos llevaría al nodo F. Luego regresaríamos al nodo B y exploraríamos la rama izquierda, que nos llevaría a nodo G. Luego regresaríamos al nodo A y exploraríamos la rama derecha, que nos llevaría al nodo H. Luego regresaríamos al nodo raíz y nos detendríamos, ya que no hay más nodos para explorar.

El orden en que se visitan los nodos en este ejemplo es: A, B, G, C, F, D, E, H.

## Ejemplos de código

Ahora que hemos cubierto el concepto y la teoría detrás de DFS, veamos algunos ejemplos de código.

La siguiente es una implementación simple de DFS en C++. Usaremos el mismo árbol del ejemplo anterior.

```C++
void dfs(Node* root) {
    if (root == nullptr) {
        return;
    }

    // visit the root
    cout << root->val << " ";

    // visit the left subtree
    dfs(root->left);

    // visit the right subtree
    dfs(root->right);
}
```

En este ejemplo, estamos usando una implementación recursiva de DFS. El algoritmo comienza en el nodo raíz y visita recursivamente los subárboles izquierdo y derecho.

La siguiente es una implementación no recursiva de DFS en C++.

```C++
void dfs(Node* root) {
    if (root == nullptr) {
        return;
    }

    stack<Node*> st;
    st.push(root);

    while (!st.empty()) {
        Node* curr = st.top();
        st.pop();

        // visit the node
        cout << curr->val << " ";

        // push the right child first
        // so that it will be processed last
        if (curr->right != nullptr) {
            st.push(curr->right);
        }

        // push the left child
        if (curr->left != nullptr) {
            st.push(curr->left);
        }
    }
}
```

En este ejemplo, estamos utilizando una implementación iterativa de DFS. Estamos utilizando una pila para realizar un seguimiento de los nodos que deben procesarse. Empujamos el nodo raíz a la pila y luego sacamos los nodos de la pila hasta que esté vacío.

## Ejercicios

Ahora que hemos visto algunos ejemplos de código, probemos algunos ejercicios.

1. Recorra el siguiente árbol usando DFS e imprima el valor de cada nodo:

![árbol2](https://raw.githubusercontent.com/Algorithm-DataStructure-Blog/Algorithm-DataStructure-Blog.github.io/master/img/tree2.png)

2. Recorra el siguiente gráfico usando DFS e imprima el valor de cada nodo:

![gráfico](https://raw.githubusercontent.com/Algorithm-DataStructure-Blog/Algorithm-DataStructure-Blog.github.io/master/img/graph.png)

## Respuestas

1. El orden en que se visitan los nodos es: A, B, D, E, C, F, G, H, I.

2. El orden en que se visitan los nodos es: A, B, D, F, E, G, C, H.