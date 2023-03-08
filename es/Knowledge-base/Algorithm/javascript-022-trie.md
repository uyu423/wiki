---
title: [JavaScript] 022: Trio
description: 
published: true
date: 2023-02-10T00:32:32.374Z
tags: 
editor: markdown
dateCreated: 2023-02-10T00:32:30.716Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [[JavaScript] 022: Trie***English** document is available*](/en/Knowledge-base/Algorithm/javascript-022-trie)
{.links-list}


# JavaScript 022: Prueba

En informática, un trie, también llamado árbol digital o árbol de prefijos, es una especie de árbol de búsqueda: una estructura de datos de árbol ordenada que se utiliza para almacenar un conjunto dinámico o una matriz asociativa donde las claves suelen ser cadenas. A diferencia de un árbol de búsqueda binario, ningún nodo del árbol almacena la clave asociada con ese nodo; en cambio, su posición en el árbol define la clave con la que está asociado. Todos los descendientes de un nodo tienen un prefijo común de la cadena asociada con ese nodo, y la raíz está asociada con la cadena vacía. Los valores no están necesariamente asociados con todos los nodos. Más bien, los valores tienden a asociarse con hojas y con algunos nodos internos que corresponden a claves de interés.

![Trie](https://upload.wikimedia.org/wikipedia/commons/thumb/b/be/Trie_example.svg/200px-Trie_example.svg.png)

En el ejemplo que se muestra, las claves se enumeran en los nodos y los valores debajo de ellas. Cada palabra completa en inglés tiene un valor entero arbitrario asociado. Cuando el trie se recorre desde la raíz hacia una clave en particular, el valor asociado se recupera concatenando las letras en los bordes recorridos.

Un trie puede verse como un autómata finito determinista en forma de árbol. Un autómata finito determinista se construye a partir de un conjunto de estados Q y un conjunto de símbolos de entrada Σ, donde Σ es el alfabeto del trie. El autómata tiene un estado inicial s, un conjunto de estados finales F y una función de transición que asigna cada estado y símbolo de entrada a un nuevo estado. En un trie, el conjunto de estados finales es generalmente el conjunto de todas las cadenas.

La función de transición para un trie se define como sigue: dado un estado s y un símbolo de entrada a, el nuevo estado se obtiene descendiendo desde el estado s a lo largo del borde etiquetado con el símbolo a. Si no hay borde etiquetado con el símbolo a, entonces el nuevo estado es el estado de falla. En un intento, el estado de falla es generalmente la raíz.

Un trie puede verse como un caso especial de un árbol N-ario en el que cada nodo tiene como máximo N hijos, donde N es el número de símbolos en el alfabeto. La ruta desde la raíz hasta cualquier hoja describe un prefijo de la cadena asociada con esa hoja.

## Implementación

Un trie se puede implementar como un árbol N-ario, un árbol radix, un árbol de búsqueda digital, un árbol digital o un árbol Patricia.

### Árbol N-ario

Un árbol N-ario es un árbol enraizado en el que cada nodo no tiene más de N hijos. Un trie con N símbolos en su alfabeto puede verse como un árbol N-ario en el que cada nodo tiene como máximo N hijos.

![Árbol N-ario](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5e/Trie_nary_tree_example.svg/200px-Trie_nary_tree_example.svg.png)

En el ejemplo que se muestra, las claves se enumeran en los nodos y los valores están debajo de ellos. Cada palabra completa en inglés tiene un valor entero arbitrario asociado. Cuando el trie se recorre desde la raíz hacia una clave en particular, el valor asociado se recupera concatenando las letras en los bordes recorridos.

Un trie puede verse como un caso especial de un árbol N-ario en el que cada nodo tiene como máximo N hijos, donde N es el número de símbolos en el alfabeto. La ruta desde la raíz hasta cualquier hoja describe un prefijo de la cadena asociada con esa hoja.

### Árbol Radix

Un árbol radix o árbol comprimido es una especie de árbol de búsqueda en el que las claves son cadenas. El árbol se comprime almacenando solo las diferencias entre claves sucesivas. Por ejemplo, si las claves son las palabras "Hola", "Mundo" e "Infierno", el nodo raíz tendrá las letras "H" y "W", y el primer hijo de la raíz tendrá la letra "o ". El segundo hijo de la raíz tendrá las letras "r" y "l".

![Árbol Radix](https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Radix_tree.svg/200px-Radix_tree.svg.png)

En el ejemplo que se muestra, las claves se enumeran en los nodos y los valores están debajo de ellos. Cada palabra completa en inglés tiene un valor entero arbitrario asociado. Cuando el trie se recorre desde la raíz hacia una clave en particular, el valor asociado se recupera concatenando las letras en los bordes recorridos.

Un árbol radix puede verse como un caso especial de un árbol N-ario en el que cada nodo tiene como máximo N hijos, donde N es el número de símbolos en el alfabeto. La ruta desde la raíz hasta cualquier hoja describe un prefijo de la cadena asociada con esa hoja.

### Árbol de búsqueda digital

Un árbol de búsqueda digital o árbol digital es una especie de árbol de búsqueda en el que las claves son cadenas. El árbol se comprime almacenando solo las diferencias entre claves sucesivas. Por ejemplo, si las claves son las palabras "Hola", "Mundo" e "Infierno", el nodo raíz tendrá las letras "H" y "W", y el primer hijo de la raíz tendrá la letra "o ". El segundo hijo de la raíz tendrá las letras "r" y "l".

![Árbol digital](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b4/Digital_tree.svg/200px-Digital_tree.svg.png)

En el ejemplo que se muestra, las claves se enumeran en los nodos y los valores están debajo de ellos. Cada palabra completa en inglés tiene un valor entero arbitrario asociado. Cuando el trie se recorre desde la raíz hacia una clave en particular, el valor asociado se recupera concatenando las letras en los bordes recorridos.

Un árbol digital puede verse como un caso especial de un árbol N-ario en el que cada nodo tiene como máximo N hijos, donde N es el número de símbolos en el alfabeto. La ruta desde la raíz hasta cualquier hoja describe un prefijo de la cadena asociada con esa hoja.

### Patricia Árbol

Un árbol Patricia o árbol radix es una especie de árbol de búsqueda en el que las claves son cadenas. El árbol se comprime almacenando solo las diferencias entre claves sucesivas. Por ejemplo, si las claves son las palabras "Hola", "Mundo" e "Infierno", el nodo raíz tendrá las letras "H" y "W", y el primer hijo de la raíz tendrá la letra "o ". El segundo hijo de la raíz tendrá las letras "r" y "l".

![Árbol de Patricia](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0d/Patricia_tree.svg/200px-Patricia_tree.svg.png)

En el ejemplo que se muestra, las claves se enumeran en los nodos y los valores están debajo de ellos. Cada palabra completa en inglés tiene un valor entero arbitrario asociado. Cuando el trie se recorre desde la raíz hacia una clave en particular, el valor asociado se recupera concatenando las letras en los bordes recorridos.

Un árbol de Patricia puede verse como un caso especial de un árbol N-ario en el que cada nodo tiene como máximo N hijos, donde N es el número de símbolos en el alfabeto. La ruta desde la raíz hasta cualquier hoja describe un prefijo de la cadena asociada con esa hoja.

## Aplicaciones

Los intentos se utilizan en muchas aplicaciones, tales como:

- **Compresión**: los intentos se pueden usar para comprimir cadenas almacenando cadenas que tienen un prefijo común en el mismo nodo. Por ejemplo, la cadena "aaaabbbbccccdddd" se puede comprimir a "4a4b4c4d".

- **Corrección ortográfica**: los intentos se pueden usar para almacenar un diccionario de palabras y luego se usan para verificar si una palabra determinada está escrita correctamente.

- **Búsqueda de direcciones IP**: los intentos se pueden usar para almacenar una lista de direcciones IP y luego se pueden usar para buscar la dirección IP de un host determinado.

- **Análisis de secuencias de ADN**: los intentos se pueden usar para almacenar secuencias de ADN y luego se pueden usar para encontrar la secuencia de ADN coincidente para una consulta determinada.