---
title: Aprovechamiento del paquete java.util.stream de Java para el procesamiento de transmisiones
description: 
published: true
date: 2023-02-04T12:18:06.965Z
tags: 
editor: markdown
dateCreated: 2023-02-04T12:18:05.317Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Leveraging Java's java.util.stream Package for Stream Processing***English** document is available*](/en/Knowledge-base/Java/leveraging-java-s-java-util-stream-package-for-stream-processing)
{.links-list}


# Aprovechando el paquete java.util.stream de Java para el procesamiento de transmisiones

El paquete java.util.stream se introdujo en Java 8 y ha ido ganando popularidad desde entonces. Ofrece una forma concisa y poderosa de procesar las recopilaciones de datos.

En este artículo, exploraremos cómo usar el paquete java.util.stream para realizar el procesamiento de secuencias. Veremos algunas operaciones de transmisión comunes y mostraremos cómo se pueden usar para resolver problemas del mundo real.

## ¿Qué es el procesamiento de flujo?

El procesamiento de flujo es una forma de procesar recopilaciones de datos de forma declarativa. Una tubería de flujo es una secuencia de operaciones de flujo, cada una de las cuales toma un flujo de entrada y produce un flujo de salida.

La operación de transmisión más básica es la operación de filtrado. Toma un predicado (una función que devuelve un booleano) y produce una nueva secuencia que contiene solo los elementos que satisfacen el predicado.

Por ejemplo, podemos usar la operación de filtro para encontrar todos los números pares en una secuencia de enteros:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> evenStream = stream.filter(i -> i % 2 == 0);
```

El paquete java.util.stream también proporciona la operación de mapa. Toma una función que transforma un elemento de entrada en un elemento de salida y produce una nueva secuencia que contiene los elementos transformados.

Por ejemplo, podemos usar la operación de mapa para transformar un flujo de números enteros en un flujo de sus raíces cuadradas:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Double> squareRootStream = stream.map(i -> Math.sqrt(i));
```

## Operaciones de transmisión

Hay muchas otras operaciones de transmisión en el paquete java.util.stream. Exploraremos algunos de los más comunes.

### mapa

La operación de mapa toma una función que transforma un elemento de entrada en un elemento de salida y produce una nueva secuencia que contiene los elementos transformados.

Por ejemplo, podemos usar la operación de mapa para transformar un flujo de números enteros en un flujo de sus raíces cuadradas:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Double> squareRootStream = stream.map(i -> Math.sqrt(i));
```

También podemos usar la operación map para transformar un flujo de cadenas en un flujo de sus longitudes:

```java
Stream<String> stream = Stream.of("hello", "world");

Stream<Integer> lengthStream = stream.map(s -> s.length());
```

### mapa plano

La operación flatMap toma una función que transforma un elemento de entrada en un flujo de salida y produce un nuevo flujo que contiene los elementos de los flujos de salida de todos los elementos de entrada.

Esto se explica mejor con un ejemplo. Digamos que tenemos un flujo de cadenas y queremos encontrar todos los caracteres que aparecen en esas cadenas. Podemos usar la operación flatMap para hacer esto:

```java
Stream<String> stream = Stream.of("hello", "world");

Stream<Character> characterStream = stream.flatMap(s -> {
  List<Character> characters = new ArrayList<>();
  
  for (char c : s.toCharArray()) {
    characters.add(c);
  }
  
  return characters.stream();
});
```

En el ejemplo anterior, hemos usado la operación flatMap para transformar un flujo de cadenas en un flujo de caracteres.

### filtro

La operación de filtro toma un predicado (una función que devuelve un booleano) y produce una nueva secuencia que contiene solo los elementos que satisfacen el predicado.

Por ejemplo, podemos usar la operación de filtro para encontrar todos los números pares en una secuencia de enteros:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> evenStream = stream.filter(i -> i % 2 == 0);
```

También podemos usar la operación de filtro para encontrar todas las cadenas en una transmisión que comiencen con la letra 'a':

```java
Stream<String> stream = Stream.of("apple", "banana", "cat", "dog");

Stream<String> filteredStream = stream.filter(s -> s.startsWith("a"));
```

### ordenado

La operación ordenada toma un comparador opcional y produce una nueva secuencia que se ordena de acuerdo con el comparador dado. Si no se proporciona un comparador, los elementos se clasifican en su orden natural.

Por ejemplo, podemos usar la operación sorted para ordenar un flujo de números enteros en orden ascendente:

