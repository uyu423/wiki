---
title: 030: Desarrollo e implementación de una aplicación Spring Boot con Gradle
description: 
published: true
date: 2023-02-03T22:32:28.692Z
tags: 
editor: markdown
dateCreated: 2023-02-03T22:32:27.163Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [030: Developing and deploying a Spring Boot application with Gradle***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/030-developing-and-deploying-a-spring-boot-application-with-gradle)
{.links-list}


# 030: Desarrollo e implementación de una aplicación Spring Boot con Gradle

Spring Boot es un marco Java popular para desarrollar aplicaciones web. Facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción que puede "simplemente ejecutar".

En esta publicación, veremos cómo desarrollar e implementar una aplicación Spring Boot usando Gradle. Comenzaremos configurando nuestro proyecto, luego escribiremos nuestro código y lo empaquetaremos en un archivo jar. Finalmente, implementaremos nuestra aplicación en un servidor.

## Configurando nuestro proyecto

Lo primero que tenemos que hacer es configurar nuestro proyecto. Crearemos un nuevo directorio para nuestro proyecto e inicializaremos un script de compilación de Gradle.

```
$ mkdir my-spring-boot-app
$ cd my-spring-boot-app
$ gradle init
```

A continuación, debemos agregar la dependencia de Spring Boot a nuestro script de compilación. Haremos esto agregando la siguiente línea a nuestro archivo `build.gradle`:

```
dependencies {
    compile 'org.springframework.boot:spring-boot-starter-web'
}
```

## Escribiendo nuestro código

Ahora que nuestro proyecto está configurado, podemos comenzar a escribir nuestro código. Crearemos una aplicación Spring Boot simple que imprima "¡Hola, mundo!"

Primero, crearemos un archivo llamado `HelloWorldController.java` en nuestro directorio `src/main/java`. Este archivo contendrá nuestro controlador:

```java
package com.example.myapp;

import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class HelloWorldController {

    @RequestMapping("/")
    public String index() {
        return "Hello, world!";
    }

}
```

A continuación, crearemos un archivo llamado `Application.java` en nuestro directorio `src/main/java`. Este archivo contendrá nuestra clase de aplicación principal:

```java
package com.example.myapp;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## Empaquetando nuestra aplicación

Ahora que nuestro código está escrito, debemos empaquetarlo en un archivo jar. Podemos hacer esto ejecutando el comando `gradle build`. Esto creará un archivo jar en nuestro directorio `build/libs`.

## Desplegando nuestra aplicación

Ahora que nuestra aplicación está empaquetada, podemos implementarla en un servidor. Usaremos el comando `java -jar` para ejecutar nuestro archivo jar:

```
$ java -jar build/libs/my-spring-boot-app.jar
```

Nuestra aplicación se iniciará en el puerto 8080. Podemos acceder a ella yendo a http://localhost:8080 en nuestro navegador.

## Conclusión

En esta publicación, hemos repasado cómo desarrollar e implementar una aplicación Spring Boot usando Gradle. Configuramos nuestro proyecto, escribimos nuestro código, lo empaquetamos en un archivo jar y lo implementamos en un servidor.