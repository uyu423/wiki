---
title: Creación de una aplicación CRUD con Spring Boot
description: 
published: true
date: 2023-02-06T08:33:26.065Z
tags: 
editor: markdown
dateCreated: 2023-02-06T08:33:24.337Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Building a CRUD Application with Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/building-a-crud-application-with-spring-boot)
{.links-list}


# Creación de una aplicación CRUD con Spring Boot

Desarrollar una aplicación CRUD (Crear, Leer, Actualizar, Eliminar) es un requisito común al crear aplicaciones web. Spring Boot facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción que puede "simplemente ejecutar". En este artículo, nos centraremos en cómo crear una aplicación CRUD con Spring Boot.

## ¿Qué es Spring Boot?

Spring Boot es un marco basado en Java que se utiliza para crear aplicaciones basadas en Spring independientes y de grado de producción. Se necesita una visión obstinada de la plataforma Spring y las bibliotecas de terceros, para que pueda comenzar con un mínimo de complicaciones. La mayoría de las aplicaciones de Spring Boot necesitan muy poca configuración de Spring.

## ¿Por qué usar Spring Boot?

SpringBoot proporciona una serie de funciones que facilitan el desarrollo de una aplicación web.

- Puede incrustar Tomcat, Jetty o Undertow directamente (no es necesario implementar archivos WAR)
- Utiliza un enfoque obstinado para la configuración.
- Reduce el código repetitivo
- Proporciona funciones listas para producción, como métricas, controles de estado y configuración externalizada

## Empezando

En esta sección, le mostraremos cómo crear una aplicación CRUD simple con Spring Boot.

### Requisitos previos

Para seguir este artículo, necesitará lo siguiente:

- Java 8 o superior
- Spring Boot 2.0 o superior
- Un IDE de su elección
- Maven 3.0 o superior

### Crear el proyecto

Primero, cree un proyecto Maven en su IDE. Asegúrese de seleccionar el proyecto inicial "Spring Boot" y el módulo "web".

