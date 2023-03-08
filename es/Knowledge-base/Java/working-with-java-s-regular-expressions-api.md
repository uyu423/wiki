---
title: Trabajar con la API de expresiones regulares de Java
description: 
published: true
date: 2023-02-13T17:17:32.052Z
tags: 
editor: markdown
dateCreated: 2023-02-13T17:17:30.349Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Working with Java's Regular Expressions API***English** document is available*](/en/Knowledge-base/Java/working-with-java-s-regular-expressions-api)
{.links-list}


# Trabajar con la API de expresiones regulares de Java

La API de expresión regular de Java es una de las más poderosas en cualquier lenguaje. Se puede usar para hacer coincidir cadenas, buscar subcadenas y reemplazar subcadenas. En este artículo, veremos cómo usar la API de expresión regular para hacer cada una de estas cosas.

## Cadenas coincidentes

El uso más básico de la API de expresiones regulares es hacer coincidir una cadena con una expresión regular. Esto se puede hacer con el método `matches()` de la clase `java.util.regex.Pattern`. Por ejemplo, para hacer coincidir una cadena con la expresión regular `"\\d+"`, que coincide con uno o más dígitos, haríamos lo siguiente:

```java
String input = "12345";
String regex = "\\d+";

boolean matches = Pattern.matches(regex, input);
// matches is true
```

Si la expresión regular incluye grupos de captura, entonces se puede acceder a esos grupos mediante el método `matches()`. Por ejemplo, la expresión regular `"(\\d)(\\d)"` tiene dos grupos de captura. Podemos acceder a esos grupos de captura así:

```java
String input = "12";
String regex = "(\\d)(\\d)";

boolean matches = Pattern.matches(regex, input);
// matches is true

// Get the first capture group
Matcher m = Pattern.compile(regex).matcher(input);
m.matches();
String group1 = m.group(1); // "1"

// Get the second capture group
String group2 = m.group(2); // "2"
```

## Buscando subcadenas

La API de expresiones regulares también se puede usar para buscar subcadenas que coincidan con una expresión regular. Esto se puede hacer con el método `find()` de la clase `java.util.regex.Matcher`. Por ejemplo, para buscar la subcadena `"\\d+"` en la cadena `"12345"`, haríamos lo siguiente:

```java
String input = "12345";
String regex = "\\d+";

Matcher m = Pattern.compile(regex).matcher(input);

boolean found = m.find();
// found is true

// Get the substring that was found
String found = m.group(); // "12345"
```

De manera similar a `matches()`, el método `find()` también admite grupos de captura. Por ejemplo, la expresión regular `"(\\d)(\\d)"` tiene dos grupos de captura. Podemos acceder a esos grupos de captura así:

```java
String input = "12345";
String regex = "(\\d)(\\d)";

Matcher m = Pattern.compile(regex).matcher(input);

boolean found = m.find();
// found is true

// Get the first capture group
String group1 = m.group(1); // "1"

// Get the second capture group
String group2 = m.group(2); // "2"
```

## Reemplazo de subcadenas

La API de expresión regular también se puede usar para reemplazar subcadenas que coincidan con una expresión regular. Esto se puede hacer con el método `replaceAll()` de la clase `java.util.regex.Matcher`. Por ejemplo, para reemplazar todas las subcadenas que coinciden con la expresión regular `"\\d"` con la cadena `"X"` en la cadena `"12345"`, haríamos lo siguiente:

```java
String input = "12345";
String regex = "\\d";

Matcher m = Pattern.compile(regex).matcher(input);

String replaced = m.replaceAll("X");
// replaced is "XXXXX"
```

## Conclusión

En este artículo, hemos visto cómo usar la API de expresiones regulares de Java para hacer coincidir cadenas, buscar subcadenas y reemplazar subcadenas. También hemos visto cómo acceder a los grupos de captura. Con este conocimiento, debería poder usar la API de expresiones regulares para resolver una variedad de problemas.