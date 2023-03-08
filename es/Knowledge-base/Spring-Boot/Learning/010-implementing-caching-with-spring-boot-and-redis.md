---
title: 010: Implementación de almacenamiento en caché con Spring Boot y Redis
description: 
published: true
date: 2023-02-03T08:43:41.420Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:43:36.494Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [010: Implementing caching with Spring Boot and Redis***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/010-implementing-caching-with-spring-boot-and-redis)
{.links-list}


# Implementando el almacenamiento en caché con Spring Boot y Redis

En esta publicación, cubriremos cómo implementar el almacenamiento en caché con Spring Boot y Redis. Comenzaremos con una breve descripción general del almacenamiento en caché y por qué es útil. Luego veremos cómo configurar Spring Boot para usar Redis para el almacenamiento en caché. Finalmente, escribiremos una aplicación Spring Boot simple para demostrar cómo usar Redis para el almacenamiento en caché.

## ¿Qué es el almacenamiento en caché?

El almacenamiento en caché es una técnica para almacenar datos en una ubicación de memoria temporal para acelerar el acceso posterior a esos datos. Cuando los datos se almacenan en caché, las solicitudes futuras de esos datos se pueden atender mucho más rápido ya que los datos ya están en la memoria.

Hay dos tipos principales de almacenamiento en caché: almacenamiento en caché de aplicaciones y almacenamiento en caché de bases de datos. El almacenamiento en caché de aplicaciones se usa para almacenar datos en la memoria de la aplicación, mientras que el almacenamiento en caché de la base de datos se usa para almacenar datos en la memoria de la base de datos.

## ¿Por qué usar el almacenamiento en caché?

El almacenamiento en caché se puede utilizar para mejorar el rendimiento de una aplicación al reducir la cantidad de veces que se leen datos de un medio de almacenamiento lento, como una base de datos. El almacenamiento en caché también se puede utilizar para reducir la cantidad de datos que deben leerse desde un medio de almacenamiento lento almacenando una copia de los datos en un medio de almacenamiento más rápido, como la memoria.

## Configuración de Spring Boot para usar Redis para el almacenamiento en caché

Spring Boot proporciona soporte integrado para Redis, lo que facilita la configuración de Redis para el almacenamiento en caché. Para configurar Spring Boot para usar Redis para el almacenamiento en caché, debe agregar la siguiente dependencia a su proyecto:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

También debe configurar el host y el puerto del servidor Redis en el archivo application.properties:

```properties
spring.redis.host=localhost
spring.redis.port=6379
```

## Escribir una aplicación Spring Boot para usar Redis para el almacenamiento en caché

Ahora que hemos configurado Spring Boot para usar Redis para el almacenamiento en caché, escribamos una aplicación Spring Boot simple para demostrar cómo usar Redis para el almacenamiento en caché.

Comenzaremos creando un modelo de datos simple para representar a un usuario:

```java
public class User {

    private Long id;
    private String name;
    private Integer age;

    // getters and setters
}
```

A continuación, crearemos una aplicación Spring Boot simple con un solo controlador REST para administrar usuarios:

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUser(@PathVariable Long id) {
        // code to get user from database
    }

    @PostMapping
    public User createUser(@RequestBody User user) {
        // code to create user in database
    }

    @PutMapping("/{id}")
    public User updateUser(@PathVariable Long id, @RequestBody User user) {
        // code to update user in database
    }

    @DeleteMapping("/{id}")
    public void deleteUser(@PathVariable Long id) {
        // code to delete user from database
    }
}
```

Ahora podemos usar este controlador para administrar usuarios en nuestra base de datos. Sin embargo, cada vez que llamamos al método getUser(), se ejecutará una consulta a la base de datos para obtener al usuario de la base de datos. Esto puede ser lento, especialmente si la base de datos es grande.

Podemos mejorar el rendimiento de nuestra aplicación almacenando en caché los resultados del método getUser() usando Redis. Para hacer esto, agregaremos la anotación @Cacheable al método getUser():

```java
@Cacheable("users")
@GetMapping("/{id}")
public User getUser(@PathVariable Long id) {
    // code to get user from database
}
```

Esta anotación le dice a Spring que almacene en caché los resultados del método getUser() en un caché de Redis llamado "usuarios". La próxima vez que se llame al método getUser() con la misma identificación, se devolverá el resultado almacenado en caché en lugar de ejecutar una consulta de base de datos.

También podemos usar la anotación @CacheEvict para eliminar una entrada almacenada en caché:

```java
@CacheEvict("users")
@DeleteMapping("/{id}")
public void deleteUser(@PathVariable Long id) {
    // code to delete user from database
}
```

Esta anotación le dice a Spring que elimine la entrada en caché para el usuario con la identificación dada cuando se llama al método deleteUser().

## Conclusión

En esta publicación, cubrimos cómo implementar el almacenamiento en caché con Spring Boot y Redis. Hemos visto cómo configurar Spring Boot para usar Redis para el almacenamiento en caché y hemos escrito una aplicación Spring Boot simple para demostrar cómo usar Redis para el almacenamiento en caché.