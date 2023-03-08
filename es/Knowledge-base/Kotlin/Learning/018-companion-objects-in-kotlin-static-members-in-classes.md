---
title: 018: Objetos complementarios en Kotlin: miembros estáticos en clases
description: 
published: true
date: 2023-02-16T05:32:16.571Z
tags: 
editor: markdown
dateCreated: 2023-02-16T05:32:14.984Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [018: Companion Objects in Kotlin: Static Members in Classes***English** document is available*](/en/Knowledge-base/Kotlin/Learning/018-companion-objects-in-kotlin-static-members-in-classes)
{.links-list}


# Objetos complementarios en Kotlin: miembros estáticos en clases

Los objetos complementarios de Kotlin le permiten definir miembros estáticos en una clase. En esta publicación, veremos qué son los objetos complementarios y cómo usarlos.

## ¿Qué son los objetos complementarios?

 Los objetos complementarios son objetos que están asociados con una clase. Se utilizan para almacenar miembros estáticos en una clase.

Los miembros estáticos son miembros que están asociados con una clase, no con una instancia de una clase. Esto significa que puede acceder a ellos sin crear una instancia de la clase.

 Los objetos complementarios se declaran utilizando la palabra clave `objeto complementario`. Se pueden utilizar para almacenar constantes, funciones de utilidad y métodos de fábrica.

## Cómo usar objetos complementarios

Los objetos complementarios se declaran utilizando la palabra clave `objeto complementario`. Se pueden utilizar para almacenar constantes, funciones de utilidad y métodos de fábrica.

Para acceder a los miembros de un objeto complementario, utiliza el nombre de la clase como calificador. Por ejemplo, si tiene un objeto complementario llamado `MyClass` en un archivo llamado `MyClass.kt`, accedería a sus miembros de esta manera:

```kotlin
MyClass.Companion.myFunction()
```

Si desea acceder a los miembros de un objeto complementario desde dentro de la clase, puede omitir la palabra clave `compañero`. Por ejemplo:

```kotlin
class MyClass {
    companion object {
        fun myFunction() {
            // ...
        }
    }
}
```

## Conclusión

En esta publicación, hemos visto qué son los objetos complementarios y cómo usarlos. Los objetos complementarios son una excelente manera de almacenar miembros estáticos en una clase.