---
title: 043: Clases internas y anidadas en Kotlin: creación de clases dentro de clases
description: 
published: true
date: 2023-02-16T13:32:30.921Z
tags: 
editor: markdown
dateCreated: 2023-02-16T13:32:29.314Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [043: Nested and Inner Classes in Kotlin: Creating Classes within Classes***English** document is available*](/en/Knowledge-base/Kotlin/Learning/043-nested-and-inner-classes-in-kotlin-creating-classes-within-classes)
{.links-list}


# 043: Clases Internas y Anidadas en Kotlin: Creando Clases dentro de Clases

Kotlin admite dos tipos de clases que se pueden crear dentro de otra clase: clases anidadas y clases internas. En esta publicación, veremos las diferencias entre las clases anidadas e internas en Kotlin y cómo crear cada tipo de clase.

## Clases anidadas

Una clase anidada es una clase que se define dentro de otra clase. Las clases anidadas no son miembros de la clase en la que están definidas. Son simplemente clases que se definen dentro de otra clase.

Aquí hay un ejemplo de una clase anidada en Kotlin:

```kotlin
class OuterClass {
    class NestedClass {
        // ...
    }
}
```

En el ejemplo anterior, `NestedClass` no es miembro de `OuterClass`. Es simplemente una clase que se define dentro de `OuterClass`.

Las clases anidadas se pueden usar para agrupar clases relacionadas. Por ejemplo, si tiene una clase que representa un automóvil, puede crear una clase anidada que represente el motor del automóvil.

Las clases anidadas también se pueden usar para crear miembros estáticos de una clase. En el siguiente ejemplo, `NestedClass` tiene un miembro estático llamado `foo`:

```kotlin
class OuterClass {
    class NestedClass {
        companion object {
            val foo = "bar"
        }
    }
}
```

En el ejemplo anterior, `NestedClass` tiene un miembro estático llamado `foo`. Esto significa que se puede acceder a `NestedClass` sin una instancia de `OuterClass`.

## Clases internas

Una clase interna es una clase que se define dentro de otra clase y es miembro de esa clase. Las clases internas tienen acceso a los miembros de la clase en la que están definidas.

Aquí hay un ejemplo de una clase interna en Kotlin:

```kotlin
class OuterClass {
    inner class InnerClass {
        // ...
    }
}
```

En el ejemplo anterior, `InnerClass` es miembro de `OuterClass`. Esto significa que `InnerClass` tiene acceso a los miembros de `OuterClass`.

Las clases internas se pueden usar para crear objetos que están asociados con una instancia particular de una clase. Por ejemplo, si tiene una clase que representa un automóvil, puede crear una clase interna que represente el motor del automóvil.

Las clases internas también se pueden usar para crear clases anónimas. Una clase anónima es una clase que se define sin nombre. Las clases anónimas son útiles para crear objetos que no están asociados con ninguna instancia particular de una clase.

Aquí hay un ejemplo de una clase interna anónima en Kotlin:

```kotlin
class OuterClass {
    val anonymousInnerClass = object: SomeType {
        // ...
    }
}
```

En el ejemplo anterior, se crea una clase interna anónima que implementa la interfaz `SomeType`.

## Conclusión

En esta publicación, echamos un vistazo a las diferencias entre las clases anidadas y las internas en Kotlin. También hemos visto cómo crear cada tipo de clase.