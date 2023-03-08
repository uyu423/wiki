---
title: [Lenguaje C] 046: Trio
description: 
published: true
date: 2023-02-13T19:56:14.228Z
tags: 
editor: markdown
dateCreated: 2023-02-13T19:56:12.649Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 046: Trie***English** document is available*](/en/Knowledge-base/Algorithm/c-language-046-trie)
{.links-list}


# 046: Prueba

Un trie, también llamado árbol digital o árbol de prefijos, es una estructura de datos de árbol ordenada que se utiliza para almacenar un conjunto dinámico o una matriz asociativa donde las claves suelen ser cadenas. A diferencia de un árbol de búsqueda binario, ningún nodo del árbol almacena la clave asociada con ese nodo; en cambio, su posición en el árbol define la clave con la que está asociado. Todos los descendientes de un nodo tienen un prefijo común de la cadena asociada con ese nodo, y la raíz está asociada con la cadena vacía. Los valores no están necesariamente asociados con todos los nodos. Más bien, los valores tienden a asociarse con hojas y con algunos nodos internos que corresponden a claves de interés.

## Concepto

Un trie puede verse como una estructura de datos en forma de árbol que almacena cadenas. En un trie, cada nodo puede tener varios hijos. Cada nodo en un trie almacena un carácter, y las cadenas se forman atravesando desde la raíz hasta un nodo en particular.

![Trie](https://upload.wikimedia.org/wikipedia/commons/b/be/Trie_example.svg)

En el ejemplo anterior, el nodo raíz está representado por la cadena vacía y cada nodo representa una cadena formada al concatenar los caracteres en la ruta desde la raíz hasta ese nodo. Las hojas son los nodos que representan cadenas que no son prefijos de ninguna otra cadena en el trie. En este ejemplo, se almacenan las cadenas "to", "tea", "ted", "ten", "i", "in" y "inn".

## Ejemplo de código

Aquí hay una implementación simple de un trie en C.

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define ALPHABET_SIZE 26

// A node in the trie
struct TrieNode
{
    // The children of this node
    struct TrieNode *children[ALPHABET_SIZE];

    // Is this the end of a word?
    int is_end_of_word;
};

// Returns a new TrieNode
struct TrieNode *get_node(void)
{
    struct TrieNode *p_node = (struct TrieNode *)malloc(sizeof(struct TrieNode));

    if (p_node)
    {
        int i;

        p_node->is_end_of_word = 0;

        for (i = 0; i < ALPHABET_SIZE; i++)
            p_node->children[i] = NULL;
    }

    return p_node;
}

// Inserts a word into the trie
void insert(struct TrieNode *root, const char *key)
{
    int level;
    int length = strlen(key);
    int index;

    struct TrieNode *p_crawl = root;

    for (level = 0; level < length; level++)
    {
        index = CHAR_TO_INDEX(key[level]);

        if (!p_crawl->children[index])
            p_crawl->children[index] = get_node();

        p_crawl = p_crawl->children[index];
    }

    // Mark the last node as leaf
    p_crawl->is_end_of_word = 1;
}

// Searches a word in the trie
int search(struct TrieNode *root, const char *key)
{
    int level;
    int length = strlen(key);
    int index;
    struct TrieNode *p_crawl = root;

    for (level = 0; level < length; level++)
    {
        index = CHAR_TO_INDEX(key[level]);

        if (!p_crawl->children[index])
            return 0;

        p_crawl = p_crawl->children[index];
    }

    return (p_crawl != NULL && p_crawl->is_end_of_word);
}

// Driver
int main()
{
    // Input keys (use only 'a' through 'z' and lower case)
    char keys[][8] = {"the", "a", "there", "answer", "any", "by", "bye", "their"};
    int n = sizeof(keys) / sizeof(keys[0]);

    struct TrieNode *root = get_node();

    // Construct trie
    int i;
    for (i = 0; i < n; i++)
        insert(root, keys[i]);

    // Search for different keys
    search(root, "the") ? printf("Yes\n") : printf("No\n");
    search(root, "these") ? printf("Yes\n") : printf("No\n");
    search(root, "their") ? printf("Yes\n") : printf("No\n");
    search(root, "thaw") ? printf("Yes\n") : printf("No\n");

    return 0;
}
```

## Ejercicio

1. Implemente una función que tome una cadena y la inserte en un trie.

2. Implemente una función que tome una cadena y la busque en un intento.

3. Implemente una función que tome una cadena y devuelva el número de veces que ocurre en un trie.

4. Implemente una función que tome una cadena y devuelva el número de palabras en un trie que comiencen con esa cadena.

## Código de respuesta

1.

```c
void insert(struct TrieNode *root, const char *key)
{
    int level;
    int length = strlen(key);
    int index;

    struct TrieNode *p_crawl = root;

    for (level = 0; level < length; level++)
    {
        index = CHAR_TO_INDEX(key[level]);

        if (!p_crawl->children[index])
            p_crawl->children[index] = get_node();

        p_crawl = p_crawl->children[index];
    }

    // Mark the last node as leaf
    p_crawl->is_end_of_word = 1;
}
```

2.

```c
int search(struct TrieNode *root, const char *key)
{
    int level;
    int length = strlen(key);
    int index;
    struct TrieNode *p_crawl = root;

    for (level = 0; level < length; level++)
    {
        index = CHAR_TO_INDEX(key[level]);

        if (!p_crawl->children[index])
            return 0;

        p_crawl = p_crawl->children[index];
    }

    return (p_crawl != NULL && p_crawl->is_end_of_word);
}
```

3.

```c
int search(struct TrieNode *root, const char *key)
{
    int level;
    int length = strlen(key);
    int index;
    struct TrieNode *p_crawl = root;

    for (level = 0; level < length; level++)
    {
        index = CHAR_TO_INDEX(key[level]);

        if (!p_crawl->children[index])
            return 0;

        p_crawl = p_crawl->children[index];
    }

    return (p_crawl != NULL && p_crawl->is_end_of_word);
}
```

4.

```c
int starts_with(struct TrieNode *root, const char *key)
{
    int level;
    int length = strlen(key);
    int index;
    struct TrieNode *p_crawl = root;

    for (level = 0; level < length; level++)
    {
        index = CHAR_TO_INDEX(key[level]);

        if (!p_crawl->children[index])
            return 0;

        p_crawl = p_crawl->children[index];
    }

    return 1;
}
```

## Comentario

Los intentos son una forma muy eficiente de almacenar cadenas. Se utilizan en muchas aplicaciones, como correctores ortográficos, sugerencias de autocompletar y enrutamiento de IP.