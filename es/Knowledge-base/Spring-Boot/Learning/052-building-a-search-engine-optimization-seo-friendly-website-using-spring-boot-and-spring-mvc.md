---
title: 052: Creación de un sitio web compatible con la optimización de motores de búsqueda (SEO) utilizando Spring Boot y Spring MVC
description: 
published: true
date: 2023-02-02T18:57:28.155Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:57:26.477Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [052: Building a search engine optimization (SEO) friendly website using Spring Boot and Spring MVC***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/052-building-a-search-engine-optimization-seo-friendly-website-using-spring-boot-and-spring-mvc)
{.links-list}


## Introducción

La optimización de motores de búsqueda (SEO) es la práctica de mejorar la clasificación de un sitio web en los motores de búsqueda. Cuanto más alto sea el ranking, más probabilidades hay de que las personas encuentren el sitio web.

Hay muchos factores que contribuyen a la clasificación de un sitio web, incluida la calidad del contenido, la estructura del sitio web y la forma en que está codificado.

En esta publicación, nos centraremos en cómo codificar un sitio web utilizando Spring Boot y Spring MVC que sea compatible con los motores de búsqueda.

## ¿Qué es Spring Boot?

Spring Boot es un marco que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

Spring Boot incluye una serie de características que facilitan la creación y ejecución de una aplicación web, que incluyen:

- Servidor Tomcat o Jetty integrado
- Compatibilidad con Thymeleaf, FreeMarker y otros motores de plantillas
- Configuración automática
- Generación automática de documentación del proyecto.

## ¿Qué es Spring MVC?

Spring MVC es un marco para crear aplicaciones web. Está construido sobre el marco Spring y proporciona un enfoque unificado para el desarrollo de aplicaciones web.

Spring MVC incluye una serie de características que facilitan el desarrollo de aplicaciones web, que incluyen:

- Un modelo simple y consistente para el manejo de solicitudes y respuestas.
- Un mecanismo de resolución de vista flexible
- Soporte para múltiples tecnologías de vista
- Un mecanismo de localización enchufable

## Creación de una aplicación web Spring Boot

Usaremos Spring Initializr para crear una aplicación web Spring Boot.

Vaya al sitio web de Spring Initializr (https://start.spring.io/) y complete el formulario para crear un nuevo proyecto.

![Inicializar resorte](https://i.imgur.com/hm3Y6uq.png)

Selecciona las siguientes opciones:

- Proyecto: Proyecto Gradle
- Idioma: Java
- Versión de arranque de primavera: 2.1.4

Haga clic en "Generar proyecto" para descargar el proyecto.

## Importando el Proyecto a Eclipse

Importe el proyecto a Eclipse como un proyecto de Gradle.

## Crear un controlador

Los controladores son el corazón de una aplicación Spring MVC. Son responsables de manejar las solicitudes y respuestas.

En nuestro ejemplo, crearemos un controlador que maneje las solicitudes a la URL "/".

Cree una nueva clase en el paquete com.example.demo y asígnele el nombre "HelloController.java".

Agregue el siguiente código a la clase:

```java
package com.example.demo;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class HelloController {

    @RequestMapping("/")
    @ResponseBody
    public String index() {
        return "Hello, world!";
    }

}
```

La anotación ```@Controller``` marca la clase como un controlador.

La anotación ```@RequestMapping``` asigna solicitudes a la URL "/" al método index().

La anotación ```@ResponseBody``` indica que la cadena devuelta por el método index() debe ser el cuerpo de la respuesta.

## Crear una vista

En una aplicación Spring MVC, las vistas suelen ser archivos de plantilla que procesa un motor de plantilla.

En nuestro ejemplo, utilizaremos el motor de plantillas Thymeleaf para procesar un archivo de plantilla HTML.

Cree un nuevo directorio en el directorio src/main/resources y asígnele el nombre "templates".

Cree un nuevo archivo en el directorio de plantillas y asígnele el nombre "index.html".

Agregue el siguiente código al archivo:

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Hello, world!</title>
    </head>
    <body>
        <p>Hello, world!</p>
    </body>
</html>
```

## Configuración de la aplicación

Las aplicaciones Spring Boot normalmente se configuran mediante archivos de propiedades.

En nuestro ejemplo, utilizaremos un archivo de propiedades para configurar el motor de plantillas de Thymeleaf.

Cree un nuevo archivo en el directorio src/main/resources y asígnele el nombre "application.properties".

Agregue el siguiente código al archivo:

```properties
spring.thymeleaf.prefix=classpath:/templates/
spring.thymeleaf.suffix=.html
spring.thymeleaf.mode=HTML5
spring.thymeleaf.encoding=UTF-8
spring.thymeleaf.content-type=text/html
spring.thymeleaf.cache=false
```

## Ejecutando la aplicación

Podemos ejecutar la aplicación desde la línea de comandos o desde Eclipse.

Para ejecutar la aplicación desde la línea de comandos, vaya al directorio del proyecto y escriba el siguiente comando:

```
./gradlew bootRun
```

Para ejecutar la aplicación desde Eclipse, haga clic derecho en el proyecto y seleccione "Ejecutar como -> Aplicación Spring Boot".

## Prueba de la aplicación

Podemos probar la aplicación enviando una solicitud a la URL "/".

Para probar la aplicación desde la línea de comandos, podemos usar el comando curl.

```
curl http://localhost:8080/
```

Para probar la aplicación de Eclipse, podemos usar el navegador incorporado.

Haga clic derecho en el archivo HelloController.java y seleccione "Ejecutar como -> Aplicación Spring Boot".

Se iniciará la aplicación y se abrirá la URL "/" en el navegador.

## Conclusión

En esta publicación, hemos visto cómo crear un sitio web compatible con la optimización de motores de búsqueda (SEO) utilizando Spring Boot y Spring MVC.

Hemos visto cómo crear un controlador que maneje solicitudes y respuestas, y cómo crear una vista que sea procesada por un motor de plantillas.

También hemos visto cómo configurar la aplicación mediante archivos de propiedades.