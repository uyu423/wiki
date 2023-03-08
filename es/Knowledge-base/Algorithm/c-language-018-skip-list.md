---
title: [Idioma C] 018: Lista de omisión
description: 
published: true
date: 2023-02-13T02:32:45.921Z
tags: 
editor: markdown
dateCreated: 2023-02-13T02:32:38.547Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 018: Skip List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-018-skip-list)
{.links-list}


# Omitir lista

Una lista de saltos es una estructura de datos que permite una búsqueda eficiente dentro de una secuencia ordenada de elementos. Las listas de exclusión fueron descritas por primera vez por Pugh en 1990 y se ha descubierto que son muy útiles en una variedad de aplicaciones.

Una lista de saltos es una lista enlazada con un nivel adicional de punteros. La lista de saltos se construye de tal manera que cada nodo tiene un puntero al siguiente nodo en el mismo nivel, así como un puntero al siguiente nodo en el nivel inferior.

El número de niveles se elige de modo que la probabilidad de encontrar un elemento sea alta. La altura de la lista de omisión se elige de modo que el número esperado de pasos para encontrar un elemento sea logarítmico en el número de elementos de la lista.

El siguiente es un ejemplo de una lista de exclusión con seis elementos:

![](https://github.com/BryanBo-Chen/Algorithm-Data-Structure-notes/blob/master/assets/skiplist.png)

## Operaciones

La lista de omisión admite las siguientes operaciones:

- Buscar un elemento con una clave determinada.
- Insertar un elemento con una clave dada.
- Eliminar un elemento con una clave determinada.

La complejidad temporal de estas operaciones es la siguiente:

- Buscar: O(log n)
- Insertar: O (registro n)
- Borrar: O(log n)

donde n es el número de elementos en la lista de salto.

## Implementación

Una lista de omisión se puede implementar usando una lista enlazada. Cada nodo en la lista de omisión contiene una clave y punteros al siguiente nodo en el mismo nivel y al siguiente nodo en el nivel inferior.

El siguiente es un ejemplo de implementación de una lista de exclusión en C:

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
 
typedef struct node {
    int key;
    struct node *next;
    struct node *down;
} node;
 
node *create_node(int key, node *next, node *down) {
    node *n = malloc(sizeof(node));
    n->key = key;
    n->next = next;
    n->down = down;
    return n;
}
 
node *create_skip_list(int *keys, int n, int h) {
    node *head, *tail, *curr, *down;
    int i, j;
 
    head = create_node(0, NULL, NULL);
    tail = create_node(0, NULL, NULL);
    down = head;
 
    for (i = 0; i < h; i++) {
        curr = create_node(0, tail, down);
        down->next = curr;
        down = tail;
        for (j = 0; j < n; j++) {
            curr->next = create_node(keys[j], tail, NULL);
            curr = curr->next;
        }
    }
 
    return head;
}
 
void print_skip_list(node *head) {
    node *curr;
 
    while (head != NULL) {
        curr = head;
        while (curr->next != NULL) {
            printf("%d -> ", curr->next->key);
            curr = curr->next;
        }
        printf("NULL\n");
        head = head->down;
    }
}
 
node *search(node *head, int key) {
    node *curr;
 
    while (head != NULL) {
        curr = head;
        while (curr->next != NULL && curr->next->key <= key) {
            if (curr->next->key == key) {
                return curr->next;
            }
            curr = curr->next;
        }
        head = head->down;
    }
 
    return NULL;
}
 
node *insert(node *head, int key) {
    node *curr, *down, *new_node;
    int i;
 
    curr = head;
    down = NULL;
 
    while (curr != NULL) {
        while (curr->next != NULL && curr->next->key < key) {
            curr = curr->next;
        }
 
        if (curr->next != NULL && curr->next->key == key) {
            return curr->next;
        }
 
        new_node = create_node(key, curr->next, NULL);
        curr->next = new_node;
 
        if (down != NULL) {
            down->down = new_node;
        }
 
        down = new_node;
        curr = curr->down;
    }
 
    i = 0;
 
    while (rand() % 2 == 0) {
        if (i >= head->key) {
            break;
        }
 
        new_node = create_node(0, NULL, head);
        head->down = new_node;
        head = new_node;
 
        i++;
    }
 
    head->key = i;
 
    return NULL;
}
 
node *delete(node *head, int key) {
    node *curr, *down, *tmp;
 
    curr = head;
    down = NULL;
 
    while (curr != NULL) {
        while (curr->next != NULL && curr->next->key < key) {
            curr = curr->next;
        }
 
        if (curr->next == NULL || curr->next->key > key) {
            down = curr->down;
            curr = down;
            continue;
        }
 
        tmp = curr->next;
        curr->next = curr->next->next;
        free(tmp);
 
        if (down != NULL) {
            down->down = curr;
        }
 
        down = curr;
        curr = curr->down;
    }
 
    while (head->next == NULL) {
        tmp = head;
        head = head->down;
        free(tmp);
    }
 
    return head;
}
 
int main() {
    int keys[] = {1, 2, 3, 4, 5, 6};
    int n = sizeof(keys) / sizeof(keys[0]);
    int h = 3;
 
    node *head = create_skip_list(keys, n, h);
 
    print_skip_list(head);
 
    return 0;
}
```

## Ejercicios

1. Implementar las operaciones de una lista de salto.

2. Modifique las operaciones de inserción y eliminación para que devuelvan el encabezado de la lista de omisión.

3. Modifique la operación de búsqueda para que devuelva el nodo con la clave más grande menor o igual que la clave dada.

4. Modifique las operaciones de inserción y eliminación para que tomen un **puntero** de nodo como argumento e inserten o eliminen el nodo de la lista de omisión.

5. Implementar las operaciones de una lista de salto utilizando una lista doblemente enlazada.