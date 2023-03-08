---
title: [Lenguaje C] 041: Montón de Fibonacci
description: 
published: true
date: 2023-02-13T21:32:52.990Z
tags: 
editor: markdown
dateCreated: 2023-02-13T21:32:51.263Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 041: Fibonacci Heap***English** document is available*](/en/Knowledge-base/Algorithm/c-language-041-fibonacci-heap)
{.links-list}


# Montón de Fibonacci

En informática, un montón de Fibonacci es una estructura de datos para operaciones de cola de prioridad, que consta de una colección de árboles ordenados por montón. Tiene un mejor tiempo de ejecución amortizado que muchas otras estructuras de datos de cola de prioridad, incluido el montón binario y el montón binomial. Michael L. Fredman y Robert E. Tarjan desarrollaron montones de Fibonacci en 1984 y los publicaron en una revista científica en 1987.

Los montones de Fibonacci llevan el nombre de los números de Fibonacci, que se utilizan en su análisis de tiempo de ejecución. Los montones de Fibonacci tienen un tiempo de ejecución amortizado asintóticamente mejor que los montones binomiales y los montones binarios.

Un montón de Fibonacci es una colección de árboles que satisfacen la propiedad min-heap, en la que la clave de cada nodo es menor o igual que la clave de su padre. Además, cada nodo tiene un grado, que es el número de hijos de ese nodo. Un montón de Fibonacci se compone de un conjunto de árboles, cada uno de los cuales es un montón mínimo.

La clave mínima de un montón de Fibonacci es la clave del nodo raíz del árbol. Cada nodo tiene un puntero a su padre, si lo hay. Si un nodo no tiene padre, entonces es el nodo raíz de su árbol y es miembro del montón de Fibonacci.

Un montón de Fibonacci es una estructura de datos para operaciones de cola de prioridad, que consta de una colección de árboles ordenados por montón. Tiene un mejor tiempo de ejecución amortizado que muchas otras estructuras de datos de cola de prioridad, incluido el montón binario y el montón binomial. Michael L. Fredman y Robert E. Tarjan desarrollaron montones de Fibonacci en 1984 y los publicaron en una revista científica en 1987.

Los montones de Fibonacci llevan el nombre de los números de Fibonacci, que se utilizan en su análisis de tiempo de ejecución. Los montones de Fibonacci tienen un tiempo de ejecución amortizado asintóticamente mejor que los montones binomiales y los montones binarios.

Un montón de Fibonacci es una colección de árboles que satisfacen la propiedad min-heap, en la que la clave de cada nodo es menor o igual que la clave de su padre. Además, cada nodo tiene un grado, que es el número de hijos de ese nodo. Un montón de Fibonacci se compone de un conjunto de árboles, cada uno de los cuales es un montón mínimo.

La clave mínima de un montón de Fibonacci es la clave del nodo raíz del árbol. Cada nodo tiene un puntero a su padre, si lo hay. Si un nodo no tiene padre, entonces es el nodo raíz de su árbol y es miembro del montón de Fibonacci.

Las operaciones en un montón de Fibonacci toman un tiempo logarítmico, con un factor constante de O(1), excepto la operación de disminución de clave, que toma un tiempo logarítmico amortizado.

El montón de Fibonacci fue la primera estructura de datos del montón en tener un límite de tiempo logarítmico amortizado para todas las operaciones.

## Operaciones

Las operaciones en un montón de Fibonacci toman un tiempo logarítmico, con un factor constante de O(1), excepto la operación de disminución de clave, que toma un tiempo logarítmico amortizado.

El montón de Fibonacci fue la primera estructura de datos del montón en tener un límite de tiempo logarítmico amortizado para todas las operaciones.

Las operaciones en un montón de Fibonacci son:

- insertar: inserta un nuevo nodo en el montón con una clave determinada.
- mínimo: devuelve el nodo con la clave mínima.
- extractMin: elimina y devuelve el nodo con la clave mínima.
- unión: crea un montón nuevo que es la unión de dos montones dados.
- eliminar: elimina un nodo del montón.
- disminuirKey: disminuye la clave de un nodo dado.

