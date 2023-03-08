---
title: [Lenguaje C] 047: Sufijo Trie
description: 
published: true
date: 2023-02-14T00:32:25.449Z
tags: 
editor: markdown
dateCreated: 2023-02-14T00:32:23.594Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 047: Suffix Trie***English** document is available*](/en/Knowledge-base/Algorithm/c-language-047-suffix-trie)
{.links-list}


# 047: Sufijo Trie

## ¿Qué es un Sufijo Trie?

Un trie de sufijo es una especie de trie comprimido en el que solo los sufijos de un texto determinado se almacenan como claves en los nodos. Es una estructura de datos eficiente en el espacio que permite algoritmos de coincidencia de patrones rápidos, como aquellos para encontrar todas las ocurrencias de un patrón dado o para encontrar la subcadena repetida más larga.

## ¿Como funciona?

Para construir un sufijo trie, primero necesitamos construir un trie para el texto. Luego podemos comprimir el trie eliminando todos los nodos que tienen un solo hijo.

La estructura de datos resultante se denomina sufijo trie. Tiene la misma complejidad de tiempo de búsqueda que un trie, pero usa menos espacio.

## Ejemplo de código

Aquí hay una implementación simple de un sufijo trie en C++.

```cpp
#include <iostream>
#include <string>
#include <unordered_map>
#include <vector>

using namespace std;

class SuffixTrie {
public:
  SuffixTrie(string s) {
    root = new TrieNode();
    for (int i = 0; i < s.size(); i++) {
      insert(s.substr(i));
    }
  }

  void insert(string s) {
    TrieNode* curr = root;
    for (char c : s) {
      if (curr->children.find(c) == curr->children.end()) {
        curr->children[c] = new TrieNode();
      }
      curr = curr->children[c];
    }
    curr->isEnd = true;
  }

  bool search(string s) {
    TrieNode* curr = root;
    for (char c : s) {
      if (curr->children.find(c) == curr->children.end()) {
        return false;
      }
      curr = curr->children[c];
    }
    return curr->isEnd;
  }

private:
  struct TrieNode {
    unordered_map<char, TrieNode*> children;
    bool isEnd;
    TrieNode() : isEnd(false) {}
  };

  TrieNode* root;
};

int main() {
  string s = "banana";
  SuffixTrie trie(s);
  cout << trie.search("an") << endl; // 1
  cout << trie.search("ana") << endl; // 1
  cout << trie.search("nan") << endl; // 1
  cout << trie.search("nana") << endl; // 1
  cout << trie.search("banana") << endl; // 1
  cout << trie.search("bana") << endl; // 0
  return 0;
}
```

## Ejercicios relacionados

1. Implemente una función que tome una cadena y cree un sufijo trie para ella.

2. Implemente una función que tome una cadena y un patrón, y devuelva la lista de todos los índices iniciales en la cadena donde ocurre el patrón.

3. Implemente una función que tome una cadena y devuelva la subcadena repetida más larga en ella.