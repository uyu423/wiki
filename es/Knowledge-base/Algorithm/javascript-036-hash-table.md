---
title: [JavaScript] 036: tabla hash
description: 
published: true
date: 2023-02-10T14:33:06.486Z
tags: 
editor: markdown
dateCreated: 2023-02-10T14:33:04.735Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 036: Hash Table***English** document is available*](/en/Knowledge-base/Algorithm/javascript-036-hash-table)
{.links-list}


# JavaScript 036: tabla hash

En esta publicación, analizaremos las tablas hash, una estructura de datos que se utiliza para almacenar pares clave-valor. Cubriremos el concepto y la teoría detrás de las tablas hash, veremos algunos ejemplos de código y terminaremos con algunos ejercicios relacionados.

## ¿Qué es una tabla hash?

Una tabla hash es una estructura de datos que almacena pares clave-valor. Es similar a una matriz, pero la clave se usa para indexar la ubicación del valor en lugar de un índice numérico.

Las tablas hash se utilizan para implementar mapas y conjuntos. También se utilizan en muchas otras aplicaciones, como almacenamiento en caché, búsquedas rápidas y más.

## ¿Cómo funcionan las tablas hash?

Las tablas hash utilizan una función hash para asignar claves a valores. Una función hash es una función que toma una clave y la asigna a una ubicación en la tabla hash.

La ubicación se llama cubeta. Un cubo es simplemente un índice de matriz.

La función hash se usa para calcular el depósito para una clave determinada. La función toma la clave y calcula un índice de matriz basado en la clave. Este índice se utiliza para almacenar el valor en la matriz.

## ¿Por qué usar tablas hash?

Las tablas hash son rápidas. Tienen inserción y búsqueda de tiempo constante. Esto significa que el tiempo que lleva insertar o buscar un valor es independiente del tamaño de la tabla hash.

Las tablas hash también son flexibles. Se pueden usar para implementar muchas estructuras de datos diferentes, como mapas, conjuntos y más.

## Ejemplos de código

Aquí hay una implementación de tabla hash simple en JavaScript.


```javascript
function HashTable(size) {
  this.buckets = new Array(size);
  this.numBuckets = this.buckets.length;
}

function HashNode(key, value, next) {
  this.key = key;
  this.value = value;
  this.next = next || null;
}

HashTable.prototype.hash = function(key) {
  var total = 0;
  for (var i = 0; i < key.length; i++) {
    total += key.charCodeAt(i);
  }
  var bucket = total % this.numBuckets;
  return bucket;
};

HashTable.prototype.insert = function(key, value) {
  var bucket = this.hash(key);
  if (!this.buckets[bucket]) {
    this.buckets[bucket] = new HashNode(key, value);
  }
  else if (this.buckets[bucket].key === key) {
    this.buckets[bucket].value = value;
  }
  else {
    var currentNode = this.buckets[bucket];
    while (currentNode.next) {
      if (currentNode.next.key === key) {
        currentNode.next.value = value;
        return;
      }
      currentNode = currentNode.next;
    }
    currentNode.next = new HashNode(key, value);
  }
};

HashTable.prototype.get = function(key) {
  var bucket = this.hash(key);
  if (!this.buckets[bucket]) {
    return null;
  }
  else {
    var currentNode = this.buckets[bucket];
    while (currentNode) {
      if (currentNode.key === key) {
        return currentNode.value;
      }
      currentNode = currentNode.next;
    }
    return null;
  }
};

HashTable.prototype.retrieveAll = function() {
  var allValues = [];
  for (var i = 0; i < this.numBuckets; i++) {
    var currentNode = this.buckets[i];
    while (currentNode) {
      allValues.push(currentNode.value);
      currentNode = currentNode.next;
    }
  }
  return allValues;
};

var myHT = new HashTable(30);

myHT.insert('dean', 'dean@gmail.com');
myHT.insert('megan', 'megan@gmail.com');
myHT.insert('dave', 'dave@gmail.com');
myHT.insert('jane', 'jane@gmail.com');
myHT.insert('mike', 'mike@gmail.com');
myHT.insert('sarah', 'sarah@gmail.com');
myHT.insert('john', 'john@gmail.com');

console.log(myHT.retrieveAll());
// ['dean@gmail.com', 'megan@gmail.com', 'dave@gmail.com', 'jane@gmail.com', 'mike@gmail.com', 'sarah@gmail.com', 'john@gmail.com']
```

En el ejemplo de código anterior, hemos creado una clase HashTable y una clase HashNode. La clase HashTable tiene una propiedad de tamaño que se usa para inicializar la matriz. También tiene una propiedad numBuckets que se usa para almacenar el tamaño de la matriz.

La clase HashNode tiene una clave, un valor y la siguiente propiedad. La clave se usa para almacenar la clave del nodo, el valor se usa para almacenar el valor del nodo y la siguiente propiedad se usa para almacenar el siguiente nodo en la lista vinculada.

La clase HashTable tiene una función hash que toma una clave y la asigna a una ubicación en la matriz. La ubicación se llama cubeta. Un cubo es simplemente un índice de matriz.

La clase HashTable también tiene una función de inserción que toma una clave y un valor. Utiliza la función hash para calcular el cubo para la clave dada. Si el depósito está vacío, crea un nuevo HashNode y lo almacena en el depósito. Si el cubo no está vacío, comprueba si la clave ya existe. Si la clave existe, actualiza el valor. Si la clave no existe, agrega el nuevo HashNode al final de la lista vinculada.

La clase HashTable también tiene una función de obtención que toma una clave y devuelve el valor de la clave dada. Si la clave no existe, devuelve nulo.

La clase HashTable también tiene una función retrieveAll que devuelve una matriz de todos los valores en la tabla hash.

## Ejercicios

1. Implemente una tabla hash en su lenguaje de programación favorito.

2. Escriba una función que tome una clave y un valor y los inserte en una tabla hash.

3. Escribe una función que tome una clave y devuelva el valor de la clave dada.

4. Escriba una función que devuelva una matriz de todos los valores en la tabla hash.