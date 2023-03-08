---
title: [Lenguaje C] 009: Lista de enlaces dobles
description: 
published: true
date: 2023-02-12T20:33:46.901Z
tags: 
editor: markdown
dateCreated: 2023-02-12T20:33:39.907Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 009: Double Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-009-double-linked-list)
{.links-list}


# C Language 009: Lista de enlaces dobles

Una lista de doble enlace es una estructura de datos que consta de un conjunto de nodos conectados entre sí de forma lineal. Cada nodo contiene dos campos, llamados enlaces, que apuntan a los nodos anterior y siguiente de la lista. El primer nodo, llamado cabeza, apunta al último nodo, llamado cola.

Una lista doblemente enlazada se puede recorrer en ambas direcciones, de la cabeza a la cola y de la cola a la cabeza. También es posible insertar y eliminar nodos en cualquier punto de la lista.

El siguiente ejemplo de código muestra cómo crear una lista de doble enlace en C:

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node* next;
    struct node* prev;
};

struct node* head; // global variable - pointer to the head node.

// Create a new node and return its address.
struct node* getnode() {
    struct node* newnode = (struct node*)malloc(sizeof(struct node));
    newnode->data = 0;
    newnode->next = NULL;
    newnode->prev = NULL;
    return newnode;
}

// Insert a new node at the head of the list.
void insert_at_head(int x) {
    struct node* newnode = getnode();
    newnode->data = x;
    newnode->next = head;
    if(head != NULL)
        head->prev = newnode;
    head = newnode;
}

// Insert a new node at the tail of the list.
void insert_at_tail(int x) {
    struct node* newnode = getnode();
    newnode->data = x;
    newnode->next = NULL;
    if(head == NULL) {
        newnode->prev = NULL;
        head = newnode;
        return;
    }
    struct node* temp = head;
    while(temp->next != NULL)
        temp = temp->next;
    temp->next = newnode;
    newnode->prev = temp;
}

