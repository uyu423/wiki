---
title: 082: Pruebas en Kotlin: escribir y ejecutar pruebas para su código Kotlin
description: 
published: true
date: 2023-02-10T22:55:25.937Z
tags: 
editor: markdown
dateCreated: 2023-02-10T22:55:24.346Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [082: Testing in Kotlin: Writing and Running Tests for Your Kotlin Code***English** document is available*](/en/Knowledge-base/Kotlin/Learning/082-testing-in-kotlin-writing-and-running-tests-for-your-kotlin-code)
{.links-list}


# 082: Pruebas en Kotlin: escribir y ejecutar pruebas para su código Kotlin

La prueba es una parte crítica del proceso de desarrollo de software. Ayuda a garantizar que su código sea correcto y funcione como se esperaba. En esta publicación, aprenderemos cómo escribir y ejecutar pruebas para el código de Kotlin.

## Pruebas de escritura

Las pruebas están escritas en Kotlin utilizando el marco [JUnit](https://junit.org/). JUnit es un marco de prueba popular para Java que se puede usar para proyectos de Kotlin.

Para escribir una prueba, cree un nuevo archivo Kotlin en su proyecto y anótelo con la anotación `@Test`. Esta anotación le dice al marco JUnit que el código en este archivo es una prueba.

```kotlin
@Test
fun test() {
    // code for the test goes here
}
```

Las pruebas generalmente se componen de tres partes: configuración, ejecución y verificación. En la fase de configuración, inicializará todos los objetos o datos necesarios para la prueba. En la fase de ejecución, ejecutará el código que está probando. En la fase de verificación, afirmará que el código se comportó como se esperaba.

Veamos un ejemplo sencillo. Supongamos que tenemos una función que calcula el factorial de un número. Podemos escribir una prueba para esta función usando la siguiente plantilla:

```kotlin
@Test
fun test() {
    // setup
    val input = 5

    // execution
    val output = factorial(input)

    // verification
    assertEquals(120, output)
}
```

En la fase de configuración, creamos una variable `input` y la configuramos en `5`. En la fase de ejecución, llamamos a la función `factorial` con `input` como argumento. Esta función devuelve el factorial de `input`, que almacenamos en la variable `output`. En la fase de verificación, usamos la función `assertEquals` para afirmar que `output` es igual a `120`.

Si ejecutamos esta prueba y pasa, podemos estar seguros de que nuestra función `factorial` está funcionando correctamente.

## Ejecución de pruebas

Las pruebas se pueden ejecutar desde la línea de comandos o desde dentro de un IDE. Para ejecutar pruebas desde la línea de comandos, deberá usar la herramienta de compilación [Gradle](https://gradle.org/). Gradle es una herramienta de compilación para proyectos Java que se puede usar para proyectos Kotlin.

Para ejecutar pruebas desde la línea de comandos, navegue hasta el directorio raíz de su proyecto y ejecute el siguiente comando:

```
gradle test
```

Esto ejecutará todas las pruebas en su proyecto.

Para ejecutar pruebas desde un IDE, deberá instalar el [complemento JUnit](https://plugins.gradle.org/plugin/org.junit.platform.idea) para su IDE. Una vez que se instala el complemento, debería poder ejecutar pruebas desde su IDE.

## Información adicional

- [Sitio web de JUnit](https://junit.org/)
- [Documentación JUnit](https://junit.org/junit5/docs/current/user-guide/)
- [Sitio web de Gradle] (https://gradle.org/)
- [Documentación de Gradle] (https://docs.gradle.org/current/userguide/userguide.html)