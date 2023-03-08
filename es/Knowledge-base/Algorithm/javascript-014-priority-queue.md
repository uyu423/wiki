---
title: [JavaScript] 014: cola de prioridad
description: 
published: true
date: 2023-02-09T16:32:46.529Z
tags: 
editor: markdown
dateCreated: 2023-02-09T16:32:40.308Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 014: Priority Queue***English** document is available*](/en/Knowledge-base/Algorithm/javascript-014-priority-queue)
{.links-list}


# cola de prioridad

Una cola de prioridad es una estructura de datos donde cada elemento tiene una "prioridad" asociada. Los elementos con mayor prioridad se procesan antes que los elementos con menor prioridad.

En una cola de prioridad, el elemento con la prioridad más alta siempre está al frente de la cola. Cuando los elementos tienen la misma prioridad, se procesan en el orden en que se agregaron a la cola.

## Implementación

Hay muchas formas de implementar una cola de prioridad. Una forma es usar una matriz.

```javascript
function PriorityQueue() {
  this.items = [];
}

PriorityQueue.prototype.enqueue = function(item, priority) {
  this.items.push({item: item, priority: priority});
};

PriorityQueue.prototype.dequeue = function() {
  return this.items.shift();
};

PriorityQueue.prototype.isEmpty = function() {
  return this.items.length === 0;
};
```

Otra forma de implementar una cola de prioridad es usar un montón mínimo. Un montón mínimo es un árbol binario donde el nodo raíz es el elemento con la prioridad más baja. Los nodos secundarios izquierdo y derecho de un nodo principal son elementos con una prioridad más alta que el nodo principal.

```javascript
function Heap() {
  this.items = [];
}

Heap.prototype.enqueue = function(item, priority) {
  this.items.push({item: item, priority: priority});
  this.heapifyUp();
};

Heap.prototype.dequeue = function() {
  var item = this.items[0];
  this.items[0] = this.items[this.items.length - 1];
  this.items.pop();
  this.heapifyDown();
  return item;
};

Heap.prototype.heapifyUp = function() {
  var index = this.items.length - 1;
  var parentIndex = Math.floor((index - 1) / 2);
  var item = this.items[index];
  while(index > 0 && this.items[parentIndex].priority > item.priority) {
    this.items[index] = this.items[parentIndex];
    index = parentIndex;
    parentIndex = Math.floor((index - 1) / 2);
  }
  this.items[index] = item;
};

Heap.prototype.heapifyDown = function() {
  var index = 0;
  var leftChildIndex = 2 * index + 1;
  var rightChildIndex = 2 * index + 2;
  var item = this.items[index];
  while(leftChildIndex < this.items.length) {
    var minIndex = index;
    if(this.items[leftChildIndex].priority < item.priority) {
      minIndex = leftChildIndex;
    }
    if(rightChildIndex < this.items.length && this.items[rightChildIndex].priority < this.items[minIndex].priority) {
      minIndex = rightChildIndex;
    }
    if(minIndex !== index) {
      this.items[index] = this.items[minIndex];
      index = minIndex;
      leftChildIndex = 2 * index + 1;
      rightChildIndex = 2 * index + 2;
    } else {
      break;
    }
  }
  this.items[index] = item;
};

Heap.prototype.isEmpty = function() {
  return this.items.length === 0;
};
```

## Uso

Las colas de prioridad se pueden utilizar para una variedad de propósitos. Un uso común es para programar. Por ejemplo, una cola de prioridad se puede usar para programar tareas para que las ejecute una computadora.

Las tareas que son más importantes (p. ej., tareas con una prioridad más alta) se pueden programar para que se ejecuten antes que las tareas que son menos importantes (p. ej., tareas con una prioridad más baja).

Otro uso común para las colas de prioridad es en algoritmos que necesitan procesar datos que están "cerca" de un objetivo determinado. Por ejemplo, el algoritmo de búsqueda de rutas A* utiliza una cola de prioridad para encontrar la ruta más corta desde un nodo de inicio hasta un nodo de destino.

## Ejercicio

1. Implemente una cola de prioridad utilizando una matriz.

2. Implemente una cola de prioridad utilizando un montón mínimo.

3. Use una cola de prioridad para programar las tareas que debe ejecutar una computadora.

4. Use una cola de prioridad para encontrar la ruta más corta en un gráfico.