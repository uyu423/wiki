---
title: Kotlin y Spring Data: conexión a una base de datos
description: 
published: true
date: 2023-02-08T09:17:31.298Z
tags: 
editor: markdown
dateCreated: 2023-02-08T09:17:29.682Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin and Spring Data: Connecting to a Database***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-spring-data-connecting-to-a-database)
{.links-list}


# Kotlin y Spring Data: conexión a una base de datos

Kotlin es un lenguaje de programación de tipo estático que se ejecuta en la máquina virtual de Java y también se puede compilar en el código fuente de JavaScript. Kotlin es desarrollado por JetBrains.

Spring Data es un proyecto que facilita el trabajo con tecnologías de acceso a datos, como bases de datos relacionales, en Spring Framework.

En este artículo, veremos cómo usar Kotlin y Spring Data para conectarnos a una base de datos.

## Configuración del proyecto

Primero, necesitaremos crear un nuevo proyecto de Kotlin usando Spring Initializr. Tendremos que seleccionar las siguientes dependencias:

- Internet
- Spring Data JPA
- Base de datos H2

![inicialización de primavera](https://i.imgur.com/G9dLNcJ.png)

Una vez generado el proyecto, podemos importarlo a nuestro IDE favorito. Usaré IntelliJ IDEA.

## Configuración de la fuente de datos

A continuación, necesitaremos configurar el DataSource. Podemos hacer esto agregando lo siguiente al archivo `application.properties`:

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

spring.jpa.generate-ddl=true
spring.jpa.hibernate.ddl-auto=create-drop
```

La propiedad `spring.datasource.url` define la URL de la base de datos. La propiedad `spring.datasource.driverClassName` define el nombre de la clase del controlador. La propiedad `spring.datasource.username` define el nombre de usuario. La propiedad `spring.datasource.password` define la contraseña.

La propiedad `spring.jpa.generate-ddl` le dice a Spring Data que genere el esquema de la base de datos. La propiedad `spring.jpa.hibernate.ddl-auto` le dice a Hibernate que cree y elimine el esquema de la base de datos.

## Creando la Entidad

A continuación, necesitaremos crear una entidad. Una entidad es una clase que representa una tabla en la base de datos. Podemos crear una entidad anotando una clase con la anotación `@Entity`.

```kotlin
@Entity
class User(
        @Id @GeneratedValue val id: Long,
        val name: String,
        val age: Int
)
```

La anotación `@Entity` indica que se trata de una entidad. La anotación `@Id` indica que la propiedad `id` es la clave principal. La anotación `@GeneratedValue` indica que la base de datos debe generar la propiedad `id`.

Las propiedades `name` y `age` se asignarán a las columnas de la base de datos.

## Creando el Repositorio

A continuación, necesitaremos crear un repositorio. Un repositorio es una clase que proporciona acceso a los datos de la base de datos. Podemos crear un repositorio anotando una clase con la anotación `@Repository`.

```kotlin
@Repository
interface UserRepository : CrudRepository<User, Long>
```

La anotación `@Repository` indica que se trata de un repositorio. La interfaz `CrudRepository` proporciona métodos para operaciones CRUD.

## Creando el Servicio

A continuación, necesitaremos crear un servicio. Un servicio es una clase que contiene lógica empresarial. Podemos crear un servicio anotando una clase con la anotación `@Service`.

```kotlin
@Service
class UserService(
        private val userRepository: UserRepository
) {
    fun createUser(user: User): User {
        return userRepository.save(user)
    }

    fun getUserById(id: Long): User? {
        return userRepository.findById(id).orElse(null)
    }

    fun getAllUsers(): List<User> {
        return userRepository.findAll().toList()
    }

    fun updateUser(user: User): User {
        return userRepository.save(user)
    }

    fun deleteUserById(id: Long) {
        userRepository.deleteById(id)
    }
}
```

La anotación `@Service` indica que se trata de un servicio. El método `createUser` crea un nuevo usuario. El método `getUserById` obtiene un usuario por id. El método `getAllUsers` obtiene todos los usuarios. El método `updateUser` actualiza un usuario. El método `deleteUserById` elimina un usuario por id.

## Creando el controlador

Finalmente, necesitaremos crear un controlador. Un controlador es una clase que contiene métodos que manejan solicitudes HTTP. Podemos crear un controlador anotando una clase con la anotación `@RestController`.

```kotlin
@RestController
@RequestMapping("/users")
class UserController(
        private val userService: UserService
) {
    @PostMapping
    fun createUser(@RequestBody user: User): User {
        return userService.createUser(user)
    }

    @GetMapping("/{id}")
    fun getUserById(@PathVariable id: Long): User? {
        return userService.getUserById(id)
    }

    @GetMapping
    fun getAllUsers(): List<User> {
        return userService.getAllUsers()
    }

    @PutMapping
    fun updateUser(@RequestBody user: User): User {
        return userService.updateUser(user)
    }

    @DeleteMapping("/{id}")
    fun deleteUserById(@PathVariable id: Long) {
        userService.deleteUserById(id)
    }
}
```

La anotación `@RestController` indica que se trata de un controlador. La anotación `@RequestMapping` asigna solicitudes HTTP a métodos en el controlador. La anotación `@PostMapping` asigna solicitudes HTTP POST al método `createUser`. La anotación `@GetMapping` mapea las solicitudes HTTP GET al método `getUserById`. La anotación `@PutMapping` mapea las solicitudes HTTP PUT al método `updateUser`. La anotación `@DeleteMapping` mapea las solicitudes HTTP DELETE al método `deleteUserById`.

## Prueba de los puntos finales

Podemos probar los puntos finales usando curl o Postman.

```
$ curl -X POST localhost:8080/users -d '{"name": "John Doe", "age": 42}' -H "Content-Type: application/json"
{"id":1,"name":"John Doe","age":42}

$ curl localhost:8080/users/1
{"id":1,"name":"John Doe","age":42}

$ curl localhost:8080/users
[{"id":1,"name":"John Doe","age":42}]

$ curl -X PUT localhost:8080/users -d '{"id": 1, "name": "Jane Doe", "age": 43}' -H "Content-Type: application/json"
{"id":1,"name":"Jane Doe","age":43}

$ curl -X DELETE localhost:8080/users/1
```

## Conclusión

En este artículo, hemos visto cómo usar Kotlin y Spring Data para conectarse a una base de datos.