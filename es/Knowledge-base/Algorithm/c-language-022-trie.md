---
title: [Lenguaje C] 022: Triángulo
description: 
published: true
date: 2023-02-11T00:17:29.101Z
tags: 
editor: markdown
dateCreated: 2023-02-11T00:17:27.436Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[C Language] 022: Trie***English** document is available*](/en/Knowledge-base/Algorithm/c-language-022-trie)
{.links-list}


# 022: Trio

Un trie es una estructura de datos similar a un árbol que se utiliza para almacenar un conjunto dinámico o una matriz asociativa donde las claves suelen ser cadenas. A diferencia de un árbol de búsqueda binario, ningún nodo del árbol almacena la clave asociada con ese nodo; en cambio, su posición en el árbol define la clave con la que está asociado. Todos los descendientes de un nodo tienen un prefijo común de la cadena asociada con ese nodo, y la raíz está asociada con la cadena vacía. Los valores no están necesariamente asociados con todos los nodos. Más bien, los valores tienden a asociarse con hojas y con algunos nodos internos que corresponden a claves de interés.

![Trie](https://upload.wikimedia.org/wikipedia/commons/b/be/Trie_example.svg)

En la imagen de ejemplo, las claves se enumeran en los nodos y los valores debajo de ellas. Cada palabra completa en inglés tiene un asterisco debajo. Aquí, el trie almacena un conjunto de palabras en inglés. Las claves son las letras de las palabras y los valores son las propias palabras.

## Ejemplo de código

```c
#include <stdio.h> 
#include <stdlib.h> 
#include <string.h> 
#include <stdbool.h> 

#define ARRAY_SIZE(a) sizeof(a)/sizeof(a[0]) 
#define CHAR_TO_INDEX(c) ((int)c - (int)'a') 

// Alphabet size (# of symbols) 
#define ALPHABET_SIZE (26) 

// Converts key current character into index 
// use only 'a' through 'z' and lower case 
#define CHAR_TO_INDEX(c) ((int)c - (int)'a') 

// trie node 
struct TrieNode 
{ 
	struct TrieNode *children[ALPHABET_SIZE]; 

	// isEndOfWord is true if the node represents 
	// end of a word 
	bool isEndOfWord; 
}; 

// Returns new trie node (initialized to NULLs) 
struct TrieNode *getNode(void) 
{ 
	struct TrieNode *pNode = NULL; 

	pNode = (struct TrieNode *)malloc(sizeof(struct TrieNode)); 

	if (pNode) 
	{ 
		int i; 

		pNode->isEndOfWord = false; 

		for (i = 0; i < ALPHABET_SIZE; i++) 
			pNode->children[i] = NULL; 
	} 

	return pNode; 
} 

// If not present, inserts key into trie 
// If the key is prefix of trie node, just marks leaf node 
void insert(struct TrieNode *root, const char *key) 
{ 
	int level; 
	int length = strlen(key); 
	int index; 

	struct TrieNode *pCrawl = root; 

	for (level = 0; level < length; level++) 
	{ 
		index = CHAR_TO_INDEX(key[level]); 
		if (!pCrawl->children[index]) 
			pCrawl->children[index] = getNode(); 

		pCrawl = pCrawl->children[index]; 
	} 

	// mark last node as leaf 
	pCrawl->isEndOfWord = true; 
} 

// Returns true if key presents in trie, else false 
bool search(struct TrieNode *root, const char *key) 
{ 
	int level; 
	int length = strlen(key); 
	int index; 
	struct TrieNode *pCrawl = root; 

	for (level = 0; level < length; level++) 
	{ 
		index = CHAR_TO_INDEX(key[level]); 

		if (!pCrawl->children[index]) 
			return false; 

		pCrawl = pCrawl->children[index]; 
	} 

	return (pCrawl != NULL && pCrawl->isEndOfWord); 
} 

// Driver 
int main() 
{ 
	// Input keys (use only 'a' through 'z' and lower case) 
	char keys[][8] = {"the", "a", "there", "answer", "any", "by", "bye", "their"}; 

	char output[][32] = {"Not present in trie", "Present in trie"}; 


	struct TrieNode *root = getNode(); 

	// Construct trie 
	int i; 
	for (i = 0; i < ARRAY_SIZE(keys); i++) 
		insert(root, keys[i]); 

	// Search for different keys 
	printf("%s --- %s\n", "the", output[search(root, "the")] ); 
	printf("%s --- %s\n", "these", output[search(root, "these")] ); 
	printf("%s --- %s\n", "their", output[search(root, "their")] ); 
	printf("%s --- %s\n", "thaw", output[search(root, "thaw")] ); 

	return 0; 
} 
```

## Explicación

En el ejemplo de código anterior, hemos implementado un trie en el lenguaje de programación C. El código incluye una función para insertar claves en el trie y una función para buscar en el trie una clave determinada.

También hemos definido una estructura para representar un nodo trie. Cada nodo tiene una matriz de punteros a los nodos secundarios (uno para cada letra del alfabeto) y un indicador booleano para indicar si el nodo representa el final de una palabra.

La función de inserción toma un nodo raíz y una clave como entrada e inserta la clave en el trie. Si la clave ya está presente en el trie, la función no hace nada.

La función de búsqueda toma un nodo raíz y una clave como entrada y devuelve verdadero si la clave está presente en el trie y falso en caso contrario.

## Aplicaciones

Los intentos se usan a menudo para almacenar cadenas que se usan con frecuencia, como palabras en un diccionario. También se utilizan para almacenar cadenas que comparten un prefijo común, como secuencias de ADN.

Los intentos también se pueden usar para almacenar claves que no son cadenas, como números enteros. En este caso, cada nodo almacenaría un número en lugar de una letra, y las claves se almacenarían en el orden en que aparecen en la secuencia.

## Ejercicios

1. Implemente una función para eliminar una clave de un trie.

2. Implemente una función para encontrar el prefijo único más corto de una clave dada.

3. Implemente una función para encontrar el prefijo común más largo de un conjunto de claves.

4. Implemente una función para verificar si una cadena dada es una palabra válida en un intento dado.