---
title: [Lenguaje C] 011: Pila
description: 
published: true
date: 2023-02-09T09:55:46.138Z
tags: 
editor: markdown
dateCreated: 2023-02-09T09:55:39.784Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 011: Stack***English** document is available*](/en/Knowledge-base/Algorithm/c-language-011-stack)
{.links-list}


# Pila

Una pila es una estructura de datos básica que puede pensarse lógicamente como una estructura lineal representada por una pila o pila física real, que es una estructura donde los objetos se apilan uno encima del otro. El principio básico de una pila es que el último elemento que se inserta en la pila será el primero en ser eliminado.

Una pila es una estructura de datos restringida porque tiene un orden predefinido en el que se pueden realizar las operaciones. El orden está restringido a LIFO (Last In First Out).

Hay muchos ejemplos del mundo real de pilas. Algunos ejemplos son los siguientes:

- Una baraja de cartas
- Un plato de comida
- Una pila de libros.

## Implementación

Una pila se puede implementar usando una matriz o una lista enlazada. En esta publicación, discutiremos la implementación de una pila usando una matriz.

### Implementación de matrices

La implementación de una matriz de una pila es muy simple. Solo necesitamos mantener una variable que realice un seguimiento del elemento superior de la pila. El elemento superior es el último elemento que se agregó a la pila.

Las siguientes operaciones se pueden realizar en una pila:

- Empujar: esta operación agrega un elemento a la parte superior de la pila.
- Pop: esta operación elimina un elemento de la parte superior de la pila.
- Peek: esta operación devuelve el elemento en la parte superior de la pila sin eliminarlo.
- isEmpty: esta operación devuelve verdadero si la pila está vacía, falso en caso contrario.

La siguiente es la implementación de una pila usando una matriz en el lenguaje de programación C:

```c
#include <stdio.h>
#include <stdlib.h>
 
#define MAXSIZE 10
 
struct stack
{
    int top;
    int items[MAXSIZE];
};
 
struct stack* createStack()
{
    struct stack* s = (struct stack*) malloc(sizeof(struct stack));
    s->top = -1;
    return s;
}
 
int isEmpty(struct stack* s)
{
    return (s->top == -1);
}
 
int peek(struct stack* s)
{
    if (!isEmpty(s))
        return s->items[s->top];
    return -1;
}
 
void push(struct stack* s, int x)
{
    if (s->top == MAXSIZE-1)
    {
        printf("Stack overflow\n");
        return;
    }
    s->items[++s->top] = x;
}
 
int pop(struct stack* s)
{
    if (isEmpty(s))
    {
        printf("Stack underflow\n");
        return -1;
    }
    return s->items[s->top--];
}
 
int main()
{
    struct stack* s = createStack();
    push(s, 1);
    push(s, 2);
    push(s, 3);
    printf("%d popped from stack\n", pop(s));
    printf("Top element is %d\n", peek(s));
    return 0;
}
```

Producción:

```
3 popped from stack
Top element is 2
```

En el programa anterior, hemos creado una pila de tamaño MAXSIZE=10. La variable superior almacena el índice del elemento superior de la pila. La operación de inserción agrega un elemento a la parte superior de la pila y la operación de extracción elimina un elemento de la parte superior de la pila. La operación peek devuelve el elemento en la parte superior de la pila sin eliminarlo. La operación isEmpty devuelve verdadero si la pila está vacía, falso en caso contrario.

## Aplicaciones

Las pilas tienen muchas aplicaciones en informática. Algunas de las aplicaciones de las pilas son las siguientes:

- Análisis: Las pilas se utilizan en el análisis. Por ejemplo, cuando se proporciona una expresión aritmética como "3 + ((5*9) + 2)", se puede analizar mediante una pila.
- Retroceso: Las pilas se utilizan en el retroceso. Por ejemplo, cuando se da un laberinto, podemos usar una pila para realizar un seguimiento del camino y retroceder cuando lleguemos a un callejón sin salida.
- Operaciones de deshacer en editores de texto: las pilas se utilizan para implementar operaciones de deshacer en editores de texto. Por ejemplo, cuando escribimos un carácter, se coloca en una pila. Cuando presionamos el botón de deshacer, el carácter superior se extrae de la pila.
- Evaluación y conversión de expresiones: las pilas se utilizan en la evaluación de expresiones en notación infija y conversión a notación postfija.