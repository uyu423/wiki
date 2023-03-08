---
title: [JavaScript] 011: Pila
description: 
published: true
date: 2023-02-09T13:32:30.653Z
tags: 
editor: markdown
dateCreated: 2023-02-09T13:32:29.057Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 011: Stack***English** document is available*](/en/Knowledge-base/Algorithm/javascript-011-stack)
{.links-list}


# JavaScript 011: Pila

Una pila es una estructura de datos que le permite almacenar datos de forma ordenada. Puede pensar en ello como una pila de libros, donde solo puede agregar o quitar libros de la parte superior de la pila.

Las pilas se utilizan a menudo en la programación de computadoras para almacenar datos en un orden particular. Por ejemplo, cuando está escribiendo un programa que necesita realizar un seguimiento de qué función se llamó por última vez, usaría una pila.

Hay dos operaciones principales que se pueden realizar en una pila:

- **Push**: esto agrega un elemento a la parte superior de la pila.
- **Pop**: esto elimina el elemento de la parte superior de la pila.

Veamos un ejemplo para ver cómo funcionan estas operaciones.

Supongamos que tenemos una pila de números enteros. Podemos empujar los números 1, 2 y 3 a la pila en ese orden. La pila ahora se vería así:

3
2
1

Si luego sacamos la pila, el 3 se eliminaría de la parte superior y la pila ahora se vería así:

2
1

Si metemos 4 en la pila, se vería así:

4
2
1

Y si sacamos la pila de nuevo, el 4 se eliminaría y la pila se vería así:

2
1

Como puede ver, la pila siempre mantiene los datos en un orden particular. El último elemento que se añade es siempre el primero que se elimina.

Hay muchas aplicaciones de pilas. Un ejemplo es cuando estás escribiendo un compilador para un lenguaje de programación. El compilador necesita realizar un seguimiento de qué función se está llamando para que pueda generar el código correcto. Para hacer esto, utiliza una pila.

Otro ejemplo es cuando estás escribiendo un navegador web. Cuando haces clic en un enlace, el navegador necesita realizar un seguimiento de la página en la que estabas para poder volver a ella cuando hagas clic en el botón Atrás. Para hacer esto, utiliza una pila.

Las pilas también se utilizan en muchos algoritmos, como la búsqueda en profundidad.

## Implementación

Hay muchas formas de implementar una pila. Una forma es usar una matriz.

Podemos empujar un elemento a la pila agregándolo al final de la matriz. Podemos sacar un elemento de la pila eliminando el elemento del final de la matriz.

Aquí hay un código que implementa una pila usando una matriz:

```javascript
class Stack {
  constructor() {
    this.data = [];
  }

  push(element) {
    this.data.push(element);
  }

  pop() {
    return this.data.pop();
  }
}
```

Otra forma de implementar una pila es usar una lista enlazada.

Podemos empujar un elemento a la pila agregándolo al encabezado de la lista enlazada. Podemos sacar un elemento de la pila eliminando el elemento del encabezado de la lista enlazada.

Aquí hay un código que implementa una pila usando una lista enlazada:

```javascript
class Stack {
  constructor() {
    this.head = null;
  }

  push(element) {
    const node = {
      data: element,
      next: this.head
    };
    this.head = node;
  }

  pop() {
    const node = this.head;
    this.head = node.next;
    return node.data;
  }
}
```

## Complejidad del tiempo

La complejidad temporal de las operaciones push y pop es O(1).

## Complejidad espacial

La complejidad espacial de las operaciones push y pop es O(1).