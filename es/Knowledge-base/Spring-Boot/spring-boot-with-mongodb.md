---
title: Arranque de primavera con MongoDB
description: 
published: true
date: 2023-02-07T10:32:36.629Z
tags: 
editor: markdown
dateCreated: 2023-02-07T10:32:34.922Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot with MongoDB***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-with-mongodb)
{.links-list}


# Spring Boot con MongoDB

Spring Boot es un marco popular basado en Java que se utiliza para crear microservicios. Ofrece una forma sencilla de crear aplicaciones basadas en Spring de nivel de producción independientes que puede "simplemente ejecutar".

 MongoDB es una base de datos NoSQL de código abierto que utiliza un modelo de datos orientado a documentos. Es una poderosa herramienta para el manejo y análisis de datos.

En este artículo, le mostraremos cómo conectar Spring Boot con MongoDB.

## Requisitos previos

Para seguir este artículo, necesitará lo siguiente:

- Java 8 o superior
- Spring Boot 2.0 o superior
- MongoDB 3.6 o superior

## Creación de un proyecto Spring Boot

Usaremos Spring Initializr para generar nuestro proyecto Spring Boot.

Vaya a http://start.spring.io/ y seleccione lo siguiente:

- Proyecto: Proyecto Maven
- Idioma: Java
- Bota de primavera: 2.0.3
- Grupo: com.ejemplo
- Artefacto: demostración

Haga clic en **Generar proyecto**.

## Configuración de MongoDB

Spring Boot buscará un archivo llamado `application.properties` (o `application.yml`) en el directorio `src/main/resources`. Aquí es donde configuraremos nuestra conexión MongoDB.

Agregue lo siguiente a su archivo `application.properties`:

```
spring.data.mongodb.uri=mongodb://localhost/test
```

Esto se conectará a una base de datos MongoDB llamada `test` en `localhost`.

Si está utilizando `application.yml`, la configuración se verá así:

```yaml
spring:
  data:
    mongodb:
      uri: mongodb://localhost/test
```

## Creando un Repositorio MongoDB

A continuación, crearemos una interfaz de repositorio para nuestra base de datos MongoDB. Esto ampliará la interfaz `MongoRepository` proporcionada por Spring Data MongoDB.

```java
package com.example.demo.repository;

import org.springframework.data.mongodb.repository.MongoRepository;

import com.example.demo.model.User;

public interface UserRepository extends MongoRepository<User, String> {

}
```

La interfaz `UserRepository` realizará operaciones CRUD en la colección `User` en MongoDB.

## Creando un modelo MongoDB

Ahora crearemos una clase `Usuario` para representar documentos en la colección `Usuario`.

```java
package com.example.demo.model;

import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

@Document
public class User {

    @Id
    private String id;

    private String name;
    private int age;

    // Getters and setters
}
```

La anotación `@Document` le dice a Spring Data MongoDB que la clase `User` es un documento en la colección `User`.

La anotación `@Id` marca el campo `id` como la clave principal del documento.

## Crear un controlador REST

Ahora crearemos un controlador REST para exponer nuestro repositorio MongoDB como una API REST.

```java
package com.example.demo.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.bind.annotation.RestController;

import com.example.demo.model.User;
import com.example.demo.repository.UserRepository;

@RestController
@RequestMapping("/api/v1/users")
public class UserController {

    @Autowired
    private UserRepository userRepository;

    @RequestMapping(method = RequestMethod.GET)
    public List<User> getUsers() {
        return userRepository.findAll();
    }
}
```

La anotación `@RestController` marca la clase `UserController` como un controlador REST.

La anotación `@RequestMapping` asigna solicitudes HTTP a métodos en el controlador. En este caso, la ruta `/api/v1/users` se asigna al método `getUsers()`.

La anotación `@Autowired` inyecta `UserRepository` en el controlador.

El método `getUsers()` recupera una lista de usuarios de la base de datos MongoDB y la devuelve como JSON.

## Ejecutando la aplicación

Para ejecutar la aplicación, simplemente escriba el siguiente comando en su terminal:

```
./mvnw spring-boot:run
```

Debería ver el siguiente resultado:

```
...
2017-12-01 10:21:59.593  INFO 85511 --- [           main] s.b.c.e.t.TomcatEmbeddedServletContainer : Tomcat started on port(s): 8080 (http)
2017-12-01 10:21:59.596  INFO 85511 --- [           main] com.example.demo.DemoApplication         : Started DemoApplication in 4.166 seconds (JVM running for 4.681)
```

Ahora puede acceder a la API REST en http://localhost:8080/api/v1/users.

## Conclusión

En este artículo, le mostramos cómo conectar Spring Boot con MongoDB. También hemos creado una API REST simple para operaciones CRUD en nuestra base de datos MongoDB.

Para obtener más información sobre Spring Boot, consulte los siguientes recursos:

- [Documentación de Spring Boot] (https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
- [Tutorial de Spring Boot con MongoDB](https://www.baeldung.com/spring-boot-mongodb)

Para obtener más información sobre MongoDB, consulte los siguientes recursos:

- [Documentación de MongoDB](https://docs.mongodb.com/)
- [Universidad MongoDB](https://university.mongodb.com/)