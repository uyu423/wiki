---
title: 040: Objetos complementarios en Kotlin: Implementación de miembros estáticos
description: 
published: true
date: 2023-02-16T12:32:59.749Z
tags: 
editor: markdown
dateCreated: 2023-02-16T12:32:58.129Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [040: Companion Objects in Kotlin: Implementing Static Members***English** document is available*](/en/Knowledge-base/Kotlin/Learning/040-companion-objects-in-kotlin-implementing-static-members)
{.links-list}




Los objetos complementarios son una excelente manera de implementar miembros estáticos en Kotlin. Al usar objetos complementarios, puede evitar tener que crear una clase separada para cada miembro estático.

Para crear un objeto complementario, simplemente agregue la palabra clave "compañero" antes de la declaración del objeto. Por ejemplo, para crear un objeto complementario para una clase denominada "MyClass", agregaría el siguiente código:

```kotlin
class MyClass {
    companion object {
        // ...
    }
}
```

Dentro del objeto complementario, puede agregar los miembros estáticos que desee. Por ejemplo, podría agregar un campo estático como este:

```kotlin
class MyClass {
    companion object {
        val myField = "Hello, world!"
    }
}
```

También puede agregar métodos estáticos. Por ejemplo, podría agregar un método estático llamado "myMethod" como este:

```kotlin
class MyClass {
    companion object {
        fun myMethod() {
            // ...
        }
    }
}
```

Para acceder a los miembros del objeto complementario, utilice el nombre de la clase seguido del nombre del objeto complementario. Por ejemplo, para acceder al campo "myField", usaría el siguiente código:

```kotlin
MyClass.myField // "Hello, world!"
```

Y para llamar al método "myMethod", usaría el siguiente código:

```kotlin
MyClass.myMethod()
```

Una ventaja de usar objetos complementarios es que puede evitar colisiones de nombres. Por ejemplo, suponga que tiene una clase llamada "Foo" y otra clase llamada "Bar". Si ambas clases tienen un campo estático llamado "myField", puede acceder a cada campo usando el siguiente código:

```kotlin
Foo.myField // accesses the "myField" field in the "Foo" class
Bar.myField // accesses the "myField" field in the "Bar" class
```

Otra ventaja de usar objetos complementarios es que puede acceder a miembros privados del objeto complementario desde fuera del objeto. Por ejemplo, suponga que tiene un objeto complementario con un campo privado llamado "myField":

```kotlin
class MyClass {
    companion object {
        private val myField = "Hello, world!"
    }
}
```

Puede acceder a este campo desde fuera del objeto complementario utilizando el siguiente código:

```kotlin
MyClass.Companion.myField // "Hello, world!"
```

Esto puede ser útil si desea crear un método de fábrica estático que devuelva una instancia del objeto complementario. Por ejemplo, podría crear un método de fábrica estático llamado "crear" como este:

```kotlin
class MyClass {
    companion object {
        private val myField = "Hello, world!"
        
        fun create(): MyClass {
            return MyClass()
        }
    }
}
```

Luego puede llamar a este método desde fuera del objeto complementario usando el siguiente código:

```kotlin
MyClass.Companion.create() // creates and returns an instance of the "MyClass" class
```

Una desventaja de usar objetos complementarios es que pueden hacer que su código sea más difícil de leer. Por ejemplo, suponga que tiene una clase llamada "Foo" con un objeto complementario. Si desea acceder a un miembro del objeto complementario, debe usar el nombre completo del objeto:

```kotlin
Foo.Companion.myField // accesses the "myField" field in the "Foo" class
```

Esto puede hacer que su código sea más difícil de leer, especialmente si accede con frecuencia a miembros del objeto complementario.

Otra desventaja de usar objetos complementarios es que no se pueden heredar. Por ejemplo, suponga que tiene una clase llamada "Foo" con un objeto complementario. Si crea una subclase de "Foo", la subclase no heredará el objeto complementario:

```kotlin
class Foo {
    companion object {
        // ...
    }
}

class FooSubclass: Foo {
    // does not inherit the companion object from the "Foo" class
}
```

Esto puede ser un problema si desea crear un método de fábrica estático en la subclase. Por ejemplo, suponga que desea crear un método de fábrica estático en "FooSubclass" que devuelve una instancia de "FooSubclass". No puede hacer esto porque "FooSubclass" no hereda el objeto complementario de la clase "Foo":

```kotlin
class Foo {
    companion object {
        // ...
    }
}

class FooSubclass: Foo {
    companion object {
        fun create(): FooSubclass { // error: does not inherit the companion object from the "Foo" class
            return FooSubclass()
        }
    }
}
```

Si desea poder heredar el objeto complementario, puede usar una clase anidada en su lugar. Por ejemplo, podría crear una clase anidada llamada "Compañero" como esta:

```kotlin
class Foo {
    class Companion {
        // ...
    }
}
```

La clase "Compañero" puede ser heredada por subclases:

```kotlin
class Foo {
    class Companion {
        // ...
    }
}

class FooSubclass: Foo() {
    class Companion: Foo.Companion() {
        fun create(): FooSubclass {
            return FooSubclass()
        }
    }
}
```

En resumen, los objetos complementarios son una excelente forma de implementar miembros estáticos en Kotlin. Tienen las ventajas de poder evitar colisiones de nombres y poder acceder a miembros privados desde fuera del objeto. Sin embargo, tienen la desventaja de ser más difíciles de leer y no poder ser heredados.