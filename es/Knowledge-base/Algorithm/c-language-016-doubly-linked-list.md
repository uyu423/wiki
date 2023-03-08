---
title: [Lenguaje C] 016: Lista doblemente enlazada
description: 
published: true
date: 2023-02-11T21:18:16.338Z
tags: 
editor: markdown
dateCreated: 2023-02-11T21:18:14.571Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 016: Doubly Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-016-doubly-linked-list)
{.links-list}


# Lista doblemente enlazada

Una lista doblemente enlazada es un tipo de lista enlazada en la que cada nodo está conectado a otros dos nodos en lugar de a uno solo. Esto permite el recorrido bidireccional de la lista.

## Concepto

Una lista doblemente enlazada es una estructura de datos que consiste en un conjunto de nodos que están interconectados por enlaces. Cada nodo contiene dos campos:

- Un campo de **datos** que almacena la información asociada al nodo.
- Un campo **siguiente** que almacena una referencia al siguiente nodo en la lista.
- Un campo **anterior** que almacena una referencia al nodo anterior en la lista.

El primer y el último nodo de una lista doblemente enlazada se denominan nodos **cabeza** y **cola**, respectivamente. El nodo principal es el primer nodo de la lista y el nodo final es el último nodo de la lista.

El campo **siguiente** del nodo final contiene una referencia al nodo principal y el campo **anterior** del nodo principal contiene una referencia al nodo final. Esto permite el recorrido bidireccional de la lista.

## Ejemplo de código

Aquí hay un ejemplo de una lista doblemente enlazada en el lenguaje de programación C:

```c
struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(int data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(int data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(curr_node->data == data) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%d ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

int main() {
    insert_node(1);
    insert_node(2);
    insert_node(3);
    insert_node(4);
    insert_node(5);

    print_list();

    delete_node(3);

    print_list();

    return 0;
}
```

## Ejercicios

1. Implementar una lista doblemente enlazada en el lenguaje de programación C.

2. Implemente las siguientes operaciones en una lista doblemente enlazada:

- Insertar un nodo al principio de la lista.
- Insertar un nodo al final de la lista.
- Eliminar un nodo de la lista.
- Buscar un nodo en la lista.
- Invertir el orden de la lista.

3. Escriba un programa que use una lista doblemente enlazada para almacenar una lista de números enteros. El programa debe permitir al usuario realizar las siguientes operaciones:

- Insertar un nuevo entero al principio de la lista.
- Insertar un nuevo entero al final de la lista.
- Eliminar un número entero de la lista.
- Buscar un número entero en la lista.
- Imprimir el contenido de la lista.

4. Escriba un programa que use una lista doblemente enlazada para almacenar una lista de cadenas. El programa debe permitir al usuario realizar las siguientes operaciones:

- Insertar una nueva cadena al principio de la lista.
- Insertar una nueva cadena al final de la lista.
- Eliminar una cadena de la lista.
- Buscar una cadena en la lista.
- Imprimir el contenido de la lista.

## Respuestas

1. La siguiente es una implementación en C de una lista doblemente enlazada:

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(int data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(int data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(curr_node->data == data) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%d ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

int main() {
    insert_node(1);
    insert_node(2);
    insert_node(3);
    insert_node(4);
    insert_node(5);

    print_list();

    delete_node(3);

    print_list();

    return 0;
}
```

2. La siguiente es una implementación en C de las operaciones en una lista doblemente enlazada:

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(int data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(int data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(curr_node->data == data) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%d ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

void reverse_list() {
    struct node* curr_node = head;
    struct node* temp_node = NULL;

    while(curr_node != NULL) {
        temp_node = curr_node->prev;
        curr_node->prev = curr_node->next;
        curr_node->next = temp_node;

        curr_node = curr_node->prev;
    }

    if(temp_node != NULL) {
        head = temp_node->prev;
    }
}

int main() {
    insert_node(1);
    insert_node(2);
    insert_node(3);
    insert_node(4);
    insert_node(5);

    print_list();

    delete_node(3);

    print_list();

    reverse_list();

    print_list();

    return 0;
}
```

3. La siguiente es una implementación en C de un programa que usa una lista doblemente enlazada para almacenar una lista de números enteros:

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(int data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(int data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(curr_node->data == data) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%d ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

int main() {
    int data;

    while(1) {
        printf("Enter an integer (Enter -1 to exit): ");
        scanf("%d", &data);

        if(data == -1) {
            break;
        }

        insert_node(data);
    }

    print_list();

    while(1) {
        printf("Enter an integer to delete (Enter -1 to exit): ");
        scanf("%d", &data);

        if(data == -1) {
            break;
        }

        delete_node(data);
    }

    print_list();

    return 0;
}
```

4. La siguiente es una implementación en C de un programa que usa una lista doblemente enlazada para almacenar una lista de cadenas:

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct node {
    char data[100];
    struct node* next;
    struct node* prev;
};

struct node* head = NULL;
struct node* tail = NULL;

void insert_node(char* data) {
    struct node* new_node = (struct node*)malloc(sizeof(struct node));
    strcpy(new_node->data, data);
    new_node->next = NULL;
    new_node->prev = NULL;

    if(head == NULL) {
        head = new_node;
        tail = new_node;
    }
    else {
        new_node->prev = tail;
        tail->next = new_node;
        tail = new_node;
    }
}

void delete_node(char* data) {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        if(strcmp(curr_node->data, data) == 0) {
            if(curr_node == head) {
                head = head->next;
                head->prev = NULL;
            }
            else if(curr_node == tail) {
                tail = tail->prev;
                tail->next = NULL;
            }
            else {
                curr_node->prev->next = curr_node->next;
                curr_node->next->prev = curr_node->prev;
            }

            free(curr_node);
            break;
        }

        curr_node = curr_node->next;
    }
}

void print_list() {
    struct node* curr_node = head;

    while(curr_node != NULL) {
        printf("%s ", curr_node->data);
        curr_node = curr_node->next;
    }

    printf("\n");
}

int main() {
    char data[100];

    while(1) {
        printf("Enter a string (Enter -1 to exit): ");
        scanf("%s", data);

        if(strcmp(data, "-1") == 0) {
            break;
        }

        insert_node(data);
    }

    print_list();

    while(1) {
        printf("Enter a string to delete (Enter -1 to exit): ");
        scanf("%s", data);

        if(strcmp(data, "-1") == 0) {
            break;
        }

        delete_node(data);
    }

    print_list();

    return 0;
}
```