---
title: 065: El patrón del método de plantilla en Kotlin: definición de un algoritmo común con pasos personalizados
description: 
published: true
date: 2023-02-17T01:32:35.307Z
tags: 
editor: markdown
dateCreated: 2023-02-17T01:32:33.656Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [065: The Template Method Pattern in Kotlin: Defining a Common Algorithm with Custom Steps***English** document is available*](/en/Knowledge-base/Kotlin/Learning/065-the-template-method-pattern-in-kotlin-defining-a-common-algorithm-with-custom-steps)
{.links-list}


# El patrón del método de plantilla en Kotlin: definición de un algoritmo común con pasos personalizados

En ingeniería de software, el patrón de método de plantilla es un patrón de diseño de comportamiento que define el esqueleto del programa de un algoritmo en una clase base, pero permite que sus subclases proporcionen una implementación concreta para una parte o la totalidad del algoritmo.

El patrón de método de plantilla es una técnica poderosa para la reutilización de código y para definir la estructura de un algoritmo, pero debe usarse con cuidado. En particular, los métodos de plantilla deben usarse solo cuando es apropiado definir un algoritmo en términos de sus pasos, y cuando se puede esperar razonablemente que esos pasos se implementen de manera diferente por diferentes subclases.

## ¿Qué es el patrón del método de plantilla?

El patrón de método de plantilla es un patrón de diseño de comportamiento que define el esqueleto del programa de un algoritmo en una clase base, pero permite que sus subclases proporcionen una implementación concreta para una parte o la totalidad del algoritmo.

El patrón de método de plantilla es una técnica poderosa para la reutilización de código y para definir la estructura de un algoritmo, pero debe usarse con cuidado. En particular, los métodos de plantilla deben usarse solo cuando es apropiado definir un algoritmo en términos de sus pasos, y cuando se puede esperar razonablemente que esos pasos se implementen de manera diferente por diferentes subclases.

En el patrón de método de plantilla, los pasos del algoritmo se implementan en métodos que son abstractos o tienen una implementación predeterminada. Estos métodos se denominan métodos de plantilla. Los métodos de plantilla definen la estructura general del algoritmo, mientras que los detalles de implementación concretos los proporcionan los métodos que son abstractos o tienen una implementación predeterminada.

El patrón de método de plantilla se usa a menudo en marcos, donde el marco define la estructura general de un algoritmo o aplicación, mientras que el usuario del marco proporciona los detalles concretos.

## ¿Cuándo usar el patrón del método de plantilla?

El patrón de método de plantilla debe usarse cuando desee definir un algoritmo en términos de sus pasos, y cuando se puede esperar razonablemente que esos pasos se implementen de manera diferente por diferentes subclases.

En particular, el patrón del método de plantilla es útil cuando:

* Debe definir un algoritmo que se pueda descomponer en una serie de pasos.

* Se espera que diferentes subclases implementen uno o más de los pasos del algoritmo de manera diferente.

* El orden en que se ejecutan los pasos es importante.

* Desea encapsular los detalles de implementación del algoritmo en una clase base, para que puedan cambiarse fácilmente sin afectar las subclases.

## ¿Cómo implementar el patrón del método de plantilla?

El patrón del método de plantilla se puede implementar en Kotlin mediante herencia o delegación.

### Herencia

Cuando se utiliza la herencia, la clase base define la estructura general del algoritmo, mientras que las subclases proporcionan los detalles de implementación concretos.

Para implementar el patrón del método de plantilla usando la herencia, necesitamos:

* Defina una clase base abstracta que contenga el método de plantilla.

* Definir subclases concretas que invaliden los métodos de la clase base para proporcionar la implementación deseada.

Por ejemplo, considere una aplicación que necesita registrar mensajes en un archivo. Podemos definir una clase base que contenga el método de plantilla para registrar mensajes y subclases concretas que invaliden los métodos para proporcionar la implementación deseada.

