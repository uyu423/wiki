---
title: 090: Procesamiento de anotaciones en Kotlin: generación de código en tiempo de compilación con procesamiento de anotaciones
description: 
published: true
date: 2023-02-16T05:18:20.255Z
tags: 
editor: markdown
dateCreated: 2023-02-16T05:18:12.413Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [090: Annotation Processing in Kotlin: Generating Code at Compile-Time with Annotation Processing***English** document is available*](/en/Knowledge-base/Kotlin/Learning/090-annotation-processing-in-kotlin-generating-code-at-compile-time-with-annotation-processing)
{.links-list}


# Procesamiento de anotaciones en Kotlin: generación de código en tiempo de compilación con procesamiento de anotaciones

El procesamiento de anotaciones es una poderosa herramienta para la generación de código en Kotlin. Mediante el uso de procesadores de anotaciones, podemos generar código en tiempo de compilación, que se puede usar en nuestras aplicaciones de Kotlin.

En esta publicación, veremos cómo usar los procesadores de anotaciones para generar código en Kotlin. Exploraremos qué son los procesadores de anotaciones y cómo funcionan. También veremos cómo escribir nuestros propios procesadores de anotaciones y usarlos en nuestras aplicaciones Kotlin.

## ¿Qué son los procesadores de anotaciones?

Los procesadores de anotaciones son programas que se ejecutan durante la compilación de nuestro código y generan código basado en las anotaciones presentes en nuestro código. Podemos usar procesadores de anotaciones para generar código repetitivo, para validar nuestro código o para realizar cualquier otra tarea que se pueda automatizar.

Los procesadores de anotaciones están escritos en Kotlin o Java y se ejecutan con el compilador kotlinc. Podemos escribir nuestros propios procesadores de anotaciones o utilizar los que proporcionan las bibliotecas de terceros.

## ¿Cómo funcionan los procesadores de anotaciones?

Los procesadores de anotaciones son ejecutados por el compilador kotlinc cuando compila nuestro código. El compilador kotlinc primero compila el código sin ejecutar los procesadores de anotaciones. Esto permite que los procesadores de anotaciones accedan al código fuente y al código de bytes compilado.

Después de la compilación inicial, el compilador kotlinc ejecuta los procesadores de anotaciones. Luego, los procesadores de anotaciones pueden generar código, que se compila y se agrega al resultado final de la compilación.

## Escribiendo nuestro propio procesador de anotaciones

Escribamos nuestro propio procesador de anotaciones para generar código repetitivo. Comenzaremos creando un nuevo proyecto de Kotlin en IntelliJ IDEA.

![Crear proyecto Kotlin](https://i.imgur.com/p0lC5Nq.png)

Nombraremos a nuestro proyecto "Procesador de anotaciones" y dejaremos la configuración predeterminada para la estructura del proyecto.

![Estructura del proyecto](https://i.imgur.com/gY0CWt6.png)

A continuación, crearemos un nuevo archivo Kotlin en el directorio `src/main/kotlin`. Llamaremos a este archivo "GenerateBoilerplate.kt".

En este archivo, escribiremos nuestro procesador de anotaciones. Comenzaremos definiendo una nueva anotación llamada `@GenerateBoilerplate`.

```kotlin
@Retention(AnnotationRetention.SOURCE)
@Target(AnnotationTarget.CLASS)
annotation class GenerateBoilerplate
```

Esta anotación se puede utilizar en las clases. Se conservará en el código fuente, pero no estará presente en el código de bytes compilado.

A continuación, escribiremos una función para generar el código repetitivo para una clase anotada con `@GenerateBoilerplate`. Esta función tomará una `Class<*>` como parámetro y devolverá una `String` que contiene el código generado.

```kotlin
fun generateBoilerplate(clazz: Class<*>): String {
    val className = clazz.simpleName
    return "class $className {\n}\n"
}
```

Esta función simplemente generará una declaración de `clase` con el nombre de la clase anotada.

Ahora que hemos escrito nuestra función para generar el código repetitivo, escribiremos nuestro procesador de anotaciones. Comenzaremos definiendo una nueva clase llamada `GenerateBoilerplateProcessor`. Esta clase extenderá la clase `AbstractProcessor`.

```kotlin
class GenerateBoilerplateProcessor : AbstractProcessor() {
}
```

A continuación, anularemos la función `proceso`. El compilador kotlinc llamará a esta función cuando ejecute nuestro procesador de anotaciones.

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
}
```

Esta función toma dos parámetros. El primer parámetro es un conjunto de anotaciones que debe procesar el procesador. El segundo parámetro es el entorno en el que se ejecuta el procesador.

Podemos usar el parámetro `roundEnv` para acceder a los elementos anotados en nuestro código. Usaremos la función `getElementsAnnotatedWith` para obtener una lista de elementos anotados con nuestra anotación `@GenerateBoilerplate`.

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
    val annotatedElements = roundEnv.getElementsAnnotatedWith(GenerateBoilerplate::class.java)
}
```

Luego podemos iterar sobre esta lista y generar el código repetitivo para cada elemento anotado.

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
    val annotatedElements = roundEnv.getElementsAnnotatedWith(GenerateBoilerplate::class.java)

    for (element in annotatedElements) {
        val clazz = element as TypeElement
        val generatedCode = generateBoilerplate(clazz)
    }
}
```

Finalmente, escribiremos el código generado en un archivo. Usaremos la clase `Filer` para crear un nuevo archivo. La clase `Filer` es parte del paquete `javax.annotation.processing`.

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
    val annotatedElements = roundEnv.getElementsAnnotatedWith(GenerateBoilerplate::class.java)

    for (element in annotatedElements) {
        val clazz = element as TypeElement
        val generatedCode = generateBoilerplate(clazz)

        val filer = processingEnv.filer
        val file = filer.createSourceFile(clazz.qualifiedName.toString())
    }
}
```

