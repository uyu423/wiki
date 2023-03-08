---
title: [JavaScript] 049: Árbol Radix (Trie compacto)
description: 
published: true
date: 2023-02-11T03:32:26.674Z
tags: 
editor: markdown
dateCreated: 2023-02-11T03:32:20.149Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 049: Radix Tree (Compact Trie)***English** document is available*](/en/Knowledge-base/Algorithm/javascript-049-radix-tree-compact-trie)
{.links-list}


# Radix Tree (Trie compacto)

Un árbol radix, también conocido como trie compacto, es una estructura de datos eficiente en el espacio que se utiliza para almacenar cadenas. Es similar a un trie, pero en lugar de almacenar cada carácter en un nodo, almacena cada carácter en un borde. Esto permite que el árbol radix ocupe menos espacio que un trie.

Los árboles Radix a menudo se usan para almacenar cadenas que son demasiado largas para caber en un trie tradicional. También se utilizan para almacenar cadenas a las que se accede con frecuencia, como en un diccionario.

## Cómo funciona

Un árbol radix es una estructura de datos similar a un árbol que almacena cadenas. Cada nodo en el árbol de base representa un carácter en la cadena. Los bordes entre los nodos representan los caracteres que son adyacentes entre sí en la cadena.

El árbol radix es similar a un trie, pero en lugar de almacenar cada carácter en un nodo, almacena cada carácter en un borde. Esto permite que el árbol radix ocupe menos espacio que un trie.

El árbol radix también es más eficiente que un trie cuando se trata de buscar cadenas. Un trie debe buscar en todos los nodos del árbol para encontrar una cadena, mientras que un árbol radix puede dejar de buscar tan pronto como llegue a un nodo que no coincida con la cadena.

## Ejemplo de código

Aquí hay una implementación simple de un árbol radix en JavaScript.

```javascript
function RadixTree() {
  this.root = new Node();
}

function Node() {
  this.children = {};
}

RadixTree.prototype.insert = function(string) {
  var node = this.root;

  for (var i = 0; i < string.length; i++) {
    var char = string[i];

    if (!node.children[char]) {
      node.children[char] = new Node();
    }

    node = node.children[char];
  }
};

RadixTree.prototype.search = function(string) {
  var node = this.root;

  for (var i = 0; i < string.length; i++) {
    var char = string[i];

    if (!node.children[char]) {
      return false;
    }

    node = node.children[char];
  }

  return true;
};

var tree = new RadixTree();
tree.insert("cat");
tree.insert("dog");
tree.insert("cats");
tree.insert("dogs");

console.log(tree.search("cat")); // true
console.log(tree.search("cats")); // true
console.log(tree.search("dog")); // true
console.log(tree.search("dogs")); // true
console.log(tree.search("c")); // false
console.log(tree.search("ca")); // false
console.log(tree.search("d")); // false
console.log(tree.search("do")); // false
```

## Ejercicios relacionados

- [Ejercicio Radix Tree](https://repl.it/@jimt/Radix-Tree-Exercise)
- [Ejercicio Compact Trie](https://repl.it/@jimt/Compact-Trie-Exercise)

## Conclusión

Los árboles Radix son una estructura de datos eficiente en el espacio que se utiliza para almacenar cadenas. Son similares a los intentos, pero almacenan cada carácter en un borde en lugar de un nodo. Esto permite que el árbol radix ocupe menos espacio que un trie.

Los árboles Radix a menudo se usan para almacenar cadenas que son demasiado largas para caber en un trie tradicional. También se utilizan para almacenar cadenas a las que se accede con frecuencia, como en un diccionario.