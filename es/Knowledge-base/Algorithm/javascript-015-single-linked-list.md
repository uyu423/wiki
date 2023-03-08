---
title: [JavaScript] 015: lista enlazada única
description: 
published: true
date: 2023-02-09T17:33:38.570Z
tags: 
editor: markdown
dateCreated: 2023-02-09T17:33:36.929Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 015: Single Linked List***English** document is available*](/en/Knowledge-base/Algorithm/javascript-015-single-linked-list)
{.links-list}


# JavaScript 015: Lista enlazada única

Las listas enlazadas son un tipo de estructura de datos que almacena una colección de datos en nodos. Cada nodo en una lista enlazada contiene dos cosas: los datos en sí y una referencia al siguiente nodo en la lista. Las listas enlazadas se utilizan a menudo porque son fáciles de manipular y no requieren memoria adicional para almacenar los enlaces entre los nodos.

Hay dos tipos de listas enlazadas: listas con enlaces simples y listas con enlaces dobles. En una lista de enlaces simples, cada nodo solo tiene una referencia al siguiente nodo de la lista. En una lista doblemente enlazada, cada nodo tiene una referencia tanto al nodo siguiente como al nodo anterior.

## Creación de una lista vinculada

Para crear una lista enlazada, necesitamos crear una clase `Nodo`. Cada 'Nodo' tendrá dos propiedades: 'datos', que almacena los datos de ese nodo, y 'siguiente', que almacena la referencia al siguiente nodo de la lista.

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}
```

Ahora que tenemos una clase `Node`, podemos crear una clase `LinkedList`. La clase `LinkedList` tendrá dos propiedades: `head`, que almacena el primer nodo de la lista, y `tail`, que almacena el último nodo de la lista.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }
}
```

## Inserción de datos

Hay dos formas de insertar datos en una lista enlazada: al principio de la lista o al final de la lista.

### Inserción en la cabeza

Para insertar datos en el encabezado de la lista, necesitamos crear un nuevo nodo con los datos y establecer la propiedad `siguiente` del nuevo nodo en el encabezado actual de la lista. Luego, establecemos el encabezado de la lista en el nuevo nodo.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  insertAtHead(data) {
    const newNode = new Node(data);
    newNode.next = this.head;
    this.head = newNode;
  }
}
```

### Inserción en la cola

Para insertar datos al final de la lista, necesitamos crear un nuevo nodo con los datos y establecer la propiedad `siguiente` del final actual de la lista en el nuevo nodo. Luego, establecemos la cola de la lista en el nuevo nodo.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  insertAtTail(data) {
    const newNode = new Node(data);
    if (!this.head) {
      this.head = newNode;
    }
    if (this.tail) {
      this.tail.next = newNode;
    }
    this.tail = newNode;
  }
}
```

## Eliminación de datos

Hay dos formas de eliminar datos de una lista vinculada: desde el encabezado de la lista o desde el final de la lista.

### Eliminación de la cabecera

Para eliminar datos del encabezado de la lista, simplemente establecemos el encabezado de la lista en el nodo posterior al encabezado actual.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  deleteFromHead() {
    if (!this.head) {
      return;
    }
    this.head = this.head.next;
  }
}
```

### Eliminación de la cola

Para eliminar datos de la cola de la lista, debemos realizar un seguimiento del nodo antes de la cola. Luego, establecemos la propiedad `siguiente` del nodo antes de la cola en `null`, y establecemos la cola de la lista en el nodo antes de la cola.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  deleteFromTail() {
    if (!this.tail) {
      return;
    }
    if (!this.head) {
      this.head = null;
      this.tail = null;
      return;
    }
    let current = this.head;
    while (current.next !== this.tail) {
      current = current.next;
    }
    current.next = null;
    this.tail = current;
  }
}
```

## Búsqueda de datos

Para buscar datos en una lista enlazada, debemos comenzar desde el principio de la lista y comparar los datos de cada nodo con los datos que estamos buscando. Si se encuentran los datos, devolvemos el nodo. Si no se encuentran los datos, devolvemos `null`.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  search(data) {
    let current = this.head;
    while (current) {
      if (current.data === data) {
        return current;
      }
      current = current.next;
    }
    return null;
  }
}
```

## Recorriendo una lista enlazada

Para recorrer una lista enlazada, debemos comenzar en el encabezado de la lista y visitar cada nodo por turno. Podemos hacer esto usando un bucle `while`.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  traverse() {
    let current = this.head;
    while (current) {
      console.log(current.data);
      current = current.next;
    }
  }
}
```