```java
Stream<Integer> stream = Stream.of(5, 3, 7, 1, 4, 2, 6);

Stream<Integer> sortedStream = stream.sorted();
```

También podemos usar la operación sorted para ordenar un flujo de cadenas en orden descendente:

```java
Stream<String> stream = Stream.of("hello", "world", "this", "is", "a", "test");

Stream<String> sortedStream = stream.sorted((s1, s2) -> s2.compareTo(s1));
```

### distinto

La operación distintiva produce una nueva secuencia que contiene solo los elementos distintos de la secuencia de entrada.

Por ejemplo, podemos usar la operación distintiva para eliminar elementos duplicados de una secuencia:

```java
Stream<Integer> stream = Stream.of(1, 1, 2, 2, 3, 3, 4, 4, 5, 5);

Stream<Integer> distinctStream = stream.distinct();
```

### límite

La operación de límite toma un valor largo y produce una nueva secuencia que está limitada al número dado de elementos.

Por ejemplo, podemos usar la operación de límite para crear una secuencia que contenga solo los primeros cinco elementos de otra secuencia:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> limitedStream = stream.limit(5);
```

### saltar

La operación de salto toma un valor largo y produce una nueva secuencia que salta el número dado de elementos.

Por ejemplo, podemos usar la operación skip para crear una secuencia que contenga todos los elementos de otra secuencia excepto los primeros cinco:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

Stream<Integer> skippedStream = stream.skip(5);
```

### reducir

La operación de reducción toma dos argumentos: un valor inicial y un operador binario. El operador binario se aplica al valor inicial y al primer elemento de la secuencia, luego el resultado de esa operación se usa como valor inicial para la siguiente operación, y así sucesivamente. El resultado final es el valor de la última operación.

Por ejemplo, podemos usar la operación de reducción para encontrar la suma de un flujo de números enteros:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

int sum = stream.reduce(0, (i1, i2) -> i1 + i2);
```

También podemos usar la operación de reducción para encontrar el producto de un flujo de números enteros:

```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

int product = stream.reduce(1, (i1, i2) -> i1 * i2);
```

### recolectar

La operación de recopilación toma un recopilador y produce una nueva secuencia que contiene los elementos de la secuencia de entrada, procesada por el recopilador.

Un recopilador es una función que agrupa elementos del flujo en una estructura de datos mutable. Por ejemplo, podemos usar la operación de recopilación para agrupar un flujo de cadenas por su longitud:

```java
Stream<String> stream = Stream.of("hello", "world", "this", "is", "a", "test");

Map<Integer, List<String>> map = stream.collect(Collectors.groupingBy(s -> s.length()));
```

En el ejemplo anterior, hemos usado la operación de recopilación para agrupar las cadenas en la secuencia por su longitud. El resultado es un mapa de longitud a una lista de cadenas de esa longitud.

## Ejemplos de procesamiento de flujo

Ahora que hemos visto algunas de las operaciones de transmisión más comunes, veamos cómo se pueden usar para resolver problemas del mundo real.

### El recuento de palabras

Digamos que tenemos un flujo de cadenas que representan un documento. Queremos contar el número de veces que aparece cada palabra en el documento. Podemos usar las operaciones de procesamiento de flujo que hemos visto para hacer esto:

```java
Stream<String> stream = Stream.of("hello", "world", "this", "is", "a", "test");

Map<String, Long> map = stream.collect(Collectors.groupingBy(s -> s, Collectors.counting()));
```

En el ejemplo anterior, hemos usado la operación de recopilación para agrupar las cadenas en la secuencia por su valor. El resultado es un mapa de cadena a la cantidad de veces que esa cadena aparece en la secuencia.

### Tamiz de números primos

Digamos que tenemos una secuencia de números enteros. Queremos encontrar todos los números primos en la secuencia. Podemos usar las operaciones de procesamiento de flujo que hemos visto para hacer esto:

```java
Stream<Integer> stream = Stream.of(2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20);

List<Integer> primes = stream.filter(i -> {
  for (int j = 2; j < i; j++) {
    if (i % j == 0) {
      return false;
    }
  }
  
  return true;
}).collect(Collectors.toList());
```

En el ejemplo anterior, hemos usado la operación de filtro para encontrar todos los números primos en la secuencia. El resultado es una lista de los números primos en la secuencia.

## Conclusión

En este artículo, hemos visto cómo usar el paquete java.util.stream para realizar el procesamiento de secuencias. Hemos analizado algunas operaciones de transmisión comunes y hemos visto cómo se pueden usar para resolver problemas del mundo real.