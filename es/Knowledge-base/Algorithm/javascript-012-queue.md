---
title: [JavaScript] 012: Cola
description: 
published: true
date: 2023-02-09T14:32:49.046Z
tags: 
editor: markdown
dateCreated: 2023-02-09T14:32:47.398Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 012: Queue***English** document is available*](/en/Knowledge-base/Algorithm/javascript-012-queue)
{.links-list}


# JavaScript 012: Cola

Una cola es una estructura de datos que almacena elementos en forma de primero en entrar, primero en salir (FIFO). Es decir, el primer elemento agregado a la cola será el primer elemento eliminado de la cola. Una cola a veces se denomina lista de primero en entrar, primero en salir (FIFO).

Una analogía común a una cola es una fila en un banco. La primera persona en la fila es la primera en ser atendida y la última persona en la fila es la última en ser atendida.

Una cola tiene dos operaciones principales: poner en cola y quitar de la cola. Enqueue agrega un elemento al final de la cola y dequeue elimina un elemento del frente de la cola.

## Implementación

Hay muchas maneras de implementar una cola. La forma más común es usar una matriz.

### Implementación de matrices

La forma más sencilla de implementar una cola es usar una matriz. El primer elemento de la matriz es el frente de la cola y el último elemento de la matriz es la parte posterior de la cola.

#### Poner en cola

Para poner en cola un elemento, agregamos el elemento al final de la matriz.

```javascript
function enqueue(item) {
  queue.push(item);
}
```

#### Quitar de la cola

Para sacar un elemento de la cola, eliminamos el primer elemento de la matriz.

```javascript
function dequeue() {
  return queue.shift();
}
```

### Implementación de listas enlazadas

Una forma más eficiente de implementar una cola es usar una lista enlazada. Con una lista enlazada, podemos evitar la costosa operación de cambiar todos los elementos de la matriz cuando sacamos un elemento de la cola.

#### Poner en cola

Para poner en cola un elemento, lo agregamos al final de la lista vinculada.

```javascript
function enqueue(item) {
  var node = {
    data: item,
    next: null
  };

  if (queue.length === 0) {
    queue.head = node;
  } else {
    queue.tail.next = node;
  }

  queue.tail = node;
}
```

#### Quitar de la cola

Para eliminar un elemento de la cola, eliminamos el primer elemento de la lista vinculada.

```javascript
function dequeue() {
  var node = queue.head;

  if (queue.length === 1) {
    queue.tail = null;
  }

  queue.head = node.next;
  queue.length--;

  return node.data;
}
```

## Complejidad del tiempo

La complejidad temporal de las implementaciones de una cola tanto de matriz como de lista enlazada es O(1). Es decir, tanto poner como quitar la cola son operaciones de tiempo constante.

## Ejemplos

Estos son algunos ejemplos del uso de una cola.

### Ejemplo 1: cola de números

En este ejemplo, crearemos una cola de números. Pondremos en cola los números del 0 al 9 en orden. Luego sacaremos de la cola e imprimiremos cada número hasta que la cola esté vacía.

```javascript
var queue = [];

for (var i = 0; i < 10; i++) {
  enqueue(i);
}

while (queue.length > 0) {
  console.log(dequeue());
}
```

Ejecutar el código anterior imprimirá los números del 0 al 9 en orden.

### Ejemplo 2: simulación de una cola de impresión

En este ejemplo, simularemos una cola de impresión. Tendremos una cola de trabajos de impresión y cada trabajo tendrá una prioridad. El trabajo con la prioridad más alta se eliminará primero.

```javascript
var queue = [];

function enqueue(item, priority) {
  var node = {
    data: item,
    priority: priority,
    next: null
  };

  if (queue.length === 0) {
    queue.head = node;
  } else {
    var current = queue.head;
    var previous;

    while (current && current.priority >= node.priority) {
      previous = current;
      current = current.next;
    }

    if (!previous) {
      node.next = queue.head;
      queue.head = node;
    } else {
      node.next = current;
      previous.next = node;
    }
  }

  queue.length++;
}

function dequeue() {
  var node = queue.head;
  queue.head = node.next;
  queue.length--;
  return node.data;
}

enqueue('A', 1);
enqueue('B', 2);
enqueue('C', 3);
enqueue('D', 4);
enqueue('E', 5);

console.log(dequeue()); // A
console.log(dequeue()); // B
console.log(dequeue()); // C
console.log(dequeue()); // D
console.log(dequeue()); // E
```

Al ejecutar el código anterior, se imprimirán las letras de la A a la E en orden.