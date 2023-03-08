---
title: Kotlin y JSON: análisis y serialización de datos
description: 
published: true
date: 2023-02-01T18:04:45.538Z
tags: 
editor: markdown
dateCreated: 2023-02-01T18:04:43.861Z
---

> Este artículo se tradujo automáticamente con la **API de Google Cloud Translation**.
Algunas páginas pueden leerse mejor que el original.{.is-info}

- [Kotlin and JSON: Parsing and Serializing Data***Spanish** version of this document is available*](/es/Knowledge-base/Kotlin/kotlin-and-json-parsing-and-serializing-data)
{.links-list}


Kotlin y JSON: análisis y serialización de datos
============================================

Con la creciente popularidad de Kotlin, no sorprende que cada vez más desarrolladores busquen formas de trabajar con este lenguaje al analizar y serializar datos JSON.

En este artículo, veremos algunos de los métodos más populares para hacer esto.

Análisis de JSON con la biblioteca estándar de Kotlin
---------------------------------------------

La primera y más obvia forma de analizar JSON en Kotlin es usar la [clase JSON][1] integrada de la biblioteca estándar de Kotlin.

Esta clase proporciona una serie de métodos para leer y escribir datos JSON, así como para realizar tareas comunes, como convertir datos JSON hacia y desde objetos Kotlin.

Uno de los métodos más útiles en la clase JSON es el método `parse()`, que se puede usar para analizar una cadena JSON en un `JsonObject` de Kotlin:

```kotlin
val jsonString = """
    {
        "foo": "bar",
        "baz": 42
    }
    """

val jsonObject = JSON.parse(jsonString)
```

Una vez que tenga un `JsonObject`, puede usar varios métodos en esa clase para acceder a los datos que contiene. Por ejemplo, el método `get()` se puede usar para recuperar el valor de una clave específica:

```kotlin
val foo = jsonObject.get("foo") // "bar"
```

Si necesita analizar una matriz JSON, puede usar el método `parseArray()`, que devolverá una `JsonArray`. Esta clase proporciona métodos similares a la clase `JsonObject`, como `get()` y `size()`, que se pueden usar para recuperar datos de la matriz.

Analizando JSON con la biblioteca Gson
--------------------------------------------------

Otra forma popular de analizar JSON en Kotlin es usar la biblioteca [Gson][2].

Gson es una biblioteca de Java que se puede usar para convertir objetos de Java hacia y desde datos JSON. También tiene una excelente compatibilidad con Kotlin y se puede usar para analizar datos JSON en objetos de Kotlin.

Para usar Gson, primero debe agregarlo a su proyecto. Si está utilizando Gradle, puede agregar la siguiente dependencia a su archivo `build.gradle`:

```groovy
implementation 'com.google.code.gson:gson:2.8.5'
```

Una vez que se agrega Gson a su proyecto, puede crear una instancia `Gson` y usarla para analizar datos JSON:

```kotlin
val gson = Gson()

val jsonString = """
    {
        "foo": "bar",
        "baz": 42
    }
    """

val jsonObject = gson.fromJson(jsonString, JsonObject::class.java)
```

Como puedes ver, el método `fromJson()` toma una cadena JSON y una clase Kotlin como parámetros. La clase `JsonObject` es un contenedor de Kotlin alrededor de la clase estándar Java `JsonObject`.

Una vez que tenga un `JsonObject`, puede usar varios métodos en esa clase para acceder a los datos que contiene. Por ejemplo, el método `get()` se puede usar para recuperar el valor de una clave específica:

```kotlin
val foo = jsonObject.get("foo") // "bar"
```

Si necesita analizar una matriz JSON, puede usar el método `fromJson()` con una clase `JsonArray`. Esta clase proporciona métodos similares a la clase `JsonObject`, como `get()` y `size()`, que se pueden usar para recuperar datos de la matriz.

Analizando JSON con la biblioteca Jackson
---------------------------------------------

