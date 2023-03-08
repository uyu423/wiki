---
title: Kotlin y Spring Data: integración con una base de datos
description: 
published: true
date: 2023-02-07T00:55:23.444Z
tags: 
editor: markdown
dateCreated: 2023-02-07T00:55:17.811Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin and Spring Data: Integrating with a Database***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-spring-data-integrating-with-a-database)
{.links-list}


# Kotlin y Spring Data: integración con una base de datos

Kotlin es un lenguaje JVM que ha ganado popularidad en los últimos años por su sintaxis concisa e interoperabilidad con Java. Spring Data es una poderosa herramienta para trabajar con datos en aplicaciones Spring. En este artículo, veremos cómo usar Kotlin y Spring Data para trabajar con una base de datos.

Comenzaremos creando una clase de datos de Kotlin para representar una entidad de base de datos. Luego, crearemos una interfaz de Spring Data Repository para administrar nuestros datos. Implementaremos esta interfaz con un JpaRepository. Finalmente, usaremos nuestro Repositorio para consultar y actualizar nuestros datos.

## Crear una clase de datos

Comenzaremos creando una clase de datos de Kotlin para representar una entidad de base de datos. Llamaremos a nuestra clase `Usuario`. Nuestra clase `Usuario` tendrá tres propiedades: `id`, `nombre` y `correo electrónico`.


```kotlin
data class User(
        val id: Long,
        val name: String,
        val email: String
)
```

## Crear un repositorio

A continuación, crearemos una interfaz de Spring Data Repository para administrar nuestros datos. Llamaremos a nuestra interfaz `UserRepository`. Nuestro `UserRepository` extenderá `JpaRepository` y será parametrizado con nuestra clase de datos `User`.

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}
```

## Implementando el Repositorio

Implementaremos nuestra interfaz `UserRepository` con un `JpaRepository`. Inyectaremos nuestro `JpaRepository` en nuestra clase `Application` de Kotlin.

```kotlin
@SpringBootApplication
class Application {

    @Autowired
    lateinit var userRepository: UserRepository

    fun main(args: Array<String>) {
        SpringApplication.run(Application::class.java, *args)
    }
}
```

## Consultando el Repositorio

Ahora que tenemos nuestro `UserRepository`, podemos usarlo para consultar nuestra base de datos. Comenzaremos por encontrar todos los usuarios en nuestra base de datos.

```kotlin
val users = userRepository.findAll()
```

También podemos encontrar un usuario por su `id`.

```kotlin
val user = userRepository.findById(1L)
```

## Actualización de un usuario

Podemos usar nuestro `UserRepository` para actualizar un `Usuario` en nuestra base de datos. Comenzaremos por encontrar el usuario que queremos actualizar. Luego actualizaremos sus propiedades `name` y `email`. Finalmente, guardaremos nuestros cambios.

```kotlin
val user = userRepository.findById(1L)

user.name = "John Doe"
user.email = "john.doe@example.com"

userRepository.save(user)
```

## Eliminación de un usuario

Podemos usar nuestro `UserRepository` para eliminar un `Usuario` de nuestra base de datos. Comenzaremos por encontrar el usuario que queremos eliminar. Luego los eliminaremos de nuestra base de datos.

```kotlin
val user = userRepository.findById(1L)

userRepository.delete(user)
```

## Conclusión

En este artículo, hemos visto cómo usar Kotlin y Spring Data para trabajar con una base de datos. Hemos creado una clase de datos de Kotlin para representar una entidad de base de datos. También hemos creado una interfaz Spring Data Repository para administrar nuestros datos. Hemos implementado esta interfaz con un JpaRepository. Finalmente, hemos usado nuestro Repositorio para consultar y actualizar nuestros datos.