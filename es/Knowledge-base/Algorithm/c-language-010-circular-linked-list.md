---
title: [Lenguaje C] 010: Lista enlazada circular
description: 
published: true
date: 2023-02-10T13:17:44.965Z
tags: 
editor: markdown
dateCreated: 2023-02-10T13:17:38.753Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 010: Circular Linked List***English** document is available*](/en/Knowledge-base/Algorithm/c-language-010-circular-linked-list)
{.links-list}


# Lista enlazada circular

Una lista enlazada circular es una variación de una lista enlazada en la que el último nodo de la lista apunta hacia el primer nodo, formando un bucle. Este tipo de lista es útil para aplicaciones en las que es necesario recorrer la lista de forma rotativa, como en un programador de juegos o sistema operativo.

## Concepto

Una lista enlazada circular es una estructura de datos que contiene una secuencia de nodos. Cada nodo contiene un valor y un puntero al siguiente nodo de la secuencia. El último nodo de la secuencia apunta hacia el primer nodo, formando un bucle.

La ventaja de una lista enlazada circular sobre una lista enlazada lineal es que se puede recorrer de forma circular. Esto lo convierte en una estructura de datos adecuada para aplicaciones como programadores de juegos o sistemas operativos.

## Ejemplos de código

Aquí hay un ejemplo de una lista enlazada circular en el lenguaje de programación C:

```c
struct node {
   int data;
   struct node *next;
};

struct node *head = NULL;

void insert_node(int data) {
   struct node *new_node = malloc(sizeof(struct node));
   new_node->data = data;
   new_node->next = head;
   if (head != NULL) {
      struct node *temp = head;
      while (temp->next != head) {
         temp = temp->next;
      }
      temp->next = new_node;
   } else {
      new_node->next = new_node;
   }
   head = new_node;
}

void delete_node(int data) {
   if (head == NULL) {
      return;
   }
   if (head->next == head && head->data == data) {
      free(head);
      head = NULL;
      return;
   }
   struct node *temp = head;
   while (temp->next != head && temp->next->data != data) {
      temp = temp->next;
   }
   if (temp->next->data == data) {
      struct node *to_be_deleted = temp->next;
      if (to_be_deleted == head) {
         head = to_be_deleted->next;
      }
      temp->next = to_be_deleted->next;
      free(to_be_deleted);
   }
}

void print_list() {
   if (head == NULL) {
      printf("List is empty\n");
      return;
   }
   struct node *temp = head;
   printf("List: ");
   do {
      printf("%d ", temp->data);
      temp = temp->next;
   } while (temp != head);
   printf("\n");
}

int main() {
   insert_node(1);
   insert_node(2);
   insert_node(3);
   insert_node(4);
   print_list();
   delete_node(2);
   print_list();
   delete_node(1);
   print_list();
   delete_node(4);
   print_list();
   delete_node(3);
   print_list();
   return 0;
}
```

## Ejercicios

1. Implemente una función para verificar si una lista dada con un solo enlace es circular.

2. Implemente una función para encontrar el nodo medio de una lista enlazada simple dada.

3. Implemente una función para encontrar el enésimo nodo desde el final de una lista enlazada simple dada.

4. Implemente una función para verificar si una lista dada de enlace único es palíndromo.

## Respuestas

1.

```c
bool is_circular(struct node *head) {
   if (head == NULL) {
      return true;
   }
   struct node *temp = head;
   while (temp->next != head) {
      temp = temp->next;
   }
   return (temp == head);
}
```

2.

```c
struct node *find_middle(struct node *head) {
   if (head == NULL) {
      return NULL;
   }
   struct node *slow_ptr = head;
   struct node *fast_ptr = head;
   while (fast_ptr->next != head && fast_ptr->next->next != head) {
      slow_ptr = slow_ptr->next;
      fast_ptr = fast_ptr->next->next;
   }
   return slow_ptr;
}
```

3.

```c
struct node *find_nth_from_end(struct node *head, int n) {
   if (head == NULL || n <= 0) {
      return NULL;
   }
   struct node *slow_ptr = head;
   struct node *fast_ptr = head;
   int i;
   for (i = 0; i < n; i++) {
      if (fast_ptr->next == head) {
         return NULL;
      }
      fast_ptr = fast_ptr->next;
   }
   while (fast_ptr != head) {
      slow_ptr = slow_ptr->next;
      fast_ptr = fast_ptr->next;
   }
   return slow_ptr;
}
```

4.

```c
bool is_palindrome(struct node *head) {
   if (head == NULL) {
      return true;
   }
   struct node *slow_ptr = head;
   struct node *fast_ptr = head;
   struct node *prev_slow_ptr = head;
   struct node *mid_node = NULL;
   bool is_even = true;
   while (fast_ptr->next != head && fast_ptr->next->next != head) {
      fast_ptr = fast_ptr->next->next;
      prev_slow_ptr = slow_ptr;
      slow_ptr = slow_ptr->next;
   }
   if (fast_ptr->next->next == head) {
      is_even = false;
   }
   if (is_even) {
      mid_node = slow_ptr;
      slow_ptr = slow_ptr->next;
   }
   struct node *second_half = slow_ptr;
   prev_slow_ptr->next = head;
   struct node *prev_of_curr = second_half;
   struct node *curr = second_half->next;
   while (curr != head) {
      struct node *next = curr->next;
      curr->next = prev_of_curr;
      prev_of_curr = curr;
      curr = next;
   }
   second_half->next = prev_of_curr;
   bool is_palindrome = true;
   struct node *first_ptr = head;
   struct node *second_ptr = second_half;
   while (first_ptr != second_half) {
      if (first_ptr->data != second_ptr->data) {
         is_palindrome = false;
         break;
      }
      first_ptr = first_ptr->next;
      second_ptr = second_ptr->next;
   }
   prev_of_curr = second_half->next;
   curr = prev_of_curr->next;
   while (curr != second_half) {
      struct node *next = curr->next;
      curr->next = prev_of_curr;
      prev_of_curr = curr;
      curr = next;
   }
   if (is_even) {
      mid_node->next = second_half;
   } else {
      head->next = second_half;
   }
   return is_palindrome;
}
```

## Comentario

Las listas enlazadas circulares son una estructura de datos útil para aplicaciones en las que es necesario recorrer la lista de forma rotativa. Son fáciles de implementar y pueden ser una alternativa a los arreglos que ahorra espacio.