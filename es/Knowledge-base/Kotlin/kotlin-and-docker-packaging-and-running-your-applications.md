---
title: Kotlin y Docker: empaquetado y ejecución de sus aplicaciones
description: 
published: true
date: 2023-02-12T00:17:30.998Z
tags: 
editor: markdown
dateCreated: 2023-02-12T00:17:29.381Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Kotlin and Docker: Packaging and Running Your Applications***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-docker-packaging-and-running-your-applications)
{.links-list}


# Kotlin y Docker: empaquetado y ejecución de sus aplicaciones

Kotlin es un lenguaje compatible con JVM que ha ganado popularidad en los últimos años por su sintaxis concisa e interoperabilidad con Java. Docker es una plataforma de creación de contenedores que permite a los desarrolladores empaquetar y ejecutar aplicaciones en entornos aislados.

En este artículo, mostraremos cómo empaquetar una aplicación Kotlin en un contenedor Docker y ejecutarla en un servidor. También discutiremos brevemente algunos de los beneficios de usar Kotlin y Docker juntos.

## Empaquetado de una aplicación Kotlin en un contenedor Docker

Para empaquetar una aplicación Kotlin en un contenedor Docker, necesitamos crear un `Dockerfile` que especifique la imagen base y las dependencias necesarias. Usaremos la imagen `openjdk:8-jdk-alpine` como nuestra imagen base. Esta imagen contiene OpenJDK 8 JVM y la distribución Alpine Linux. Alpine Linux es una distribución ligera de Linux que es ideal para contenedores Docker.

También necesitaremos especificar la dependencia `kotlin-stdlib`. Esta dependencia contiene la biblioteca estándar de Kotlin, que es necesaria para todas las aplicaciones de Kotlin.

```Dockerfile
FROM openjdk:8-jdk-alpine

# Add the Kotlin standard library as a dependency
RUN apk add --no-cache kotlin-stdlib
```

A continuación, debemos copiar nuestro código Kotlin en el contenedor. Colocaremos nuestro código en el directorio `/app`.

```Dockerfile
# Copy our Kotlin code into the container
COPY src/ /app/src/
```

Finalmente, necesitamos especificar los valores `ENTRYPOINT` y `CMD`. El valor `ENTRYPOINT` especifica el comando que se ejecutará cuando se inicie el contenedor. El valor `CMD` especifica los argumentos que se pasarán al comando `ENTRYPOINT`. En nuestro caso, usaremos el comando `kotlinc` para compilar nuestro código y el comando `java` para ejecutar nuestro código compilado.

```Dockerfile
# Specify the entrypoint and command
ENTRYPOINT ["kotlinc", "-include-runtime", "/app/src/main.kt", "-d", "/app/app.jar"]
CMD ["java", "-jar", "/app/app.jar"]
```

El argumento `-include-runtime` le dice al compilador `kotlinc` que incluya el tiempo de ejecución de Kotlin en el código compilado. Esto es necesario porque el tiempo de ejecución de Kotlin no está incluido en la dependencia `kotlin-stdlib`.

## Ejecutar una aplicación Kotlin en un contenedor Docker

Ahora que tenemos nuestro `Dockerfile`, podemos construir nuestra imagen Docker y ejecutar nuestra aplicación Kotlin en un contenedor Docker.

Primero, necesitamos construir nuestra imagen de Docker. Usaremos el comando `docker build` para construir nuestra imagen. Nombraremos nuestra imagen `kotlin-app` y la etiquetaremos con la etiqueta `latest`.

```console
$ docker build -t kotlin-app:latest .
```

A continuación, necesitamos ejecutar nuestra imagen de Docker. Usaremos el comando `docker run` para ejecutar nuestra imagen. También especificaremos el argumento `-p 8080:8080`, que asignará el puerto `8080` en el host al puerto `8080` en el contenedor.

```console
$ docker run -p 8080:8080 kotlin-app:latest
```

Nuestra aplicación Kotlin ahora se ejecuta en un contenedor Docker y se puede acceder a ella en `http://localhost:8080`.

## Beneficios de usar Kotlin y Docker juntos

Hay varios beneficios al usar Kotlin y Docker juntos.

Primero, Kotlin es un lenguaje muy conciso. Esto significa que nuestro código Kotlin será mucho más pequeño que el código Java equivalente. Esto es importante cuando se empaquetan aplicaciones en contenedores Docker porque las imágenes más pequeñas son más rápidas de construir e implementar.

En segundo lugar, Kotlin es totalmente interoperable con Java. Esto significa que podemos usar fácilmente las bibliotecas Java existentes en nuestro código Kotlin. Esto es importante al contener aplicaciones Java existentes con Docker.

En tercer lugar, Kotlin es un lenguaje compatible con JVM. Esto significa que podemos ejecutar nuestro código Kotlin en cualquier plataforma que admita JVM. Esto es importante al implementar aplicaciones en contenedores Docker porque podemos ejecutar nuestros contenedores en cualquier plataforma que admita Docker, independientemente del sistema operativo subyacente.

## Conclusión

En este artículo, mostramos cómo empaquetar una aplicación Kotlin en un contenedor Docker y ejecutarla en un servidor. También discutimos brevemente algunos de los beneficios de usar Kotlin y Docker juntos.