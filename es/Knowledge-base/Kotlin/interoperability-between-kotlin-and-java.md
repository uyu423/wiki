---
title: Interoperabilidad entre Kotlin y Java
description: 
published: true
date: 2023-02-09T08:55:26.174Z
tags: 
editor: markdown
dateCreated: 2023-02-09T08:55:20.011Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Interoperability Between Kotlin and Java***English** document is available*](/en/Knowledge-base/Kotlin/interoperability-between-kotlin-and-java)
{.links-list}



# Interoperabilidad entre Kotlin y Java

Java y Kotlin son dos lenguajes de programación populares que se utilizan para desarrollar aplicaciones de Android. Si bien Kotlin es un lenguaje más nuevo, es totalmente interoperable con Java. Esto significa que puede usar Kotlin y Java juntos en el mismo proyecto, y que puede llamar al código de Kotlin desde Java y viceversa. En este artículo, veremos cómo interactúan Kotlin y Java y cómo puede usar ambos lenguajes en el desarrollo de su aplicación Android.

## Llamar a Kotlin desde Java

Llamar a Kotlin desde Java es sencillo y sencillo. Puede llamar a cualquier código Kotlin desde su código Java y viceversa. No es necesario agregar anotaciones o configuraciones especiales.

Para llamar al código de Kotlin desde Java, simplemente use el nombre completo de la clase, el método o la propiedad de Kotlin. Por ejemplo, para llamar a la función `foo()` en la clase `Foo` de Java, usaría el siguiente código:

```java
FooKt.foo();
```

Para llamar al código Java desde Kotlin, use la anotación `@JvmName`. Esta anotación te permite especificar el nombre de la función o propiedad de Kotlin que se usará cuando la llames desde Java. Por ejemplo, el siguiente código de Kotlin:

```kotlin
@JvmName("bar")
fun foo() {
    // ...
}
```

Se puede llamar desde Java usando el siguiente código:

```java
FooKt.bar();
```

## Trabajar con tipos anulables y no nulos

Kotlin tiene tipos anulables y no nulos, que ayudan a evitar excepciones de puntero nulo. En Kotlin, cualquier tipo se puede convertir en anulable agregando un `?` después del nombre del tipo. Por ejemplo, el siguiente código de Kotlin define una `String` anulable:

```kotlin
var s: String? = null
```

Al llamar al código de Kotlin desde Java, todos los tipos que aceptan valores NULL se convierten automáticamente en sus equivalentes que no son NULL. Por ejemplo, el siguiente código de Kotlin:

```kotlin
fun foo(s: String?) {
    // ...
}
```

Se puede llamar desde Java usando el siguiente código:

```java
foo("Hello");
```

## Trabajar con colecciones de Java

Kotlin y Java tienen enfoques muy diferentes para las colecciones. En Kotlin, todas las colecciones son inmutables por defecto, mientras que en Java son mutables. Esto puede hacer tropezar a los desarrolladores que están acostumbrados a trabajar con colecciones de Java.

Afortunadamente, Kotlin proporciona formas fáciles de convertir entre colecciones de Kotlin y Java. Para convertir una colección de Java a una de Kotlin, puedes usar las funciones `toMutableList()` o `toList()`. Por ejemplo, el siguiente código Java:

```java
List<String> list = Arrays.asList("a", "b", "c");
```

Se puede convertir a una `Lista` de Kotlin usando la función `toList()`:

```kotlin
val list = list.toList()
```

Para convertir una colección de Kotlin en una de Java, puede usar las funciones `toJavaList()` o `toJavaSet()`. Por ejemplo, el siguiente código de Kotlin:

```kotlin
val list = listOf("a", "b", "c")
```

Se puede convertir a una 'Lista' de Java usando la función 'toJavaList()':

```java
List<String> list = list.toJavaList();
```

## Conclusión

Kotlin y Java son dos lenguajes de programación populares que son totalmente interoperables. Esto significa que puede usar Kotlin y Java juntos en el mismo proyecto, y que puede llamar al código de Kotlin desde Java y viceversa. En este artículo, hemos analizado cómo interactúan Kotlin y Java y cómo puede usar ambos lenguajes en el desarrollo de su aplicación para Android.