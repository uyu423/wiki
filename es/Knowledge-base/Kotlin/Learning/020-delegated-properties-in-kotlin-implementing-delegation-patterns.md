---
title: 020: Propiedades delegadas en Kotlin: Implementando patrones de delegación
description: 
published: true
date: 2023-02-16T06:33:37.730Z
tags: 
editor: markdown
dateCreated: 2023-02-16T06:33:28.012Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [020: Delegated Properties in Kotlin: Implementing Delegation Patterns***English** document is available*](/en/Knowledge-base/Kotlin/Learning/020-delegated-properties-in-kotlin-implementing-delegation-patterns)
{.links-list}


# Propiedades delegadas en Kotlin: Implementando patrones de delegación

El modelo de delegación de Kotlin se basa en la idea de delegación por delegación. En este patrón, un objeto (el delegado) es responsable de manejar una solicitud de otro objeto (el delegador). El delegante puede delegar todas o parte de sus responsabilidades al delegado.

En Kotlin, la delegación es una función de lenguaje de primera clase. Puede utilizar la delegación para implementar patrones de diseño comunes, como el patrón Observer, el patrón Decorator y el patrón Factory. La delegación también se puede utilizar para mejorar el rendimiento de su código.

En esta publicación, veremos más de cerca las propiedades delegadas en Kotlin. Aprenderemos a crear y usar propiedades delegadas y exploraremos algunos de los beneficios de usar la delegación.

## ¿Qué son las propiedades delegadas?