## Invertir una lista enlazada

Para invertir una lista enlazada, debemos realizar un seguimiento del nodo anterior, el nodo actual y el siguiente nodo. Luego, establecemos la propiedad `siguiente` del nodo actual en el nodo anterior y pasamos al siguiente nodo.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  reverse() {
    let current = this.head;
    let previous = null;
    let next = null;
    while (current) {
      next = current.next;
      current.next = previous;
      previous = current;
      current = next;
    }
    this.head = previous;
  }
}
```

## Ordenar una lista enlazada

Hay muchas maneras diferentes de ordenar una lista enlazada. Una forma es usar el [algoritmo de clasificación de selección] (https://en.wikipedia.org/wiki/Selection_sort).

Para ordenar una lista enlazada mediante la ordenación por selección, debemos realizar un seguimiento del nodo mínimo, el nodo actual y el siguiente nodo. Luego, comparamos los datos del nodo actual con los datos del nodo mínimo. Si los datos del nodo actual son menores que los datos del nodo mínimo, establecemos el nodo mínimo en el nodo actual. Una vez que hemos recorrido toda la lista, intercambiamos los datos del nodo mínimo con los datos del nodo principal. Luego, pasamos al siguiente nodo y repetimos el proceso.

```javascript
class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
  }

  sort() {
    let current = this.head;
    let minimum = null;
    let next = null;
    while (current) {
      minimum = current;
      next = current.next;
      while (next) {
        if (next.data < minimum.data) {
          minimum = next;
        }
        next = next.next;
      }
      if (minimum !== current) {
        const temp = current.data;
        current.data = minimum.data;
        minimum.data = temp;
      }
      current = current.next;
    }
  }
}
```

## Conclusión

Las listas enlazadas son un tipo de estructura de datos que almacena una colección de datos en nodos. Cada nodo en una lista enlazada contiene dos cosas: los datos en sí y una referencia al siguiente nodo en la lista. Las listas enlazadas se utilizan a menudo porque son fáciles de manipular y no requieren memoria adicional para almacenar los enlaces entre los nodos.

Hay dos tipos de listas enlazadas: listas con enlaces simples y listas con enlaces dobles. En una lista de enlaces simples, cada nodo solo tiene una referencia al siguiente nodo de la lista. En una lista doblemente enlazada, cada nodo tiene una referencia tanto al nodo siguiente como al nodo anterior.

Para crear una lista enlazada, necesitamos crear una clase `Nodo`. Cada 'Nodo' tendrá dos propiedades: 'datos', que almacena los datos de ese nodo, y 'siguiente', que almacena la referencia al siguiente nodo de la lista.

Para insertar datos en una lista enlazada, podemos insertarlos al principio de la lista o insertarlos al final de la lista. Para eliminar datos de una lista vinculada, podemos eliminarlos del encabezado de la lista o eliminarlos del final de la lista.

Para buscar datos en una lista enlazada, debemos comenzar desde el principio de la lista y comparar los datos de cada nodo con los datos que estamos buscando. Si se encuentran los datos, devolvemos el nodo. Si no se encuentran los datos, devolvemos `null`.

Para recorrer una lista enlazada, debemos comenzar en el encabezado de la lista y visitar cada nodo por turno. Para invertir una lista enlazada, debemos realizar un seguimiento del nodo anterior, el nodo actual y el siguiente nodo. Luego, establecemos la propiedad `siguiente` del nodo actual en el nodo anterior y pasamos al siguiente nodo.

Hay muchas maneras diferentes de ordenar una lista enlazada. Una forma es usar el [algoritmo de clasificación de selección] (https://en.wikipedia.org/wiki/Selection_sort). Para ordenar una lista enlazada mediante la ordenación por selección, debemos realizar un seguimiento del nodo mínimo, el nodo actual y el siguiente nodo. Luego, comparamos los datos del nodo actual con los datos del nodo mínimo. Si los datos del nodo actual son menores que los datos del nodo mínimo, establecemos el nodo mínimo en el nodo actual. Una vez que hemos recorrido toda la lista, intercambiamos los datos del nodo mínimo con los datos del nodo principal. Luego, pasamos al siguiente nodo y repetimos el proceso.