---
title: 077: Implementación de una aplicación Spring Boot con Docker
description: 
published: true
date: 2023-02-05T08:32:53.790Z
tags: 
editor: markdown
dateCreated: 2023-02-05T08:32:52.066Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [077: Deploying a Spring Boot Application with Docker***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/077-deploying-a-spring-boot-application-with-docker)
{.links-list}


## Introducción

Docker es una tecnología de creación de contenedores que le permite empaquetar una aplicación con todas sus dependencias y enviarla como una sola unidad. Esto facilita la implementación y ejecución de su aplicación en cualquier host que admita Docker.

En esta publicación, aprenderemos cómo implementar una aplicación Spring Boot con Docker. Comenzaremos creando una aplicación Spring Boot simple y empaquetándola como una imagen de Docker. Luego, ejecutaremos la imagen de Docker en un host de Docker local. Finalmente, enviaremos la imagen de Docker a un registro de Docker para que pueda implementarse en un servidor de producción.

## Requisitos previos

Para seguir con esta publicación, necesitará lo siguiente:

- Un editor de texto
-JDK 8 o posterior
-Maven 3.0 o posterior
- Docker CE 18.03 o posterior

## Construyendo una aplicación Spring Boot

Comenzaremos creando una aplicación Spring Boot simple. La aplicación tendrá un punto final REST único que devuelve una lista de países.

Primero, cree un nuevo directorio para el proyecto y cambie a ese directorio. Luego crea un archivo llamado `pom.xml` con los siguientes contenidos:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>spring-boot-docker-example</artifactId>
    <version>1.0-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.4.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```

Este es el archivo `pom.xml` de Maven para el proyecto. Usamos el padre de inicio de Spring Boot, que proporciona una manera conveniente de administrar las dependencias y configurar la compilación. También usamos la dependencia web inicial de Spring Boot, que incluye las dependencias para crear una aplicación web.

A continuación, cree un archivo llamado `src/main/java/com/example/springboot/Application.java` con el siguiente contenido:

```java
package com.example.springboot;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

Esta es la clase de aplicación principal. Utiliza la anotación `@SpringBootApplication` para habilitar la configuración automática y el escaneo de componentes.

A continuación, cree un archivo llamado `src/main/java/com/example/springboot/controller/CountryController.java` con el siguiente contenido:

```java
package com.example.springboot.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Arrays;
import java.util.List;

@RestController
public class CountryController {

    @GetMapping("/countries")
    public List<String> getCountries() {
        return Arrays.asList("Australia", "Canada", "France", "Germany", "India", "Japan", "United Kingdom", "United States");
    }

}
```

Este es el controlador para el punto final `/countries`. Devuelve una lista de países.

Ahora que la aplicación está completa, podemos empaquetarla como una imagen de Docker.

## Empaquetar la aplicación como una imagen de Docker

Usaremos Maven para empaquetar la aplicación como una imagen de Docker. Primero, necesitamos agregar un `<plugin>` al archivo `pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
        <plugin>
            <groupId>com.spotify</groupId>
            <artifactId>dockerfile-maven-plugin</artifactId>
            <version>1.3.6</version>
            <configuration>
                <repository>${docker.repository}</repository>
                <tag>${project.version}</tag>
                <buildArgs>
                    <JAR_FILE>target/${project.build.finalName}.jar</JAR_FILE>
                </buildArgs>
            </configuration>
        </plugin>
    </plugins>
</build>
```

Esto agrega el complemento Spotify Dockerfile Maven, que empaquetará la aplicación como una imagen de Docker. También estamos configurando el complemento para usar `${project.version}` como etiqueta de imagen de Docker y para pasar el archivo `${project.build.finalName}.jar` como argumento de compilación.

A continuación, cree un archivo llamado `src/main/docker/Dockerfile` con el siguiente contenido:

```dockerfile
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG JAR_FILE
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```

Este es el Dockerfile para la imagen. Utiliza la imagen de OpenJDK 8 Alpine Docker como imagen base. También copia `${JAR_FILE}` en el archivo `app.jar` y lo establece como punto de entrada para la imagen.

Ahora podemos empaquetar la aplicación como una imagen de Docker ejecutando el siguiente comando:

```
$ mvn package docker:build
```

Esto empaquetará la aplicación como un archivo JAR y creará una imagen de Docker. La imagen de Docker se etiquetará con `${project.version}`, que en este caso es `1.0-SNAPSHOT`.

## Ejecutar la imagen de Docker

Ahora que tenemos una imagen de Docker, podemos ejecutarla en un host de Docker local. Primero, necesitamos iniciar un host Docker. Si está utilizando Docker Machine, puede iniciar un host Docker con el siguiente comando:

```
$ docker-machine create --driver virtualbox default
```

Esto creará un host Docker con el nombre `default`.

A continuación, debemos configurar algunas variables de entorno para poder acceder al host de Docker:

```
$ eval $(docker-machine env default)
```

Ahora podemos ejecutar la imagen de Docker con el siguiente comando:

```
$ docker run -d -p 8080:8080 spring-boot-docker-example:1.0-SNAPSHOT
```

Esto ejecutará la imagen de Docker en modo separado y asignará el puerto '8080' en el host de Docker al puerto '8080' en el contenedor.

Puede verificar que el contenedor se está ejecutando con el siguiente comando:

```
$ docker ps
```

Debería ver una salida como esta:

```
CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
e9c4b7a4d4f4        spring-boot-docker-example:1.0   "java -Djava.securit…"   3 seconds ago       Up 2 seconds        0.0.0.0:8080->8080/tcp   stoic_ardinghelli
```

Ahora podemos acceder a la aplicación abriendo http://localhost:8080 en un navegador web. Deberías ver una página como esta:

![Ejemplo de Spring Boot Docker](https://i.imgur.com/hm4Tv0b.png)

## Empujando la imagen de Docker a un registro

Ahora que tenemos una imagen de Docker en funcionamiento, podemos enviarla a un registro de Docker para que pueda implementarse en un servidor de producción.

Primero, necesitamos crear un registro de Docker. Usaremos Docker Hub para este ejemplo. Regístrese para obtener una cuenta de Docker Hub y luego cree un nuevo repositorio. Llamaremos a nuestro repositorio `spring-boot-docker-example`.

Una vez que se ha creado el repositorio, podemos enviarle nuestra imagen de Docker con el siguiente comando:

```
$ docker push spring-boot-docker-example:1.0-SNAPSHOT
```

Esto enviará la imagen `spring-boot-docker-example:1.0-SNAPSHOT` al repositorio `spring-boot-docker-example` en Docker Hub.

## Conclusión

En esta publicación, aprendimos cómo implementar una aplicación Spring Boot con Docker. Comenzamos creando una aplicación Spring Boot simple y empaquetándola como una imagen de Docker. Luego, ejecutamos la imagen de Docker en un host de Docker local. Finalmente, empujamos la imagen de Docker a un registro de Docker para que pudiera implementarse en un servidor de producción.