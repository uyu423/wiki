---
title: 004: Creación de API REST con Spring Boot y Spring MVC
description: 
published: true
date: 2023-02-03T07:36:48.329Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:36:46.724Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [004: Building REST APIs with Spring Boot and Spring MVC***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/004-building-rest-apis-with-spring-boot-and-spring-mvc)
{.links-list}


# 004: Creación de API REST con Spring Boot y Spring MVC

En esta publicación, aprenderemos cómo crear API REST con Spring Boot y Spring MVC.

Comenzaremos creando una aplicación Spring Boot simple. Luego, agregaremos un controlador para exponer algunos puntos finales REST. Finalmente, probaremos nuestra API usando Postman.

## Crear una aplicación Spring Boot

Primero, necesitaremos crear una aplicación Spring Boot. Podemos usar Spring Initializr para hacer esto.

Vaya a http://start.spring.io/ y seleccione las siguientes opciones:

- Generar un Proyecto Maven con Java y Spring Boot 2.0
- Envase: Tarro
- Versión Java: 8
- Grupo: com.ejemplo
- Artefacto: demostración
- Nombre: Aplicación de demostración
- Descripción: Demostración de Spring Boot REST API
- Nombre del paquete: com.example.demo

Haga clic en Generar proyecto para descargar el proyecto.

Extraiga el archivo zip y abra el proyecto en su IDE favorito.

## Agregar un controlador

A continuación, agregaremos un controlador para exponer algunos puntos finales REST.

Primero, crearemos un nuevo paquete llamado `com.example.demo.controller`. Luego, crearemos una nueva clase llamada `DemoController` dentro de ese paquete.

Nuestro controlador tendrá los siguientes puntos finales:

- `GET /`: Un mensaje de bienvenida
- `GET /hola`: Un saludo
- `POST /saludo`: Un saludo con un mensaje personalizado

Aquí está el código para nuestro controlador:

```java
package com.example.demo.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class DemoController {

    @GetMapping("/")
    public String index() {
        return "Welcome to the Spring Boot REST API!";
    }

    @GetMapping("/hello")
    public String hello() {
        return "Hello, Spring Boot!";
    }

    @PostMapping("/greeting")
    public String greeting(@RequestParam(value="name", defaultValue="World") String name) {
        return "Hello, " + name + "!";
    }

}
```

Analicemos lo que está sucediendo en el código anterior.

Primero, estamos usando la anotación `@RestController` para designar esta clase como controlador.

Luego, usamos las anotaciones `@GetMapping` y `@PostMapping` para asignar solicitudes HTTP GET y POST a métodos específicos en nuestro controlador.

Finalmente, estamos usando la anotación `@RequestParam` para extraer los parámetros de consulta de la solicitud. En este caso, estamos extrayendo el parámetro `name`. Si no se especifica el parámetro `name`, estamos usando el valor predeterminado de `World`.

## Probando la API

Ahora que tenemos nuestro controlador configurado, probemos nuestra API usando Postman.

Primero, necesitaremos iniciar nuestra aplicación. Podemos hacer esto ejecutando la clase `DemoApplication` como una aplicación Java.

Una vez iniciada la aplicación, podemos enviar solicitudes a nuestra API mediante Postman.

Enviemos una solicitud GET al extremo `/`:

![Solicitud de obtención](https://i.imgur.com/LNcuFtD.png)

Como puede ver, recibimos un mensaje de bienvenida en respuesta.

Enviemos una solicitud GET al extremo `/hello`:

![solicitud de saludo](https://i.imgur.com/VywYbnK.png)

Como puede ver, recibimos un saludo como respuesta.

Finalmente, enviemos una solicitud POST al extremo `/saludo`:

![Solicitud posterior](https://i.imgur.com/EC4nUg4.png)

Como puede ver, recibimos un saludo con un mensaje personalizado como respuesta.

## Conclusión

En esta publicación, aprendimos cómo crear API REST con Spring Boot y Spring MVC.

Comenzamos creando una aplicación Spring Boot simple. Luego, agregamos un controlador para exponer algunos puntos finales REST. Finalmente, probamos nuestra API usando Postman.