Una propiedad delegada es una propiedad cuyo valor es calculado por un delegado. Un delegado es un objeto que sabe cómo calcular el valor de una propiedad. En Kotlin, puedes crear una propiedad delegada usando la palabra clave `by`.

Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by lazy {
        // compute the name
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una instancia de la clase `Lazy`. La clase `Lazy` sabe cómo calcular el valor de la propiedad `name`.

Cuando acceda a la propiedad `nombre`, la instancia `Lazy` calculará el valor de la propiedad y lo devolverá. El valor se almacenará en caché, por lo que los accesos posteriores a la propiedad serán rápidos.

## Creación de propiedades delegadas

Como vimos en la sección anterior, puede crear una propiedad delegada usando la palabra clave `by`. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by lazy {
        // compute the name
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una instancia de la clase `Lazy`. La clase `Lazy` sabe cómo calcular el valor de la propiedad `name`.

Cuando acceda a la propiedad `nombre`, la instancia `Lazy` calculará el valor de la propiedad y lo devolverá. El valor se almacenará en caché, por lo que los accesos posteriores a la propiedad serán rápidos.

También puede crear una propiedad delegada mediante un delegado de propiedad. Un delegado de propiedad es un objeto que sabe cómo calcular el valor de una propiedad. En Kotlin, puedes crear un delegado de propiedad usando la palabra clave `by`.

Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Puede crear esta propiedad utilizando un delegado de propiedad:

```kotlin
class User {
    val name: String by NameDelegate()
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una instancia de la clase `NameDelegate`. La clase `NameDelegate` sabe cómo calcular el valor de la propiedad `name`.

Cuando accede a la propiedad `name`, la instancia `NameDelegate` calculará el valor de la propiedad y lo devolverá. El valor se almacenará en caché, por lo que los accesos posteriores a la propiedad serán rápidos.

## Implementando un Delegado

En Kotlin, puedes crear un delegado usando la palabra clave `by`. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by lazy {
        // compute the name
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una instancia de la clase `Lazy`. La clase `Lazy` sabe cómo calcular el valor de la propiedad `name`.

Cuando acceda a la propiedad `nombre`, la instancia `Lazy` calculará el valor de la propiedad y lo devolverá. El valor se almacenará en caché, por lo que los accesos posteriores a la propiedad serán rápidos.

También puede crear un delegado mediante un delegado de propiedad. Un delegado de propiedad es un objeto que sabe cómo calcular el valor de una propiedad. En Kotlin, puedes crear un delegado de propiedad usando la palabra clave `by`.

Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Puede crear esta propiedad utilizando un delegado de propiedad:

```kotlin
class User {
    val name: String by NameDelegate()
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una instancia de la clase `NameDelegate`. La clase `NameDelegate` sabe cómo calcular el valor de la propiedad `name`.

Cuando accede a la propiedad `name`, la instancia `NameDelegate` calculará el valor de la propiedad y lo devolverá. El valor se almacenará en caché, por lo que los accesos posteriores a la propiedad serán rápidos.

## Delegar en un mapa

En Kotlin, puedes usar la palabra clave `by` para delegar a un mapa. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by mapOf("id" to 1, "name" to "John")
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es un mapa. Cuando acceda a la propiedad `nombre`, se buscará en el mapa la clave `nombre`. Si se encuentra la clave, se devolverá el valor correspondiente. Si no se encuentra la clave, se lanzará una excepción.

## Delegar a una propiedad

En Kotlin, puedes usar la palabra clave `by` para delegar a una propiedad. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by lazy {
        firstName + " " + lastName
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una propiedad. Cuando acceda a la propiedad `name`, se accederá y concatenará a las propiedades `firstName` y `lastName`. El resultado será devuelto.

## Delegar a una función

En Kotlin, puedes usar la palabra clave `by` para delegar a una función. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by lazy {
        computeName()
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una función. Cuando acceda a la propiedad `name`, se llamará a la función `computeName()`. El resultado será devuelto.

## Delegar a un objeto

En Kotlin, puedes usar la palabra clave `by` para delegar en un objeto. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by NameDelegate()
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es un objeto. Cuando acceda a la propiedad `name`, el objeto `NameDelegate` se utilizará para calcular el valor de la propiedad. El resultado será devuelto.

## Delegar a una clase

En Kotlin, puedes usar la palabra clave `by` para delegar a una clase. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by lazy {
        NameDelegate.computeName()
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una clase. Cuando acceda a la propiedad `name`, se llamará al método `NameDelegate.computeName()`. El resultado será devuelto.

## Delegar a una Superclase

En Kotlin, puedes usar la palabra clave `by` para delegar a una superclase. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User : SuperUser() {
    val name: String by lazy {
        super.name
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es la propiedad `name` de la superclase. Cuando acceda a la propiedad `nombre`, se accederá a la propiedad `nombre` de la superclase. El resultado será devuelto.

## Delegar a un objeto complementario

En Kotlin, puede usar la palabra clave `by` para delegar a un objeto complementario. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by lazy {
        User.name
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es la propiedad `name` del objeto complementario. Cuando acceda a la propiedad `name`, se accederá a la propiedad `name` del objeto complementario. El resultado será devuelto.

## Delegar a una interfaz

En Kotlin, puedes usar la palabra clave `by` para delegar a una interfaz. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by NameDelegate()
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una interfaz. Cuando acceda a la propiedad `name`, la interfaz `NameDelegate` se utilizará para calcular el valor de la propiedad. El resultado será devuelto.

## Delegar a una Clase Abstracta

En Kotlin, puedes usar la palabra clave `by` para delegar a una clase abstracta. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by lazy {
        NameDelegate.computeName()
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una clase abstracta. Cuando acceda a la propiedad `name`, se llamará al método `NameDelegate.computeName()`. El resultado será devuelto.

## Delegar a un Objeto Literal

En Kotlin, puedes usar la palabra clave `by` para delegar a un objeto literal. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by mapOf("id" to 1, "name" to "John")
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es un objeto literal. Cuando acceda a la propiedad `nombre`, se buscará en el mapa la clave `nombre`. Si se encuentra la clave, se devolverá el valor correspondiente. Si no se encuentra la clave, se lanzará una excepción.

## Delegar a una clase anidada

En Kotlin, puedes usar la palabra clave `by` para delegar a una clase anidada. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by lazy {
        NestedClass.name
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una clase anidada. Cuando acceda a la propiedad `name`, se accederá a la propiedad `NestedClass.name`. El resultado será devuelto.

## Delegar a una clase interna

En Kotlin, puedes usar la palabra clave `by` para delegar a una clase interna. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by lazy {
        InnerClass.name
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una clase interna. Cuando acceda a la propiedad `name`, se accederá a la propiedad `InnerClass.name`. El resultado será devuelto.

## Delegar a un objeto anónimo

En Kotlin, puedes usar la palabra clave `by` para delegar a un objeto anónimo. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by lazy {
        object: NameDelegate {
            override fun computeName(): String {
                // compute the name
            }
        }
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es un objeto anónimo. Cuando acceda a la propiedad `name`, se llamará al método `computeName()` del objeto anónimo. El resultado será devuelto.

## Delegar en una Lambda

En Kotlin, puede usar la palabra clave `by` para delegar a una lambda. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by lazy {
        // compute the name
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una lambda. Cuando acceda a la propiedad `name`, se llamará a la lambda. El resultado será devuelto.

## Delegar a una referencia de método

En Kotlin, puedes usar la palabra clave `by` para delegar a una referencia de método. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario. Podrías crear esta propiedad usando la palabra clave `by`:

```kotlin
class User {
    val name: String by lazy {
        User::name
    }
}
```

En este ejemplo, la propiedad `nombre` es una propiedad delegada. El delegado es una referencia de método. Cuando acceda a la propiedad `nombre`, se llamará al método `nombre` de la clase `Usuario`. El resultado será devuelto.

## Delegar a un Constructor

En Kotlin, puedes usar la palabra clave `by` para delegar a un constructor. Por ejemplo, suponga que tiene una clase que representa a un usuario. Es posible que desee crear una propiedad que almacene el nombre del usuario