```kotlin
abstract class Logger {
    fun log(message: String) {
        openFile()
        writeFile(message)
        closeFile()
    }

    abstract fun openFile()
    abstract fun writeFile(message: String)
    abstract fun closeFile()
}

class FileLogger: Logger() {
    override fun openFile() {
        // ...
    }

    override fun writeFile(message: String) {
        // ...
    }

    override fun closeFile() {
        // ...
    }
}

class ConsoleLogger: Logger() {
    override fun openFile() {
        // ...
    }

    override fun writeFile(message: String) {
        // ...
    }

    override fun closeFile() {
        // ...
    }
}
```

En el ejemplo anterior, la clase base define el método de plantilla ```log()``` que contiene la estructura general del algoritmo. El método ```log()``` llama a los métodos ```openFile()```, ```writeFile()``` y ```closeFile()```, que se implementan de manera diferente las subclases.

### Delegación

Cuando se utiliza la delegación, la clase base define la estructura general del algoritmo, mientras que los detalles de implementación concretos los proporciona un objeto delegado.

Para implementar el patrón del método de plantilla usando la delegación, necesitamos:

* Definir una clase base que contenga el método de plantilla.

* Defina una clase de delegado que contenga los métodos que llamará el método de plantilla.

* Cree una instancia de la clase delegada en la clase base y pásela al método de plantilla.

Por ejemplo, considere una aplicación que necesita registrar mensajes en un archivo. Podemos definir una clase base que contenga el método de plantilla para registrar mensajes y una clase delegada que contenga los métodos que llamará el método de plantilla.

```kotlin
class Logger(val delegate: LoggerDelegate) {
    fun log(message: String) {
        delegate.openFile()
        delegate.writeFile(message)
        delegate.closeFile()
    }
}

class FileLoggerDelegate: LoggerDelegate {
    override fun openFile() {
        // ...
    }

    override fun writeFile(message: String) {
        // ...
    }

    override fun closeFile() {
        // ...
    }
}

class ConsoleLoggerDelegate: LoggerDelegate {
    override fun openFile() {
        // ...
    }

    override fun writeFile(message: String) {
        // ...
    }

    override fun closeFile() {
        // ...
    }
}
```

En el ejemplo anterior, la clase base define el método de plantilla ```log()``` que contiene la estructura general del algoritmo. El método ```log()``` llama a los métodos ```openFile()```, ```writeFile()``` y ```closeFile()``` del objeto delegado. Los detalles de implementación concretos los proporcionan las clases delegadas.

## Ventajas del patrón de método de plantilla

El patrón del método de plantilla tiene las siguientes ventajas:

* Encapsula los detalles de implementación de un algoritmo en una clase base, para que puedan cambiarse fácilmente sin afectar las subclases.

* Le permite definir la estructura general de un algoritmo en una clase base, al tiempo que permite que las subclases proporcionen una implementación concreta para algunos o todos los pasos.

* Promueve la reutilización de código al permitirle definir código común en una clase base que todas las subclases pueden reutilizar.

* Es fácil de extender al permitirle agregar nuevos pasos al algoritmo sin afectar el código existente.

## Desventajas del patrón del método de plantilla

El patrón del método de plantilla tiene las siguientes desventajas:

* Puede conducir a la duplicación de código si se necesita el mismo algoritmo en varios lugares con solo variaciones menores. En tales casos, normalmente es mejor extraer el código común en una función o método separado.

* Puede hacer que el código sea más difícil de entender y mantener si el algoritmo es demasiado complejo. En tales casos, normalmente es mejor refactorizar el código para hacerlo más legible y mantenible.

## Conclusión

El patrón de método de plantilla es una técnica poderosa para la reutilización de código y para definir la estructura de un algoritmo, pero debe usarse con cuidado. En particular, los métodos de plantilla deben usarse solo cuando es apropiado definir un algoritmo en términos de sus pasos, y cuando se puede esperar razonablemente que esos pasos se implementen de manera diferente por diferentes subclases.