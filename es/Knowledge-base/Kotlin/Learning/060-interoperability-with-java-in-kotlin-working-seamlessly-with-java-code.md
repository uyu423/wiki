---
title: 060: Interoperabilidad con Java en Kotlin: trabajar sin problemas con código Java
description: 
published: true
date: 2023-02-16T21:32:44.029Z
tags: 
editor: markdown
dateCreated: 2023-02-16T21:32:41.774Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [060: Interoperability with Java in Kotlin: Working Seamlessly with Java Code***English** document is available*](/en/Knowledge-base/Kotlin/Learning/060-interoperability-with-java-in-kotlin-working-seamlessly-with-java-code)
{.links-list}


# Interoperabilidad con Java en Kotlin: trabajar sin problemas con código Java

Como lenguaje de programación oficial para Android, Java ha sido la elección preferida de muchos desarrolladores. Sin embargo, Kotlin es una estrella en ascenso en el mundo de los lenguajes de programación y ofrece muchas características que lo convierten en una excelente alternativa a Java.

Una de las mayores ventajas de Kotlin es su interoperabilidad con Java. Esto significa que puede usar fácilmente Kotlin con el código Java existente y viceversa. En esta publicación, veremos cómo interoperar con el código Java en Kotlin y algunos de los beneficios que esto ofrece.

## Llamar código Java desde Kotlin

Uno de los escenarios más comunes es llamar código Java desde Kotlin. Esto suele ser sencillo, ya que Kotlin está diseñado para funcionar bien con Java.

Por ejemplo, digamos que tenemos una clase de Java como esta:

```java
public class MyJavaClass {
    public static void doSomething() {
        System.out.println("Doing something in Java!");
    }
}
```

Podemos llamar al método `doSomething` de Kotlin así:

```kotlin
MyJavaClass.doSomething()
```

Kotlin también facilita llamar a código Java que usa genéricos. Por ejemplo, digamos que tenemos un método Java como este:

```java
public static <T> T getValue(T defaultValue) {
    return defaultValue;
}
```

Podemos llamar a este método desde Kotlin así:

```kotlin
val result = getValue("Hello, world!")
```

Kotlin también es compatible con la función varargs de Java, que permite que un método acepte una cantidad variable de argumentos. Por ejemplo, digamos que tenemos un método Java como este:

```java
public static void printValues(String... values) {
    for (String value : values) {
        System.out.println(value);
    }
}
```

Podemos llamar a este método desde Kotlin así:

```kotlin
printValues("Hello", "world", "!")
```

## Llamar al código Kotlin desde Java

También es posible llamar al código Kotlin desde Java. El código de Kotlin se compila en el código de bytes de Java, por lo que se puede usar como cualquier otro código de Java.

Por ejemplo, digamos que tenemos una clase de Kotlin como esta:

```kotlin
class MyKotlinClass {
    fun doSomething() {
        println("Doing something in Kotlin!")
    }
}
```

Podemos llamar al método `doSomething` desde Java así:

```java
MyKotlinClass kotlinClass = new MyKotlinClass();
kotlinClass.doSomething();
```

Kotlin también admite funciones como genéricos, seguridad nula y lambdas, a las que se puede llamar desde Java.

## Los beneficios de la interoperabilidad

La interoperabilidad entre Kotlin y Java tiene muchos beneficios.

Uno de los mayores beneficios es que permite a los desarrolladores migrar lentamente de Java a Kotlin, sin tener que volver a escribir todo su código base. Esto puede ser una gran ventaja para proyectos con mucho código Java heredado.

Otro beneficio es que permite a los desarrolladores usar lo mejor de ambos lenguajes. Kotlin y Java tienen muchas características que son similares, pero también hay algunas diferencias clave. Al usar ambos lenguajes, los desarrolladores pueden aprovechar las características de cada lenguaje que son más apropiadas para sus necesidades.

## Conclusión

En esta publicación, hemos visto cómo Kotlin interactúa con Java. Hemos visto cómo se puede llamar al código Kotlin desde Java y cómo se puede llamar al código Java desde Kotlin. También hemos visto algunos de los beneficios que esto ofrece.

Si está interesado en obtener más información sobre Kotlin, consulte los recursos a continuación.

## Información adicional

* [Kotlin para desarrolladores de Java](https://kotlinlang.org/docs/reference/java-to-kotlin-interop.html)
* [Interoperabilidad de Java](https://kotlinlang.org/docs/reference/java-interop.html)