---
title: 024: Implementación de paginación en una aplicación Spring Boot
description: 
published: true
date: 2023-02-03T16:32:20.210Z
tags: 
editor: markdown
dateCreated: 2023-02-03T16:32:18.619Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [024: Implementing pagination in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/024-implementing-pagination-in-a-spring-boot-application)
{.links-list}


La paginación es una característica común en las aplicaciones web. Se utiliza para dividir grandes conjuntos de datos en fragmentos más pequeños y manejables. Spring Boot facilita la implementación de la paginación en una aplicación web.

En esta publicación, aprenderemos cómo implementar la paginación en una aplicación Spring Boot. Comenzaremos creando una aplicación Spring Boot simple. Luego, agregaremos la función de paginación a la aplicación.

Creación de una aplicación Spring Boot

Usaremos Spring Initializr para crear nuestra aplicación Spring Boot. Vaya al sitio web de Spring Initializr y seleccione las siguientes opciones:

* Proyecto: Proyecto Maven
* Idioma: Java
* Versión de arranque de primavera: 2.1.3

Haga clic en el botón "Generar" para generar el proyecto.

Una vez que se genera el proyecto, impórtelo a su IDE favorito. Estoy usando Eclipse.

Agregar la función de paginación

Usaremos la interfaz Pageable del paquete org.springframework.data.domain para implementar la paginación en nuestra aplicación.

Primero, necesitamos agregar la dependencia spring-data-commons a nuestro archivo pom.xml:

```xml
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-commons</artifactId>
    <version>2.1.3.RELEASE</version>
</dependency>
```

A continuación, crearemos un RestController simple con un método que devuelva una lista de usuarios:

```java
@RestController
public class UserController {

    @GetMapping("/users")
    public List<User> getUsers() {
        // Return a list of users
    }
}
```

Ahora, agregaremos la función de paginación al método getUsers(). Usaremos la interfaz Paginable para especificar el tamaño de página y el número de página. La interfaz Pageable tiene dos implementaciones: PageRequest y Slice. Usaremos la implementación de PageRequest en nuestro ejemplo.

```java
@GetMapping("/users")
public List<User> getUsers(Pageable pageable) {
    // Return a list of users
}
```

También podemos especificar el tamaño de página y el número de página como parámetros de consulta:

```java
@GetMapping("/users")
public List<User> getUsers(
        @RequestParam(name = "page", defaultValue = "0") int page,
        @RequestParam(name = "size", defaultValue = "10") int size) {
    // Return a list of users
}
```

En el ejemplo anterior, hemos especificado que el tamaño de página predeterminado es 10 y el número de página predeterminado es 0.

Probando la función de paginación

Podemos probar la función de paginación enviando una solicitud GET al punto final /users con los parámetros de consulta de página y tamaño.

Por ejemplo, la siguiente solicitud devolverá la primera página de usuarios con un tamaño de página de 10:

```
GET /users?page=0&size=10
```

La siguiente solicitud devolverá la segunda página de usuarios con un tamaño de página de 10:

```
GET /users?page=1&size=10
```

Etcétera.

información adicional

La interfaz Pageable tiene varios otros métodos que se pueden usar para personalizar el comportamiento de paginación. Para obtener más información, consulte los JavaDocs para la interfaz Pageable.

Advertencias

Al implementar la paginación, es importante asegurarse de que el tamaño de la página no sea demasiado grande. Si el tamaño de la página es demasiado grande, puede generar OutOfMemoryErrors.

peligros

Al implementar la paginación, es importante asegurarse de que el tamaño de la página no sea demasiado pequeño. Si el tamaño de la página es demasiado pequeño, puede generar demasiadas consultas a la base de datos.