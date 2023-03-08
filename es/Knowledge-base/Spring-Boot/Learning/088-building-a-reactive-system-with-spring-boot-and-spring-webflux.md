---
title: 088: Creación de un sistema reactivo con Spring Boot y Spring WebFlux
description: 
published: true
date: 2023-02-05T18:32:33.224Z
tags: 
editor: markdown
dateCreated: 2023-02-05T18:32:31.613Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [088: Building a Reactive System with Spring Boot and Spring WebFlux***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/088-building-a-reactive-system-with-spring-boot-and-spring-webflux)
{.links-list}


# 088: Construyendo un Sistema Reactivo con Spring Boot y Spring WebFlux

En esta publicación, aprenderemos cómo construir un sistema reactivo usando Spring Boot y Spring WebFlux.

Los sistemas reactivos son aquellos que se construyen utilizando los principios del manifiesto reactivo. Estos sistemas son receptivos, resilientes, elásticos y basados en mensajes.

En un sistema reactivo, cada componente es un productor de mensajes y un consumidor de mensajes. Los componentes se comunican entre sí de forma asincrónica mediante mensajes.

Los sistemas controlados por mensajes son más escalables y resistentes que los sistemas tradicionales porque pueden manejar fallas sin afectar el resto del sistema.

Spring Boot es un marco que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

Spring WebFlux es un marco web reactivo para crear aplicaciones web utilizando el modelo de programación reactiva.

En esta publicación, aprenderemos cómo construir un sistema reactivo simple usando Spring Boot y Spring WebFlux.

## Creación de un proyecto Spring Boot

Podemos usar Spring Initializr para crear un proyecto Spring Boot. Tendremos que seleccionar las siguientes dependencias:

- Internet
- Red reactiva
- Lombok

Lombok es una biblioteca que se puede usar para reducir el código repetitivo en nuestra aplicación.

## Escribir el código

Comenzaremos creando un controlador simple que devuelva una lista de cadenas.

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public List<String> hello() {
        return Arrays.asList("Hello", "World");
    }
}
```

En el controlador, hemos anotado el método `hello()` con la anotación `@GetMapping`. Esta anotación asigna el método `hello()` a la ruta `/hello`.

También hemos anotado la clase `HelloController` con la anotación `@RestController`. Esta anotación marca la clase como un controlador y permite que Spring maneje las solicitudes web.

La anotación `@RestController` es una anotación conveniente que equivale a anotar una clase con las anotaciones `@Controller` y `@ResponseBody`.

La anotación `@ResponseBody` le dice a Spring que serialice el valor de retorno del método `hello()` como JSON y lo envíe en el cuerpo de la respuesta.

Cuando ejecutamos la aplicación y hacemos una solicitud a la ruta `/hello`, deberíamos ver la siguiente respuesta JSON:

```json
["Hello","World"]
```

## Hacer reactivo el método `hello()`

Podemos hacer que el método `hello()` sea reactivo devolviendo `Mono<List<String>>` en lugar de `List<String>`.

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public Mono<List<String>> hello() {
        return Mono.just(Arrays.asList("Hello", "World"));
    }
}
```

La clase `Mono` representa un flujo de 0 o 1 elemento. En este caso, lo estamos usando para envolver nuestra lista de cadenas.

El método `just()` crea un `Mono` que contiene el elemento especificado.

Cuando hacemos una solicitud a la ruta `/hello`, deberíamos ver la misma respuesta JSON que antes.

## Hacer que el método `hello()` sea asíncrono

Podemos hacer que el método `hello()` sea asíncrono usando el operador `publishOn()`.

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public Mono<List<String>> hello() {
        return Mono.just(Arrays.asList("Hello", "World"))
                .publishOn(Schedulers.elastic());
    }
}
```

El operador `publishOn()` le dice a Spring que publique los elementos de la transmisión en el programador especificado. En este caso, estamos usando el programador `elástico`, que es un programador asíncrono.

Cuando hacemos una solicitud a la ruta `/hello`, deberíamos ver la misma respuesta JSON que antes.

## Hacer que el método `hello()` no bloquee

Podemos hacer que el método `hello()` no bloquee usando el operador `subscribeOn()`.

```java
@RestController
public class HelloController {

    @GetMapping("/hello")
    public Mono<List<String>> hello() {
        return Mono.just(Arrays.asList("Hello", "World"))
                .subscribeOn(Schedulers.elastic());
    }
}
```

El operador `subscribeOn()` le dice a Spring que se suscriba a la transmisión en el Programador especificado. En este caso, estamos usando el Programador `elástico`, que es un Programador asíncrono.

Cuando hacemos una solicitud a la ruta `/hello`, deberíamos ver la misma respuesta JSON que antes.

## Conclusión

En esta publicación, hemos aprendido cómo construir un sistema reactivo usando Spring Boot y Spring WebFlux. También hemos aprendido cómo hacer que el método `hello()` sea reactivo, asincrónico y sin bloqueo.