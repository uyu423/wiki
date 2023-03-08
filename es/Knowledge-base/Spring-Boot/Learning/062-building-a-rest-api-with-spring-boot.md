---
title: 062: Creación de una API REST con Spring Boot
description: 
published: true
date: 2023-02-03T02:57:30.112Z
tags: 
editor: markdown
dateCreated: 2023-02-03T02:57:28.431Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [062: Building a REST API with Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/062-building-a-rest-api-with-spring-boot)
{.links-list}


# 062: Construyendo una API REST con Spring Boot

En esta publicación, aprenderemos cómo crear una API REST con Spring Boot.

Comenzaremos creando un nuevo proyecto Spring Boot. Luego, agregaremos una dependencia a nuestro proyecto que nos permitirá crear una API REST.

A continuación, crearemos un controlador que manejará las solicitudes HTTP a nuestra API. Finalmente, probaremos nuestra API usando Postman.

## Creación de un proyecto Spring Boot

Primero, necesitaremos crear un nuevo proyecto Spring Boot. Podemos hacer esto usando Spring Initializr.

Tendremos que especificar la siguiente información:

- Grupo: com.ejemplo
- Artefacto: demostración
- Nombre: Aplicación de demostración
- Descripción: Proyecto de demostración para 062
- Nombre del paquete: com.example.demo
- Envase: Tarro
- Versión Java: 8
- Idioma: Kotlin
- Versión de arranque: 2.1.5

![primavera-inicializr](https://i.imgur.com/eU0mhVv.png)

Una vez que hayamos llenado el formulario, podemos hacer clic en "Generar proyecto". Esto descargará un archivo ZIP que contiene nuestro proyecto.

## Agregar una dependencia

A continuación, necesitaremos agregar una dependencia a nuestro proyecto. Esta dependencia nos permitirá crear una API REST.

Podemos hacer esto agregando lo siguiente a nuestro archivo build.gradle:

```groovy
dependencies {
    ...
    compile("org.springframework.boot:spring-boot-starter-web")
}
```

## Crear un controlador

Ahora que tenemos nuestro proyecto configurado, podemos comenzar a crear nuestra API.

Comenzaremos creando un controlador. Este controlador manejará las solicitudes HTTP a nuestra API.

Podemos hacer esto creando un nuevo archivo Kotlin llamado DemoController.kt en el paquete com.example.demo.

```kotlin
package com.example.demo

import org.springframework.web.bind.annotation.GetMapping
import org.springframework.web.bind.annotation.RestController

@RestController
class DemoController {

    @GetMapping("/")
    fun index(): String {
        return "Hello, world!"
    }
}
```

En este archivo, hemos creado un controlador con un solo punto final. Este punto final devolverá la cadena "¡Hola, mundo!" cuando se accede.

## Probando nuestra API

Ahora que hemos creado nuestra API, podemos probarla para asegurarnos de que funciona como se esperaba.

Podemos hacer esto usando Postman. Postman es una herramienta que nos permite enviar solicitudes HTTP a nuestra API.

Primero, necesitaremos iniciar nuestra aplicación. Esto lo podemos hacer ejecutando el siguiente comando:

```
./gradlew bootRun
```

Una vez que nuestra aplicación se ha iniciado, podemos enviar una solicitud HTTP GET al punto final "/". Deberíamos ver la cadena "¡Hola, mundo!" en el cuerpo de respuesta.

![cartero](https://i.imgur.com/zgWVLCg.png)

## Conclusión

En esta publicación, hemos aprendido cómo crear una API REST con Spring Boot. Creamos un nuevo proyecto, agregamos una dependencia, creamos un controlador y probamos nuestra API.