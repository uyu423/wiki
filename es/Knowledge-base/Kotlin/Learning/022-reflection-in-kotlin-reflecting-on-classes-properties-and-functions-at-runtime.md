---
title: 022: Reflexión en Kotlin: Reflexión sobre clases, propiedades y funciones en tiempo de ejecución
description: 
published: true
date: 2023-02-01T15:36:34.002Z
tags: 
editor: markdown
dateCreated: 2023-02-01T15:36:32.422Z
---

> Este artículo se tradujo automáticamente con la **API de Google Cloud Translation**.
Algunas páginas pueden leerse mejor que el original.{.is-info}

- [022: Reflection in Kotlin: Reflecting on Classes, Properties, and Functions at Runtime***Spanish** version of this document is available*](/es/Knowledge-base/Kotlin/Learning/022-reflection-in-kotlin-reflecting-on-classes-properties-and-functions-at-runtime)
{.links-list}


# Reflexión en Kotlin

La reflexión de Kotlin es una poderosa herramienta que se puede usar para inspeccionar y manipular el código de Kotlin en tiempo de ejecución. En este artículo, veremos qué es la reflexión y cómo se puede usar para introspeccionar clases, propiedades y funciones de Kotlin.

## ¿Qué es la reflexión?

La reflexión es la capacidad de un programa para inspeccionarse y manipularse a sí mismo en tiempo de ejecución. Esto se puede utilizar para realizar una introspección de la estructura de un programa, invocar métodos dinámicamente e incluso cambiar la estructura de un programa en tiempo de ejecución.

La reflexión es una herramienta poderosa, pero tiene un costo. La reflexión suele ser más lenta que las llamadas a métodos directos y puede dificultar la comprensión del código. Como tal, debe usarse con moderación y solo cuando sea absolutamente necesario.

## Reflexión en Kotlin

La reflexión de Kotlin se basa en la API de Java Reflection. Esto significa que cualquier código que se pueda escribir en Java también se puede escribir en Kotlin. Sin embargo, Kotlin agrega una serie de funciones que facilitan el uso de la reflexión.

Una de las características más importantes de la reflexión de Kotlin es la capacidad de acceder a los miembros de una clase mediante el operador punto. Por ejemplo, considere la siguiente clase de Kotlin:

```kotlin
class Foo {
    fun bar() {}
}
```

Podemos usar la reflexión para acceder a la función `bar()` de esta clase así:

```kotlin
val foo = Foo()
val bar = foo::class.memberFunctions.first { it.name == "bar" }
```

Esto es mucho más simple que el código equivalente en Java, que se vería así:

```java
Foo foo = new Foo();
Method bar = foo.getClass().getDeclaredMethods()[0];
```

Además del operador de punto, la reflexión de Kotlin también proporciona una serie de funciones de alto nivel que facilitan las tareas comunes. Por ejemplo, podemos usar la función `kotlin.reflect.full.declaredMemberProperties` para obtener una lista de todas las propiedades declaradas en una clase:

```kotlin
val foo = Foo()
val properties = kotlin.reflect.full.declaredMemberProperties(foo)
```

Esto es equivalente al siguiente código Java:

```java
Foo foo = new Foo();
Field[] fields = foo.getClass().getDeclaredFields();
```

## Casos de uso para la reflexión

La reflexión se puede utilizar para una serie de tareas diferentes, pero algunos de los casos de uso más comunes se enumeran a continuación:

* **Introspección**: la reflexión se puede utilizar para realizar una introspección de la estructura de un programa de Kotlin. Esto se puede usar para, por ejemplo, generar automáticamente documentación para una biblioteca de Kotlin.

* **Invocación dinámica**: Reflection se puede usar para invocar dinámicamente los métodos de Kotlin. Esto se puede usar, por ejemplo, para invocar métodos que no se conocen en tiempo de compilación.

* **Generación de código en tiempo de ejecución**: Reflection se puede usar para generar código Kotlin en tiempo de ejecución. Esto se puede usar, por ejemplo, para crear dinámicamente clases de Kotlin basadas en la entrada del usuario.

## Limitaciones de la reflexión

La reflexión es una herramienta poderosa, pero tiene una serie de limitaciones. Algunas de las limitaciones más importantes se enumeran a continuación:

* **Seguridad**: Reflection se puede usar para omitir las comprobaciones de seguridad que realiza el compilador de Kotlin. Esto se puede usar, por ejemplo, para invocar dinámicamente métodos privados o para acceder a campos privados.

* **Rendimiento**: la reflexión suele ser más lenta que las llamadas a métodos directos. Esto puede ser un problema, por ejemplo, cuando se usa la reflexión para invocar dinámicamente métodos que se llaman con frecuencia.

* **Confiabilidad**: Reflection se puede usar para cambiar la estructura de un programa de Kotlin en tiempo de ejecución. Esto puede generar problemas, por ejemplo, cuando dos fragmentos de código utilizan la reflexión para introspeccionar la misma clase y uno de ellos cambia la estructura de la clase.

## Conclusión

En este artículo, analizamos qué es la reflexión y cómo se puede usar para realizar una introspección y manipular el código de Kotlin en tiempo de ejecución. También hemos visto algunos de los casos de uso de la reflexión y algunas de las limitaciones del uso de la reflexión.