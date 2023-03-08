---
title: Spring Boot y Docker para microservicios
description: 
published: true
date: 2023-02-08T01:32:41.718Z
tags: 
editor: markdown
dateCreated: 2023-02-08T01:32:40.085Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot and Docker for Microservices***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-docker-for-microservices)
{.links-list}


# Introducción

Los desarrolladores están recurriendo a los microservicios como una forma de crear aplicaciones escalables. Los microservicios son un tipo de arquitectura de software donde las aplicaciones grandes se construyen como una colección de servicios pequeños e independientes. Este enfoque tiene muchos beneficios, incluida la capacidad de actualizar e implementar servicios de forma independiente y la capacidad de escalar los servicios horizontalmente.

Si bien los microservicios ofrecen muchos beneficios, también pueden ser complejos de administrar. Ahí es donde entra en juego Docker. Docker es una plataforma de creación de contenedores que facilita el empaquetado, la implementación y la administración de microservicios.

En este artículo, veremos cómo usar Docker y Spring Boot para desarrollar e implementar microservicios. Comenzaremos con un ejemplo simple, luego exploraremos algunas de las funciones más avanzadas que Spring Boot y Docker ofrecen para desarrollar microservicios.

# ¿Qué es Spring Boot?

Spring Boot es un marco basado en Java que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción. Proporciona una serie de características que facilitan el desarrollo y la implementación de microservicios, que incluyen:

- Tomcat incorporado: Spring Boot viene con un servidor Tomcat incorporado, lo que facilita la ejecución de su aplicación como una aplicación Java independiente.
- Gestión de dependencias: Spring Boot gestiona automáticamente las dependencias por usted. Esto puede ser un gran ahorro de tiempo cuando está desarrollando microservicios, ya que no tiene que preocuparse por administrar manualmente las dependencias.
- Configuración: Spring Boot ofrece una variedad de formas de configurar su aplicación. Puede utilizar archivos de propiedades de Java estándar, archivos YAML o variables de entorno. Esto facilita la configuración de su aplicación para diferentes entornos (desarrollo, producción, etc.).

# ¿Qué es Docker?

Docker es una plataforma de contenedores que facilita el empaquetado, la implementación y la administración de aplicaciones. Los contenedores Docker son entornos autónomos y aislados que facilitan el empaquetado y la implementación de aplicaciones.

Los contenedores Docker son livianos y portátiles, lo que los hace ideales para microservicios. También tienen el beneficio adicional de ser independientes de la plataforma, por lo que se pueden implementar en cualquier plataforma que admita Docker.

# Desarrollo de Microservicios con Spring Boot y Docker

En esta sección, veremos cómo desarrollar e implementar un microservicio simple usando Spring Boot y Docker.

# Creando el Proyecto

Primero, necesitaremos crear un nuevo proyecto Spring Boot. Podemos hacer esto usando Spring Initializr. Initializr es una herramienta basada en web que facilita la creación de proyectos Spring Boot.

Comenzaremos creando un proyecto Maven simple. Llamaremos a nuestro proyecto "hello-world" y usaremos la última versión de Spring Boot (2.0.4 en el momento de escribir este artículo). También agregaremos las dependencias "Web" y "Actuator", ya que las necesitaremos para nuestro ejemplo.

Una vez que se haya creado el proyecto, necesitaremos agregar algunas dependencias a nuestro archivo `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

# Creando el Servicio

Ahora que tenemos nuestro proyecto configurado, podemos crear nuestro microservicio. Comenzaremos creando un `HelloController` simple:

```java
@RestController
public class HelloController {

    @RequestMapping("/")
    public String index() {
        return "Hello, world!";
    }
}
```

Este controlador se asignará a la ruta `/` y devolverá la cadena "¡Hola, mundo!" cuando se llama

# Agregar un Dockerfile

Ahora que hemos creado nuestro microservicio, necesitamos agregar un `Dockerfile` a nuestro proyecto. Un `Dockerfile` es un archivo de texto que contiene las instrucciones para crear una imagen de Docker.

Nuestro `Dockerfile` será muy simple. Comenzaremos especificando la imagen base que queremos usar. Para nuestro ejemplo, usaremos la imagen `openjdk:8-jdk-alpine`. Esta imagen contiene una versión mínima de Alpine Linux y OpenJDK 8 JDK.

A continuación, añadiremos unas líneas para instalar las dependencias que necesita nuestra aplicación:

```dockerfile
FROM openjdk:8-jdk-alpine

RUN apk add --no-cache curl
```

Estamos usando el comando `apk` para instalar la herramienta de línea de comandos `curl`. `curl` se usará más tarde para hacer una solicitud a nuestra aplicación para probar que se está ejecutando.

Ahora, agregaremos algunas líneas para copiar el archivo jar de nuestra aplicación en la imagen y para especificar el comando que debe ejecutarse cuando se inicia el contenedor:

```dockerfile
FROM openjdk:8-jdk-alpine

RUN apk add --no-cache curl

COPY target/hello-world-0.0.1-SNAPSHOT.jar /hello-world.jar

ENTRYPOINT ["java", "-jar", "/hello-world.jar"]
```

# Construyendo la imagen de Docker

Ahora que tenemos nuestro `Dockerfile`, podemos construir nuestra imagen de Docker. Usaremos el comando `docker build` para construir la imagen. Le daremos a nuestra imagen el nombre "hello-world":

```
$ docker build -t hello-world .
```

# Ejecutando el Contenedor

Ahora que tenemos nuestra imagen de Docker, podemos ejecutar nuestro contenedor. Usaremos el comando `docker run` para ejecutar nuestro contenedor. También especificaremos el puerto en el que queremos que se ejecute nuestro contenedor. En nuestro ejemplo, usaremos el puerto 8080:

```
$ docker run -p 8080:8080 hello-world
```

# Prueba de la aplicación

Ahora que nuestro contenedor se está ejecutando, podemos probar nuestra aplicación. Usaremos el comando `curl` para hacer una solicitud a nuestra aplicación:

```
$ curl http://localhost:8080

Hello, world!
```

# Conclusión

En este artículo, hemos visto cómo usar Spring Boot y Docker para desarrollar e implementar microservicios. Hemos visto cómo crear un microservicio simple, cómo crear una imagen de Docker para nuestro servicio y cómo ejecutar nuestro servicio en un contenedor de Docker.