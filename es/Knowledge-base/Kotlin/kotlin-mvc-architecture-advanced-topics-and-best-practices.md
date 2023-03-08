---
title: Arquitectura Kotlin MVC: temas avanzados y mejores prácticas
description: 
published: true
date: 2023-02-08T05:18:11.922Z
tags: 
editor: markdown
dateCreated: 2023-02-08T05:18:10.564Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin MVC Architecture: Advanced Topics and Best Practices***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-mvc-architecture-advanced-topics-and-best-practices)
{.links-list}


# Arquitectura Kotlin MVC: temas avanzados y mejores prácticas

En este artículo, analizaremos algunos temas avanzados y mejores prácticas para la arquitectura Kotlin MVC. También proporcionaremos algunos ejemplos de código para ilustrar estos conceptos.

## Manejo de solicitudes

Uno de los aspectos más importantes de la arquitectura Kotlin MVC es cómo manejar correctamente las solicitudes. Hay dos formas de hacer esto: a través de filtros y controladores.

### Filtros

Los filtros se utilizan para preprocesar las solicitudes antes de que las gestionen los controladores. Esto es útil para tareas como autenticación y autorización, validación de entrada y registro.

Los filtros se registran en el archivo de ```configuración``` de la aplicación:

```kotlin
// Register a filter for all requests
configuration.addFilter("MyFilter", "/*") {
    // ...
}

// Register a filter for specific requests
configuration.addFilter("MyFilter", "/my-path") {
    // ...
}
```

Una vez que se registra un filtro, se invocará para todas las solicitudes coincidentes. El filtro tiene acceso a los ```Parámetros```, ```Encabezados``` y ```Cuerpo```. También puede establecer ```Encabezados``` y ```Atributos``` en la solicitud, que estarán disponibles para los controladores.

#### Ejemplo de filtro

Aquí hay un ejemplo simple de un filtro que registra todas las solicitudes:

```kotlin
class RequestLoggingFilter : Filter {
    override fun invoke(call: Call, next: Next) {
        val request = call.request
        val path = request.path
        val method = request.method
        val query = request.queryString
        val headers = request.headers.entries.joinToString { "${it.key}: ${it.value}" }
        val body = request.body.asText()
        
        val log = "$method $path $query $headers $body"
        println(log)
        
        // Invoke the next filter or handler in the chain
        next(call)
    }
}
```

Este filtro registra el método de solicitud, la ruta, la cadena de consulta, los encabezados y el cuerpo en la consola.

### Controladores

Los controladores se utilizan para procesar solicitudes y generar respuestas. Tienen acceso a los ```Parámetros```, ```Encabezados```, ```Atributos``` y ```Cuerpo```.

Los handlers se registran en el archivo ```configuration``` de la aplicación:

```kotlin
// Register a handler for all requests
configuration.addHandler("MyHandler", "/*") {
    // ...
}

// Register a handler for specific requests
configuration.addHandler("MyHandler", "/my-path") {
    // ...
}
```

Una vez que se registra un controlador, se invocará para todas las solicitudes coincidentes. El controlador puede establecer ```Encabezados``` y ```Atributos``` en la respuesta, que estarán disponibles para filtros y otros controladores.

#### Ejemplo de controlador

Aquí hay un ejemplo simple de un controlador que devuelve un "¡Hola, mundo!" respuesta:

```kotlin
class HelloWorldHandler : Handler {
    override fun invoke(call: Call) {
        val response = call.response
        response.status = Status.OK
        response.body = "Hello, World!"
    }
}
```

Este controlador establece el estado de la respuesta en ```200 OK``` y el cuerpo en "¡Hola, mundo!".

## Enrutamiento

El enrutamiento se utiliza para asignar solicitudes a controladores. Hay dos formas de hacer esto: a través de la configuración y el código.

### Configuración

El enrutamiento se puede configurar en el archivo ```configuration``` de la aplicación:

```kotlin
configuration.addRoute("MyRoute", "/my-path") {
    // ...
}
```

Una vez que se registra una ruta, se invocará para todas las solicitudes coincidentes. La ruta tiene acceso a los ```Parámetros```, ```Encabezados``` y ```Cuerpo```. También puede establecer ```Encabezados``` y ```Atributos``` en la solicitud, que estarán disponibles para filtros y controladores.

#### Ejemplo de ruta

Aquí hay un ejemplo simple de una ruta que asigna solicitudes a "¡Hola, mundo!" manipulador:

```kotlin
class HelloWorldRoute : Route {
    override fun invoke(call: Call, next: Next) {
        val request = call.request
        val path = request.path
        
        if (path == "/hello-world") {
            val handler = HelloWorldHandler()
            handler(call)
        } else {
            // Invoke the next route in the chain
            next(call)
        }
    }
}
```

Esta ruta comprueba la ruta de la solicitud. Si es "/hello-world", invoca el "¡Hola, mundo!" manipulador. De lo contrario, invoca la siguiente ruta de la cadena.

### Código

El enrutamiento también se puede hacer en código:

```kotlin
val route = Route {
    // ...
}

configuration.addRoute(route)
```

Una vez que se registra una ruta, se invocará para todas las solicitudes coincidentes. La ruta tiene acceso a los ```Parámetros```, ```Encabezados``` y ```Cuerpo```. También puede establecer ```Encabezados``` y ```Atributos``` en la solicitud, que estarán disponibles para filtros y controladores.

#### Ejemplo de ruta

Aquí hay un ejemplo simple de una ruta que asigna solicitudes a "¡Hola, mundo!" manipulador:

```kotlin
val route = Route {
    val request = it.request
    val path = request.path
    
    if (path == "/hello-world") {
        val handler = HelloWorldHandler()
        handler(it)
    } else {
        // Invoke the next route in the chain
        it.next()
    }
}
```

Esta ruta comprueba la ruta de la solicitud. Si es "/hello-world", invoca el "¡Hola, mundo!" manipulador. De lo contrario, invoca la siguiente ruta de la cadena.

## Mejores prácticas

Estas son algunas de las mejores prácticas generales que se deben tener en cuenta al trabajar con la arquitectura Kotlin MVC:

- Use filtros para tareas de preprocesamiento como autenticación, autorización, validación de entrada y registro.
- Utilizar controladores para procesar solicitudes y generar respuestas.
- Utilice rutas para asignar solicitudes a controladores.
- Mantenga su código limpio y conciso.
- Seguir el Principio de Responsabilidad Única.
- Siga el principio SECO.
- Seguir el principio KISS.

## Referencias

- [Arquitectura Kotlin MVC](https://kotlinlang.org/docs/reference/mvc.html)
- [Marco Kotlin MVC] (https://kotlinlang.org/docs/reference/mvc-framework.html)
- [Tutorial de Kotlin MVC](https://kotlinlang.org/docs/tutorials/kotlin-mvc.html)