## Ejemplo de código

Aquí hay un ejemplo de implementación de un montón de Fibonacci en el lenguaje de programación C.

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int key;
    struct node *parent;
    struct node *child;
    struct node *sibling;
};

struct heap {
    struct node *min;
    int n;
};

struct heap *make_heap()
{
    struct heap *h = malloc(sizeof(struct heap));
    h->min = NULL;
    h->n = 0;
    return h;
}

struct node *make_node(int key)
{
    struct node *x = malloc(sizeof(struct node));
    x->key = key;
    x->parent = NULL;
    x->child = NULL;
    x->sibling = NULL;
    return x;
}

void heap_insert(struct heap *h, struct node *x)
{
    x->sibling = h->min;
    if (h->min != NULL) {
        h->min->parent = x;
    }
    h->min = x;
    h->n++;
}

struct node *heap_minimum(struct heap *h)
{
    return h->min;
}

struct node *heap_extract_min(struct heap *h)
{
    struct node *z = h->min;
    if (z != NULL) {
        struct node *x = z->child;
        struct node *y;
        while (x != NULL) {
            y = x->sibling;
            x->sibling = z->sibling;
            x->parent = NULL;
            z->sibling = x;
            x = y;
        }
        h->min = z->sibling;
        if (z == h->min) {
            h->min = NULL;
        }
        h->n--;
    }
    return z;
}

void heap_union(struct heap *h1, struct heap *h2)
{
    struct heap *h = make_heap();
    h->min = h1->min;
    h->n = h1->n + h2->n;
    if (h1->min == NULL || (h2->min != NULL && h2->min->key < h1->min->key)) {
        h->min = h2->min;
    }
    if (h->min != NULL) {
        if (h1->min != NULL && h1->min != h2->min) {
            h1->min->sibling = h2->min->sibling;
        }
        h2->min->sibling = h1->min;
        h1->min = h2->min;
    }
    free(h2);
}

void heap_delete(struct heap *h, struct node *x)
{
    heap_decrease_key(h, x, -1);
    heap_extract_min(h);
}

void heap_decrease_key(struct heap *h, struct node *x, int k)
{
    if (k > x->key) {
        printf("error: new key is larger than current key\n");
        return;
    }
    x->key = k;
    struct node *y = x->parent;
    if (y != NULL && x->key < y->key) {
        cut(h, x, y);
        cascading_cut(h, y);
    }
    if (x->key < h->min->key) {
        h->min = x;
    }
}

void cut(struct heap *h, struct node *x, struct node *y)
{
    x->sibling = y->child;
    if (y->child != NULL) {
        y->child->parent = x;
    }
    y->child = x;
    x->parent = y;
    y->degree++;
}

void cascading_cut(struct heap *h, struct node *y)
{
    struct node *z = y->parent;
    if (z != NULL) {
        if (!y->mark) {
            y->mark = 1;
        } else {
            cut(h, y, z);
            cascading_cut(h, z);
        }
    }
}

void heap_destroy(struct heap *h)
{
    struct node *x = h->min;
    struct node *y;
    struct node *z;
    while (x != NULL) {
        y = x->child;
        while (y != NULL) {
            z = y->sibling;
            free(y);
            y = z;
        }
        z = x->sibling;
        free(x);
        x = z;
    }
    free(h);
}

int main()
{
    struct heap *h = make_heap();
    struct node *x;
    
    x = make_node(3);
    heap_insert(h, x);
    
    x = make_node(2);
    heap_insert(h, x);
    
    x = heap_extract_min(h);
    printf("%d\n", x->key);
    
    x = heap_minimum(h);
    printf("%d\n", x->key);
    
    heap_decrease_key(h, x, 1);
    
    heap_delete(h, x);
    
    heap_destroy(h);
    
    return 0;
}
```

## Ejercicios

1. Implemente las operaciones en un montón de Fibonacci en el idioma de su elección.

2. Use un montón de Fibonacci para implementar una cola de prioridad.

3. Use un montón de Fibonacci para implementar un algoritmo de árbol de expansión mínimo.

4. Use un montón de Fibonacci para implementar el algoritmo de Dijkstra.