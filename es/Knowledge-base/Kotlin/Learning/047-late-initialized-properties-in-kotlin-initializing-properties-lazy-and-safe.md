---
title: 047: Propiedades de inicialización tardía en Kotlin: inicialización de propiedades perezosas y seguras
description: 
published: true
date: 2023-02-16T14:32:27.359Z
tags: 
editor: markdown
dateCreated: 2023-02-16T14:32:19.417Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [047: Late-initialized Properties in Kotlin: Initializing Properties Lazy and Safe***English** document is available*](/en/Knowledge-base/Kotlin/Learning/047-late-initialized-properties-in-kotlin-initializing-properties-lazy-and-safe)
{.links-list}


# Propiedades inicializadas tardíamente en Kotlin: inicialización de propiedades perezosas y seguras

Las propiedades de inicialización tardía de Kotlin son una excelente manera de inicializar propiedades de forma perezosa y segura. En esta publicación, veremos cómo usar las propiedades iniciadas tardíamente para nuestro beneficio.

## ¿Qué son las propiedades con inicialización tardía?

Las propiedades de inicialización tardía son propiedades que no se inicializan durante la construcción del objeto. En cambio, se inicializan durante el primer acceso a la propiedad. Esto es útil para propiedades que son costosas de inicializar o que no se usan con frecuencia.

## Cómo usar propiedades iniciadas tarde

Para usar una propiedad inicializada tarde, primero debemos declararla con la palabra clave ```lateinit```:

```kotlin
lateinit var property: Type
```

Luego podemos inicializar la propiedad cuando accedemos a ella por primera vez:

```kotlin
property = value
```

## Ventajas de las propiedades con inicialización tardía

Hay dos ventajas principales en el uso de propiedades con inicialización tardía: rendimiento y seguridad.

### Actuación

Las propiedades con inicialización tardía pueden mejorar el rendimiento porque no se inicializan hasta que se accede a ellas por primera vez. Esto significa que podemos evitar inicializar propiedades que no se usan con frecuencia.

### Seguridad

Las propiedades inicializadas tardíamente también son seguras de usar. Esto se debe a que no se inicializan hasta que se accede a ellos por primera vez. Esto significa que podemos evitar el uso de propiedades que aún no se han inicializado.

## Desventajas de las propiedades iniciadas tarde

Hay dos desventajas principales en el uso de propiedades con inicialización tardía: legibilidad y depuración.

### Legibilidad

Las propiedades inicializadas tardíamente pueden ser más difíciles de leer porque no se inicializan hasta que se accede a ellas por primera vez. Esto significa que debemos tener cuidado de inicializar las propiedades antes de usarlas.

### Depuración

Las propiedades inicializadas tardíamente también pueden ser más difíciles de depurar porque no se inicializan hasta que se accede a ellas por primera vez. Esto significa que debemos tener cuidado de inicializar las propiedades antes de usarlas.