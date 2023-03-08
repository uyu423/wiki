---
title: 062: El patrón Singleton en Kotlin: garantizar que solo exista una instancia de una clase
description: 
published: true
date: 2023-02-16T23:32:26.287Z
tags: 
editor: markdown
dateCreated: 2023-02-16T23:32:18.300Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [062: The Singleton Pattern in Kotlin: Ensuring Only One Instance of a Class Exists***English** document is available*](/en/Knowledge-base/Kotlin/Learning/062-the-singleton-pattern-in-kotlin-ensuring-only-one-instance-of-a-class-exists)
{.links-list}


# El patrón Singleton en Kotlin: garantizar que solo exista una instancia de una clase

El patrón singleton es un patrón de diseño de software que restringe la instanciación de una clase a un objeto. Esto es útil cuando necesitamos tener solo una instancia de una clase para la aplicación, como cuando necesitamos administrar un recurso compartido, manejar un estado global o coordinar acciones en todo el sistema.

En Kotlin, podemos implementar un singleton usando una declaración de objeto. Una declaración de objeto es un azúcar sintáctico para una clase normal con un constructor privado y un campo estático público para almacenar la instancia.

Aquí hay un ejemplo simple de una clase singleton en Kotlin:

```kotlin
object MySingleton {
    fun doSomething() {
        // ...
    }
}
```

Podemos acceder a la instancia de singleton usando el nombre del objeto:

```kotlin
MySingleton.doSomething()
```

Si necesitamos inicializar el singleton con algunos parámetros, podemos usar un objeto complementario:

```kotlin
class MySingleton private constructor(val param: String) {
    companion object {
        fun getInstance(param: String): MySingleton {
            return MySingleton(param)
        }
    }

    fun doSomething() {
        // ...
    }
}
```

Luego podemos acceder a la instancia de singleton usando el nombre del objeto complementario:

```kotlin
MySingleton.getInstance("some param").doSomething()
```

Es importante tener en cuenta que, en Kotlin, la declaración del objeto no es segura para subprocesos. Si necesitamos asegurarnos de que solo se cree una instancia de la clase, debemos usar un bloque sincronizado:

```kotlin
object MySingleton {
    @Volatile
    private var instance: MySingleton? = null

    fun getInstance(): MySingleton {
        return instance ?: synchronized(this) {
            instance ?: MySingleton().also { instance = it }
        }
    }

    fun doSomething() {
        // ...
    }
}
```

Luego podemos acceder a la instancia de singleton usando el nombre del objeto:

```kotlin
MySingleton.getInstance().doSomething()
```

El patrón singleton es una herramienta útil para administrar el estado y los recursos globales. Sin embargo, debe usarse con precaución, ya que puede dar lugar a un código estrechamente acoplado y a un código difícil de probar.

## Información adicional

* [Wikipedia: Patrón Singleton](https://en.wikipedia.org/wiki/Singleton_pattern)
* [Documentación del lenguaje Kotlin: Objetos](https://kotlinlang.org/docs/reference/objects.html)

## Recursos para lecturas adicionales

* [Patrones de diseño en Kotlin: The Singleton Pattern](https://antonioleiva.com/kotlin-singleton/)
* [Reino: El debate de Kotlin Singleton](https://academy.realm.io/posts/kotlin-singleton-debate/)
* [Desarrolladores de Android: Singletons y fugas de memoria](https://developer.android.com/training/articles/memory.html# LeakCanary)