// Traverse the list from head to tail and print the data of each node.
void print_from_head() {
    struct node* temp = head;
    printf("\nPrinting from head:\n");
    while(temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}

// Traverse the list from tail to head and print the data of each node.
void print_from_tail() {
    struct node* temp = head;
    if(temp == NULL) return; // empty list
    // go to the last node
    while(temp->next != NULL)
        temp = temp->next;
    // print from tail
    printf("\nPrinting from tail:\n");
    while(temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->prev;
    }
    printf("\n");
}

// Delete the first node of the list.
void delete_at_head() {
    if(head == NULL) return; // empty list
    struct node* temp = head;
    head = head->next; // head now points to the second node
    if(head != NULL)
        head->prev = NULL;
    free(temp); // free the memory of the first node
}

// Delete the last node of the list.
void delete_at_tail() {
    if(head == NULL) return; // empty list
    struct node* temp = head;
    if(temp->next == NULL) { // only one node in the list
        free(temp);
        head = NULL;
        return;
    }
    // go to the last node
    while(temp->next != NULL)
        temp = temp->next;
    // the second last node now points to NULL
    temp->prev->next = NULL;
    free(temp); // free the memory of the last node
}

int main() {
    head = NULL; // empty list
    insert_at_head(2);
    insert_at_head(1);
    insert_at_tail(3);
    insert_at_tail(4);
    print_from_head();
    print_from_tail();
    delete_at_head();
    delete_at_tail();
    print_from_head();
    return 0;
}
```

La salida del programa anterior es:

```
Printing from head:
1 2 3 4 

Printing from tail:
4 3 2 1 

Printing from head:
2 3 
```

Como puede ver, la lista doblemente enlazada nos permite insertar y eliminar nodos en cualquier punto de la lista. También podemos recorrer la lista en ambas direcciones.

Hay muchas aplicaciones de listas doblemente enlazadas. Por ejemplo, se pueden usar para implementar colas y pilas.

## Ejercicios

1. Implemente una función para eliminar un nodo en una posición dada en una lista de doble enlace.

2. Implemente una función para invertir una lista de doble enlace.

3. Implemente una función para verificar si una lista dada de enlaces simples es un palíndromo o no.

4. Implemente una función para eliminar todos los nodos duplicados de una lista ordenada de doble enlace.

5. Implemente una función para eliminar todos los nodos duplicados de una lista de enlaces dobles sin clasificar.

6. Implemente una función para encontrar el nodo medio de una lista doble enlazada.

7. Implemente una función para contar el número de veces que aparece un int dado en una lista de doble enlace.

8. Implemente una función para insertar un nodo en una lista ordenada de doble enlace.

9. Implemente una función para eliminar todas las ocurrencias de un int dado de una lista de doble enlace.

10. Implemente una función para dividir una lista doblemente enlazada en dos mitades.

## Respuestas

1.

```c
void delete_at_position(int position) {
    if(head == NULL) return; // empty list
    if(position == 1) { // first node
        delete_at_head();
        return;
    }
    int i;
    struct node* temp = head;
    for(i=1; i<position-1 && temp!=NULL; i++)
        temp = temp->next;
    if(temp == NULL || temp->next == NULL) return; // position does not exist
    // temp->next is the node to be deleted
    struct node* next = temp->next->next;
    free(temp->next); // free the memory of the node to be deleted
    temp->next = next;
    if(next != NULL)
        next->prev = temp;
}
```

2.

```c
void reverse() {
    if(head == NULL) return; // empty list
    struct node* temp = head;
    struct node* next;
    while(temp != NULL) {
        next = temp->next;
        temp->next = temp->prev;
        temp->prev = next;
        head = temp;
        temp = next;
    }
}
```

3.

```c
// Return 1 if the list is a palindrome, 0 otherwise.
int is_palindrome(struct node* head) {
    if(head == NULL) return 1; // empty list is a palindrome
    struct node* slow = head;
    struct node* fast = head;
    // use slow and fast pointers to find the middle of the list
    while(fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }
    // slow is now pointing to the middle node
    // reverse the second half of the list
    struct node* second_half = NULL;
    struct node* temp = NULL;
    while(slow != NULL) {
        temp = slow->next;
        slow->next = second_half;
        second_half = slow;
        slow = temp;
    }
    // head and second_half now point to the first and second halves of the list
    // compare the two halves for equality
    while(second_half != NULL) {
        if(head->data != second_half->data)
            return 0; // not a palindrome
        head = head->next;
        second_half = second_half->next;
    }
    return 1; // list is a palindrome
}
```

4.

```c
// Delete all duplicate nodes from a sorted list.
void delete_duplicates(struct node* head) {
    if(head == NULL) return; // empty list
    struct node* temp = head;
    // compare each node with its next node
    while(temp->next != NULL) {
        if(temp->data == temp->next->data) {
            // duplicate node found, delete it
            struct node* next = temp->next->next;
            free(temp->next); // free the memory of the duplicate node
            temp->next = next;
            if(next != NULL)
                next->prev = temp;
        }
        else {
            temp = temp->next;
        }
    }
}
```

5.

```c
// Delete all duplicate nodes from an unsorted list.
void delete_duplicates(struct node* head) {
    if(head == NULL) return; // empty list
    struct node* temp1 = head;
    // compare each node with every other node in the list
    while(temp1->next != NULL) {
        struct node* temp2 = temp1->next;
        while(temp2 != NULL) {
            if(temp1->data == temp2->data) {
                // duplicate node found, delete it
                struct node* next = temp2->next;
                free(temp2); // free the memory of the duplicate node
                temp2 = next;
                if(next != NULL)
                    next->prev = temp1;
            }
            else {
                temp2 = temp2->next;
            }
        }
        temp1 = temp1->next;
    }
}
```

6.

```c
// Return the address of the middle node of the list.
struct node* find_middle() {
    if(head == NULL) return NULL; // empty list
    struct node* slow = head;
    struct node* fast = head;
    // use slow and fast pointers to find the middle of the list
    while(fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }
    // slow is now pointing to the middle node
    return slow;
}
```

7.

```c
// Return the number of times x occurs in the list.
int count(int x) {
    if(head == NULL) return 0; // empty list
    int count = 0;
    struct node* temp = head;
    while(temp != NULL) {
        if(temp->data == x)
            count++;
        temp = temp->next;
    }
    return count;
}
```

8.

```c
// Insert a new node with data x in a sorted list.
void insert(int x) {
    if(head == NULL) { // empty list
        insert_at_head(x);
        return;
    }
    struct node* temp = head;
    struct node* prev = NULL;
    // find the position to insert the new node
    while(temp != NULL && temp->data < x) {
        prev = temp;
        temp = temp->next;
    }
    // temp is now pointing to the node after the insertion position
    // prev is pointing to the node before the insertion position
    if(prev == NULL) { // insert at the head
        insert_at_head(x);
    }
    else {
        // insert the new node between prev and temp
        struct node* newnode = getnode();
        newnode->data = x;
        newnode->next = temp;
        newnode->prev = prev;
        prev->next = newnode;
        if(temp != NULL)
            temp->prev = newnode;
    }
}
```

9.

```c
// Remove all occurrences of x from the list.
void remove(int x) {
    if(head == NULL) return; // empty list
    struct node* temp = head;
    // compare each node with x
    while(temp != NULL) {
        if(temp->data == x) {
            // node to be removed
            if(temp == head) { // head node
                delete_at_head();
            }
            else {
                struct node* prev = temp->prev;
                struct node* next = temp->next;
                prev->next = next;
                if(next != NULL)
                    next->prev = prev;
                free(temp); // free the memory of the node to be removed
            }
        }
        temp = temp->next;
    }
}
```

10

```c
// Split the list into two halves.
// Return the address of the second half of the list.
struct node* split() {
    if(head == NULL) return NULL; // empty list
    struct node* slow = head;
    struct node* fast = head;
    // use slow and fast pointers to find the middle of the list
    while(fast != NULL && fast->next != NULL) {
        slow = slow->next;
        fast = fast->next->next;
    }
    // slow is now pointing to the middle node
    // the second half of the list starts from slow->next
    struct node* second_half = slow->next;
    if(second_half != NULL)
        second_half->prev = NULL;
    slow->next = NULL; // first half of the list ends at slow
    return second_half;
}
```