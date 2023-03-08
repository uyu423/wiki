---
title: 044: Clases internas anónimas en Kotlin: creación de clases sin nombres
description: 
published: true
date: 2023-02-15T10:17:50.202Z
tags: 
editor: markdown
dateCreated: 2023-02-15T10:17:48.491Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [044: Anonymous Inner Classes in Kotlin: Creating Classes Without Names***English** document is available*](/en/Knowledge-base/Kotlin/Learning/044-anonymous-inner-classes-in-kotlin-creating-classes-without-names)
{.links-list}


# Clases internas anónimas en Kotlin: creación de clases sin nombres

En Kotlin, puedes crear clases internas anónimas sin darles un nombre. Estas clases se usan a menudo cuando necesita crear un objeto único o cuando necesita un objeto que solo se usa en un ámbito limitado.

Las clases internas anónimas se declaran usando la palabra clave `objeto`:

```kotlin
object: SomeClass() {
    // Body of the anonymous inner class
}
```

También puede especificar el supertipo para la clase interna anónima usando la palabra clave `objeto`:

```kotlin
object: SomeInterface {
    // Body of the anonymous inner class
}
```

## Crear una clase interna anónima que amplíe una clase

Vamos a crear una clase interna anónima que amplíe la clase `Animal`. Crearemos una clase `Animal` que tenga un método `makeNoise`. Este método se anulará en la clase interna anónima.

```kotlin
open class Animal {
    open fun makeNoise() {
        println("Some noise")
    }
}

val animal = object: Animal() {
    override fun makeNoise() {
        println("Bark")
    }
}

animal.makeNoise() // Prints "Bark"
```

En el código anterior, creamos una clase `Animal` y una clase interna anónima que la amplía. Anulamos el método `makeNoise` en la clase interna anónima. Cuando llamamos al método `makeNoise` en el objeto `animal`, imprime "Bark".

## Creación de una clase interna anónima que implementa una interfaz

También puede crear clases internas anónimas que implementen interfaces. Vamos a crear una interfaz `Animal` con un método `makeNoise`. Crearemos una clase interna anónima que implemente esta interfaz.

```kotlin
interface Animal {
    fun makeNoise()
}

val animal = object: Animal {
    override fun makeNoise() {
        println("Some noise")
    }
}

animal.makeNoise() // Prints "Some noise"
```

En el código anterior, creamos una interfaz `Animal` y una clase interna anónima que la implementa. Anulamos el método `makeNoise` en la clase interna anónima. Cuando llamamos al método `makeNoise` en el objeto `animal`, imprime "Algo de ruido".

## Crear una clase interna anónima que amplíe una clase e implemente una interfaz

También puede crear clases internas anónimas que amplíen una clase e implementen una interfaz. Vamos a crear una interfaz `Animal` con un método `makeNoise`. También crearemos una clase `Animal` que tiene un método `makeNoise`. Crearemos una clase interna anónima que amplíe la clase `Animal` e implemente la interfaz `Animal`.

```kotlin
interface Animal {
    fun makeNoise()
}

open class Animal {
    open fun makeNoise() {
        println("Some noise")
    }
}

val animal = object: Animal(), Animal {
    override fun makeNoise() {
        println("Bark")
    }
}

animal.makeNoise() // Prints "Bark"
```

En el código anterior, creamos una clase `Animal` y una interfaz `Animal`. Creamos una clase interna anónima que amplía la clase `Animal` e implementa la interfaz `Animal`. Anulamos el método `makeNoise` en la clase interna anónima. Cuando llamamos al método `makeNoise` en el objeto `animal`, imprime "Bark".

## Creando un objeto de una clase interna anónima

Cuando crea una clase interna anónima, también se crea un objeto de esa clase. Puede acceder a este objeto utilizando la palabra clave `objeto`.

```kotlin
interface Animal {
    fun makeNoise()
}

open class Animal {
    open fun makeNoise() {
        println("Some noise")
    }
}

val animal = object: Animal(), Animal {
    override fun makeNoise() {
        println("Bark")
    }
}

println(animal.javaClass) // Prints "class com.example.Animal$1"
```

En el código anterior, creamos una clase `Animal` y una interfaz `Animal`. Creamos una clase interna anónima que amplía la clase `Animal` e implementa la interfaz `Animal`. Imprimimos la clase del objeto `animal` usando la propiedad `javaClass`. Como puede ver, el objeto `animal` es una instancia de la clase interna anónima.

## Crear una clase anidada estática

También puede crear clases anidadas estáticas en Kotlin. Las clases anidadas estáticas se declaran usando la palabra clave `static`:

```kotlin
class OuterClass {
    class NestedClass
}
```

Las clases anidadas estáticas pueden acceder a los miembros de la clase externa. También pueden declararse 'abstractos' o 'sellados'.

```kotlin
class OuterClass {
    class NestedClass {
        fun someMethod() {
            println("Some method")
        }
    }
}

val nestedClass = OuterClass.NestedClass()
nestedClass.someMethod() // Prints "Some method"
```

En el código anterior, creamos una clase anidada estática y una instancia de esa clase. Llamamos al método `someMethod` en el objeto `nestedClass`.

## Creando una Clase Interna

Las clases internas son clases anidadas no estáticas. Las clases internas pueden acceder a los miembros de la clase externa. También pueden declararse 'abstractos' o 'sellados'.

```kotlin
class OuterClass {
    inner class InnerClass {
        fun someMethod() {
            println("Some method")
        }
    }
}

val outerClass = OuterClass()
val innerClass = outerClass.InnerClass()
innerClass.someMethod() // Prints "Some method"
```

En el código anterior, creamos una clase interna y una instancia de esa clase. Llamamos al método `someMethod` en el objeto `innerClass`.

## Conclusión

En esta publicación, aprendimos sobre las clases internas anónimas en Kotlin. Vimos cómo crear clases internas anónimas que amplían clases, implementan interfaces y amplían clases e implementan interfaces. También vimos cómo crear clases anidadas estáticas y clases internas.