![Crear proyecto Spring Boot](https://i.imgur.com/5BkRJN4.png)

### Agregar dependencias

A continuación, debemos agregar algunas dependencias a nuestro archivo `pom.xml`.

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <scope>runtime</scope>
    </dependency>
</dependencies>
```

La dependencia `spring-boot-starter-data-jpa` agregará Spring Data e Hibernate a nuestro proyecto. La dependencia `spring-boot-starter-web` agregará Spring MVC y Tomcat. Finalmente, la dependencia `postgresql` agregará el controlador PostgreSQL.

### Configurar la base de datos

A continuación, necesitamos configurar nuestra base de datos. En este ejemplo, usaremos PostgreSQL, pero puede usar cualquier base de datos que desee.

Primero, cree un archivo llamado `application.properties` en el directorio `src/main/resources` y agregue las siguientes líneas:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=postgres
spring.datasource.password=postgres
spring.jpa.show-sql=true
```

Esto configurará nuestra aplicación para conectarse a una base de datos PostgreSQL que se ejecuta en localhost en el puerto 5432. El nombre de usuario y la contraseña son ambos `postgres`.

### Crear la entidad

Ahora, necesitamos crear una clase de entidad. Una entidad es una clase de Java que representa una tabla de base de datos. En este ejemplo, crearemos una entidad `Usuario`.

```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;
    // ... getters and setters
}
```

La anotación `@Entity` le dice a Hibernate que esta clase es una entidad. La anotación `@Id` le dice a Hibernate que el campo `id` es la clave principal. La anotación `@GeneratedValue` le dice a Hibernate que genere un valor único para la clave principal.

### Crear el repositorio

A continuación, necesitamos crear una interfaz de repositorio. Un repositorio es una interfaz de Java que proporciona métodos para almacenar y recuperar datos. En este ejemplo, crearemos una interfaz `UserRepository`.

```java
public interface UserRepository extends CrudRepository<User, Long> {
}
```

La interfaz `CrudRepository` proporciona métodos para operaciones CRUD. Usaremos esta interfaz para implementar nuestro `UserRepository`.

### Crear el servicio

Ahora, necesitamos crear una clase de servicio. Un servicio es una clase de Java que contiene lógica empresarial. En este ejemplo, crearemos una clase `UserService`.

```java
@Service
public class UserService {
    private final UserRepository userRepository;
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
    public User createUser(User user) {
        return userRepository.save(user);
    }
    public User getUserById(Long id) {
        return userRepository.findById(id).orElseThrow(() -> new RuntimeException("User not found"));
    }
    public List<User> getAllUsers() {
        return userRepository.findAll();
    }
    public User updateUser(User user) {
        return userRepository.save(user);
    }
    public void deleteUserById(Long id) {
        userRepository.deleteById(id);
    }
}
```

La anotación `@Service` le dice a Spring que se trata de un bean de servicio. La clase `UserService` contiene métodos para crear, recuperar, actualizar y eliminar usuarios.

### Crear el controlador

A continuación, necesitamos crear una clase de controlador. Un controlador es una clase de Java que contiene métodos para manejar solicitudes HTTP. En este ejemplo, crearemos una clase `UserController`.

```java
@RestController
@RequestMapping("/users")
public class UserController {
    private final UserService userService;
    public UserController(UserService userService) {
        this.userService = userService;
    }
    @PostMapping
    public User createUser(@RequestBody User user) {
        return userService.createUser(user);
    }
    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        return userService.getUserById(id);
    }
    @GetMapping
    public List<User> getAllUsers() {
        return userService.getAllUsers();
    }
    @PutMapping
    public User updateUser(@RequestBody User user) {
        return userService.updateUser(user);
    }
    @DeleteMapping("/{id}")
    public void deleteUserById(@PathVariable Long id) {
        userService.deleteUserById(id);
    }
}
```

La anotación `@RestController` le dice a Spring que este es un bean controlador. La anotación `@RequestMapping` asigna solicitudes HTTP a métodos de controlador. La clase `UserController` contiene métodos para crear, recuperar, actualizar y eliminar usuarios.

### Ejecutar la aplicación

Ahora que tenemos nuestra aplicación configurada, podemos ejecutarla. Para ejecutar la aplicación, simplemente ejecute el método `principal` en la clase `Aplicación`.

```java
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

La aplicación se iniciará en el puerto 8080.

## Prueba de la aplicación

Ahora que nuestra aplicación está funcionando, vamos a probarla. Podemos usar `curl` para enviar solicitudes HTTP a nuestra aplicación.

### Crear un usuario

Para crear un usuario, podemos usar el método `POST`.

```
curl -X POST localhost:8080/users -d '{"name": "John Doe", "email": "john.doe@example.com"}' -H "Content-Type: application/json"
```

Esto creará un usuario con el nombre `John Doe` y la dirección de correo electrónico `john.doe@example.com`.

### Obtener un usuario por ID

Para recuperar un usuario, podemos usar el método `GET`.

```
curl localhost:8080/users/1
```

Esto recuperará al usuario con el ID `1`.

### Obtener todos los usuarios

Para recuperar todos los usuarios, podemos usar el método `GET`.

```
curl localhost:8080/users
```

Esto recuperará a todos los usuarios.

### Actualizar un usuario

Para actualizar un usuario, podemos usar el método `PUT`.

```
curl -X PUT localhost:8080/users -d '{"id": "1", "name": "John Doe", "email": "john.doe@example.com"}' -H "Content-Type: application/json"
```

Esto actualizará al usuario con el ID `1`.

### Eliminar un usuario

Para eliminar un usuario, podemos usar el método `DELETE`.

```
curl -X DELETE localhost:8080/users/1
```

Esto eliminará al usuario con el ID `1`.

## Conclusión

En este artículo, le mostramos cómo crear una aplicación CRUD simple con Spring Boot. También le mostramos cómo probar la aplicación usando `curl`.

Ahora que sabe cómo crear una aplicación CRUD con Spring Boot, puede crear sus propias aplicaciones. También puede encontrar más información en el sitio web de Spring Boot: https://spring.io/projects/spring-boot