Usaremos la función `createSourceFile` para crear un nuevo archivo. Usaremos el nombre completo del elemento anotado como el nombre del archivo.

Entonces podemos escribir el código generado en el archivo usando la clase `Writer`.

```kotlin
override fun process(
    annotations: MutableSet<out TypeElement>?,
    roundEnv: RoundEnvironment
): Boolean {
    val annotatedElements = roundEnv.getElementsAnnotatedWith(GenerateBoilerplate::class.java)

    for (element in annotatedElements) {
        val clazz = element as TypeElement
        val generatedCode = generateBoilerplate(clazz)

        val filer = processingEnv.filer
        val file = filer.createSourceFile(clazz.qualifiedName.toString())

        val writer = file.openWriter()
        writer.write(generatedCode)
        writer.close()
    }
}
```

Ahora que hemos escrito nuestro procesador de anotaciones, podemos usarlo en nuestro código Kotlin. Crearemos un nuevo archivo Kotlin en el directorio `src/main/kotlin`. Llamaremos a este archivo "Main.kt".

En este archivo, anotaremos una clase con nuestra anotación `@GenerateBoilerplate`.

```kotlin
@GenerateBoilerplate
class Foo
```

Cuando compilamos este código, el compilador kotlinc ejecutará nuestro procesador de anotaciones. Nuestro procesador de anotaciones generará el siguiente código:

```kotlin
class Foo {
}
```

## Uso de procesadores de anotación en nuestras aplicaciones de Kotlin

Ahora que hemos visto cómo escribir nuestros propios procesadores de anotaciones, echemos un vistazo a cómo usarlos en nuestras aplicaciones de Kotlin.

Comenzaremos agregando el complemento `kotlin-annotation-processing` a nuestro archivo `build.gradle`.

```groovy
plugins {
    id "org.jetbrains.kotlin.plugin.allopen" version "1.3.72"
}
```

Luego podemos configurar el complemento `kotlin-annotation-processing` para ejecutar nuestro procesador de anotaciones. Agregaremos la siguiente configuración a nuestro archivo `build.gradle`.

```groovy
kotlinAnnotationProcessing {
    processors = [
            "com.example.GenerateBoilerplateProcessor"
    ]
}
```

Ahora podemos usar nuestro procesador de anotaciones en nuestro código Kotlin. Crearemos un nuevo archivo Kotlin en el directorio `src/main/kotlin`. Llamaremos a este archivo "Main.kt".

En este archivo, anotaremos una clase con nuestra anotación `@GenerateBoilerplate`.

```kotlin
@GenerateBoilerplate
class Foo
```

Cuando compilamos este código, el compilador kotlinc ejecutará nuestro procesador de anotaciones. Nuestro procesador de anotaciones generará el siguiente código:

```kotlin
class Foo {
}
```

## Conclusión

En esta publicación, hemos visto cómo usar procesadores de anotaciones para generar código en Kotlin. Hemos visto cómo escribir nuestros propios procesadores de anotaciones y cómo usarlos en nuestras aplicaciones Kotlin.