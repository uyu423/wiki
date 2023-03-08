---
title: 017: Desarrollo e implementación de aplicaciones Spring Boot con Docker
description: 
published: true
date: 2023-02-03T10:04:55.413Z
tags: 
editor: markdown
dateCreated: 2023-02-03T10:04:53.794Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [017: Developing and deploying Spring Boot applications with Docker***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/017-developing-and-deploying-spring-boot-applications-with-docker)
{.links-list}


# Desarrollo e implementación de aplicaciones Spring Boot con Docker

Docker es una herramienta que puede simplificar enormemente el proceso de desarrollo e implementación de aplicaciones Spring Boot. En esta publicación, veremos cómo usar Docker para desarrollar e implementar una aplicación Spring Boot.

## Desarrollo de una aplicación Spring Boot con Docker

Desarrollar una aplicación Spring Boot con Docker es muy sencillo. Todo lo que necesita es un editor de texto y un Dockerfile.

Un Dockerfile es un archivo de texto que contiene todos los comandos necesarios para crear una imagen de Docker. Una imagen de Docker es un archivo que contiene todos los archivos y dependencias necesarios para que se ejecute una aplicación.

Para crear un Dockerfile, cree un nuevo archivo llamado `Dockerfile` en el directorio raíz de su proyecto. Luego, agregue las siguientes líneas al archivo:

```
FROM java:8

ADD . /app

WORKDIR /app

RUN ./gradlew build

EXPOSE 8080

CMD ["java", "-jar", "build/libs/spring-boot-app-0.0.1-SNAPSHOT.jar"]
```

La primera línea, `FROM java:8`, le dice a Docker que use la imagen de Docker `java:8` como imagen base para nuestra aplicación. La imagen Docker `java:8` contiene todos los archivos y dependencias necesarios para una aplicación Java 8.

La segunda línea, `ADD . /app`, le dice a Docker que agregue todos los archivos en el directorio actual (`./`) al directorio `/app` en la imagen de Docker.

La tercera línea, `WORKDIR /app`, le dice a Docker que use el directorio `/app` como directorio de trabajo para nuestra aplicación.

La cuarta línea, `RUN ./gradlew build`, le dice a Docker que ejecute el comando `./gradlew build` para compilar nuestra aplicación. Este comando compilará nuestro código y creará un archivo `.jar` en el directorio `build/libs`.

La quinta línea, `EXPOSE 8080`, le dice a Docker que exponga el puerto `8080` para nuestra aplicación.

La sexta y última línea, `CMD ["java", "-jar", "build/libs/spring-boot-app-0.0.1-SNAPSHOT.jar"]`, le dice a Docker que ejecute el comando `java` con la opción `-jar` y el archivo `spring-boot-app-0.0.1-SNAPSHOT.jar` como argumentos. Esto iniciará nuestra aplicación en el puerto `8080`.

Ahora que tenemos un Dockerfile, podemos crear una imagen de Docker para nuestra aplicación. Para hacer esto, abra una terminal y navegue hasta el directorio raíz de su proyecto. Luego, ejecuta el siguiente comando:

```
$ docker build -t spring-boot-app .
```

Este comando creará una imagen de Docker para nuestra aplicación y la etiquetará con el nombre `spring-boot-app`.

Una vez construida la imagen, podemos ejecutarla usando el siguiente comando:

```
$ docker run -p 8080:8080 spring-boot-app
```

Este comando iniciará un contenedor Docker para nuestra imagen y asignará el puerto `8080` en la máquina host al puerto `8080` en el contenedor.

Ahora, podemos acceder a nuestra aplicación en `http://localhost:8080`.

## Implementación de una aplicación Spring Boot con Docker

Implementar una aplicación Spring Boot con Docker es tan simple como desarrollar una. Todo lo que necesitamos es un Dockerfile y un archivo docker-compose.yml.

Un archivo docker-compose.yml es un archivo YAML que contiene toda la configuración necesaria para docker-compose, una herramienta que se puede usar para administrar aplicaciones de varios contenedores.

Para crear un archivo docker-compose.yml, cree un nuevo archivo llamado `docker-compose.yml` en el directorio raíz de su proyecto. Luego, agregue las siguientes líneas al archivo:

```
version: '2'

services:
  app:
    build: .
    ports:
      - "8080:8080"
```

La primera línea, `version: '2'`, le dice a docker-compose que use la versión 2 del formato de archivo de docker-compose.

La segunda línea, `services:`, le dice a docker-compose que vamos a definir un servicio. Un servicio es un contenedor que forma parte de una aplicación de varios contenedores.

La tercera línea, `app:`, es el nombre de nuestro servicio.

La cuarta línea, `build: .`, le dice a docker-compose que construya nuestro servicio usando el `Dockerfile` en el directorio actual (`./`).

La quinta y última línea, `ports: - "8080:8080"`, le dice a docker-compose que asigne el puerto `8080` en la máquina host al puerto `8080` en el contenedor.

Ahora que tenemos un archivo docker-compose.yml, podemos implementar nuestra aplicación usando el siguiente comando:

```
$ docker-compose up
```

Este comando iniciará nuestra aplicación en el puerto `8080`.

## Conclusión

En esta publicación, hemos visto cómo usar Docker para desarrollar e implementar una aplicación Spring Boot. Docker puede simplificar enormemente el proceso de desarrollo e implementación de aplicaciones Spring Boot.