Otra forma popular de analizar JSON en Kotlin es usar la biblioteca [Jackson][3].

Jackson es una biblioteca de Java que se puede usar para convertir objetos de Java hacia y desde datos JSON. También tiene una excelente compatibilidad con Kotlin y se puede usar para analizar datos JSON en objetos de Kotlin.

Para usar Jackson, primero debe agregarlo a su proyecto. Si está utilizando Gradle, puede agregar la siguiente dependencia a su archivo `build.gradle`:

```groovy
implementation 'com.fasterxml.jackson.core:jackson-databind:2.9.8'
```

Una vez que Jackson se agrega a su proyecto, puede crear una instancia de `ObjectMapper` y usarla para analizar datos JSON:

```kotlin
val objectMapper = ObjectMapper()

val jsonString = """
    {
        "foo": "bar",
        "baz": 42
    }
    """

val jsonObject = objectMapper.readValue(jsonString, JsonNode::class.java)
```

Como puedes ver, el método `readValue()` toma una cadena JSON y una clase Kotlin como parámetros. La clase `JsonNode` es un contenedor de Kotlin alrededor de la clase estándar `JsonNode` de Java.

Una vez que tenga un `JsonNode`, puede usar varios métodos en esa clase para acceder a los datos que contiene. Por ejemplo, el método `get()` se puede usar para recuperar el valor de una clave específica:

```kotlin
val foo = jsonObject.get("foo") // "bar"
```

Si necesita analizar una matriz JSON, puede usar el método `readValue()` con una clase `JsonNode`. Esta clase proporciona métodos similares a la clase `JsonObject`, como `get()` y `size()`, que se pueden usar para recuperar datos de la matriz.

Serializar JSON con la biblioteca estándar de Kotlin
--------------------------------------------------

La biblioteca estándar de Kotlin también proporciona varios métodos para serializar datos JSON.

El método más utilizado es el método `stringify()`, que se puede usar para serializar un `JsonObject` en una cadena JSON:

```kotlin
val jsonObject = JsonObject(mapOf("foo" to "bar", "baz" to 42))

val jsonString = JSON.stringify(jsonObject)
```

Si necesita serializar una matriz JSON, puede usar el método `stringify()` con `JsonArray`.

Serializar JSON con la biblioteca Gson
---------------------------------------------

La biblioteca Gson también se puede usar para serializar datos JSON.

Para hacer esto, primero debe crear una instancia `Gson` y luego llamar al método `toJson()` en esa instancia, pasando el objeto que desea serializar:

```kotlin
val gson = Gson()

val jsonObject = JsonObject(mapOf("foo" to "bar", "baz" to 42))

val jsonString = gson.toJson(jsonObject)
```

Si necesita serializar una matriz JSON, puede usar el método `toJson()` con un `JsonArray`.

Serializar JSON con la biblioteca Jackson
---------------------------------------------------------

La biblioteca Jackson también se puede utilizar para serializar datos JSON.

Para hacer esto, primero debe crear una instancia de `ObjectMapper` y luego llamar al método `writeValueAsString()` en esa instancia, pasando el objeto que desea serializar:

```kotlin
val objectMapper = ObjectMapper()

val jsonObject = JsonObject(mapOf("foo" to "bar", "baz" to 42))

val jsonString = objectMapper.writeValueAsString(jsonObject)
```

Si necesita serializar una matriz JSON, puede usar el método `writeValueAsString()` con `JsonArray`.

Conclusión
----------

En este artículo, analizamos algunos de los métodos más populares para analizar y serializar datos JSON en Kotlin.

Hemos visto cómo usar la clase JSON integrada de la biblioteca estándar de Kotlin, así como también cómo usar las bibliotecas Gson y Jackson.

El método que elija dependerá en última instancia de sus propias preferencias personales.

[1]: https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.text/-json/
[2]: https://github.com/google/gson
[3]: https://github.com/FasterXML/jackson