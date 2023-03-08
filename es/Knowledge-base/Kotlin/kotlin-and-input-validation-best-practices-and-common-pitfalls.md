---
title: Kotlin y validación de entrada: mejores prácticas y errores comunes
description: 
published: true
date: 2023-02-05T11:17:24.394Z
tags: 
editor: markdown
dateCreated: 2023-02-05T11:17:22.765Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin and Input Validation: Best Practices and Common Pitfalls***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-input-validation-best-practices-and-common-pitfalls)
{.links-list}


# Kotlin y validación de entrada: mejores prácticas y errores comunes

## Introducción

La validación de entrada es una parte fundamental de cualquier aplicación, ya sea una aplicación web, una aplicación móvil o una aplicación de escritorio. Sin una validación de entrada adecuada, una aplicación es vulnerable a todo tipo de ataques, incluidos ataques de inyección SQL, secuencias de comandos entre sitios (XSS) y ataques de intermediario (MITM).

En este artículo, veremos algunas de las mejores prácticas para la validación de entrada en Kotlin, así como algunos errores comunes que se deben evitar.

## Mejores prácticas

### 1. Use la herramienta adecuada para el trabajo

Hay muchas bibliotecas y marcos diferentes disponibles para la validación de entrada en Kotlin. Es importante elegir el adecuado para el trabajo, en función de los requisitos del proyecto.

Por ejemplo, la biblioteca kotlinx.html proporciona un conjunto de funciones y objetos para validar la entrada HTML. La biblioteca kotlinx.validation proporciona un conjunto de funciones y objetos para validar la entrada XML.

### 2. Defina las reglas de validación por adelantado

Antes de comenzar a codificar, es importante definir las reglas de validación que deben implementarse. Esto ayudará a evitar la duplicación de código y hará que el código sea más fácil de mantener.

### 3. Usa tipos explícitos

Al definir reglas de validación, es mejor usar tipos explícitos. Por ejemplo, en lugar de usar el tipo Any, es mejor usar el tipo específico, como String o Int.

### 4. Evite el uso de tipos anulables

Los tipos que aceptan valores NULL deben evitarse cuando sea posible, ya que pueden generar resultados inesperados. Si un tipo anulable es absolutamente necesario, es mejor usar una biblioteca que proporcione seguridad nula, como la biblioteca kotlinx.validation.

### 5. Usa afirmaciones positivas

Al escribir código de validación, es mejor usar aserciones positivas. En otras palabras, el código de validación debe verificar la presencia de un valor particular, en lugar de la ausencia de un valor.

### 6. Tenga cuidado con los cortocircuitos

El comportamiento de cortocircuito de Kotlin puede generar resultados inesperados cuando se usa junto con la validación de entrada. Por ejemplo, considere el siguiente código:

```kotlin
fun validateInput(input: String): Boolean {
    // Validation code here
}

fun main() {
    val input = "test"
    if (validateInput(input) && input.isNotEmpty()) {
        // Do something with the input
    }
}
```

En este código, primero se llama a la función validateInput() y luego se llama a la función input.isNotEmpty(). Sin embargo, debido al comportamiento de cortocircuito de Kotlin, nunca se llamará a la función input.isNotEmpty() si la función validateInput() devuelve falso.

Para evitar este problema, es mejor usar la función let(), de la siguiente manera:

```kotlin
fun validateInput(input: String): Boolean {
    // Validation code here
}

fun main() {
    val input = "test"
    input.let {
        if (validateInput(it) && it.isNotEmpty()) {
            // Do something with the input
        }
    }
}
```

En este código, la función let() se usa para invocar la función validateInput() y la función input.isNotEmpty(). Esto garantiza que siempre se llame a ambas funciones, independientemente del valor de retorno de la función validateInput().

## Errores comunes

### 1. Entrada no validada

Uno de los errores más comunes que se cometen al codificar es no validar la entrada. Esto puede conducir a todo tipo de problemas de seguridad, así como a la corrupción de datos.

Es importante validar siempre la entrada, incluso si proviene de una fuente confiable.

### 2. Confiar en la validación del lado del cliente

Otro error común es confiar en la validación del lado del cliente, como la validación de formularios HTML5. Si bien la validación del lado del cliente puede ser útil, nunca debe usarse como el único medio de validación.

Esto se debe a que los usuarios malintencionados pueden omitir la validación del lado del cliente. Por lo tanto, también es importante validar siempre la entrada en el lado del servidor.

### 3. Solo validar para caracteres específicos

Un error común cuando se valida la entrada es verificar solo caracteres específicos, como caracteres alfanuméricos. Sin embargo, esto puede generar problemas de seguridad, ya que los usuarios maliciosos pueden eludir la validación utilizando otros caracteres.

Es importante validar siempre la entrada con una lista blanca de caracteres permitidos, en lugar de una lista negra de caracteres no permitidos.

### 4. Salida no higienizante

Otro error común es olvidarse de desinfectar la salida. Esto puede generar problemas de seguridad, como ataques de secuencias de comandos entre sitios (XSS).

Es importante desinfectar siempre la salida antes de mostrársela al usuario.

### 5. Usar una sola expresión regular para todas las entradas

Un error común al usar expresiones regulares (regex) para la validación de entrada es usar una única expresión regular para todas las entradas. Sin embargo, esto puede generar problemas de rendimiento, ya que será necesario volver a compilar la expresión regular para cada entrada.

Es mejor usar una expresión regular diferente para cada entrada, o compilar la expresión regular de antemano.

## Conclusión

La validación de entrada es una parte crítica de cualquier aplicación. En este artículo, cubrimos algunas de las mejores prácticas para la validación de entrada en Kotlin, así como algunos errores comunes que se deben evitar.