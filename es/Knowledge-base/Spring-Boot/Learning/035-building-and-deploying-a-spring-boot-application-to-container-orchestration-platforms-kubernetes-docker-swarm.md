---
title: 035: Creación e implementación de una aplicación Spring Boot en plataformas de orquestación de contenedores (Kubernetes, Docker Swarm)
description: 
published: true
date: 2023-02-04T03:32:43.466Z
tags: 
editor: markdown
dateCreated: 2023-02-04T03:32:38.114Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [035: Building and deploying a Spring Boot application to container orchestration platforms (Kubernetes, Docker Swarm)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/035-building-and-deploying-a-spring-boot-application-to-container-orchestration-platforms-kubernetes-docker-swarm)
{.links-list}


# 035: Construcción e implementación de una aplicación Spring Boot para plataformas de orquestación de contenedores (Kubernetes, Docker Swarm)

Spring Boot es un marco popular basado en Java que se utiliza para desarrollar microservicios. En esta publicación, aprenderemos cómo contener una aplicación Spring Boot e implementarla en Kubernetes y Docker Swarm.

## Contenerización de una aplicación Spring Boot

Para contenerizar una aplicación Spring Boot, primero necesitaremos crear un `Dockerfile`. Un `Dockerfile` es un archivo de texto que contiene instrucciones para crear una imagen de Docker.

Comenzaremos creando un `Dockerfile` en el directorio raíz de nuestro proyecto Spring Boot.

```
FROM openjdk:8-jdk-alpine
VOLUME /tmp
ARG JAR_FILE
COPY ${JAR_FILE} app.jar
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-jar","/app.jar"]
```

En este `Dockerfile`, usamos `openjdk:8-jdk-alpine` como nuestra imagen base. También estamos usando un `VOLUMEN` para crear un punto de montaje para almacenar archivos temporales.

A continuación, copiaremos nuestro archivo `.jar` de Spring Boot en el contenedor como `app.jar` y lo configuraremos como `ENTRYPOINT`.

Ahora que tenemos nuestro `Dockerfile`, podemos construir nuestra imagen de Docker. Usaremos el comando `docker build` para construir nuestra imagen, etiquetándola con la etiqueta `latest`.

```
$ docker build -t my-spring-boot-app:latest .
```

## Implementación en Kubernetes

Kubernetes es una popular plataforma de orquestación de contenedores. Se puede utilizar para gestionar un grupo de contenedores como una sola unidad.

Para implementar nuestra aplicación Spring Boot en Kubernetes, primero debemos crear una "Implementación". Una 'Implementación' define un grupo de pods idénticos y garantiza que una cierta cantidad de ellos siempre se esté ejecutando.

Crearemos un archivo `deployment.yaml` en el directorio raíz de nuestro proyecto.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-spring-boot-app
  labels:
    app: my-spring-boot-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-spring-boot-app
  template:
    metadata:
      labels:
        app: my-spring-boot-app
    spec:
      containers:
      - name: my-spring-boot-app
        image: my-spring-boot-app:latest
        ports:
        - containerPort: 8080
```

En este archivo, definimos una 'Implementación' con un recuento de réplicas de 3. También definimos un 'selector' y una 'plantilla' que especifican los pods que administrará la 'Implementación'.

Ahora, podemos crear nuestra `Implementación` en Kubernetes utilizando la herramienta de línea de comandos `kubectl`.

```
$ kubectl apply -f deployment.yaml
```

## Implementación en Docker Swarm

Docker Swarm es una plataforma de orquestación de contenedores de Docker. Se puede usar para administrar un grupo de contenedores Docker como una sola unidad.

Para implementar nuestra aplicación Spring Boot en Docker Swarm, primero debemos crear una `Stack`. Una 'Pila' es un grupo de servicios que se implementan juntos.

Crearemos un archivo `stack.yaml` en el directorio raíz de nuestro proyecto.

```yaml
version: "3.1"

services:

  my-spring-boot-app:
    image: my-spring-boot-app:latest
    ports:
      - "8080:8080"
    deploy:
      replicas: 3
```

En este archivo, hemos definido una `Pila` con un solo servicio, `my-spring-boot-app`. También hemos especificado que queremos que se implementen 3 réplicas de este servicio.

Ahora, podemos implementar nuestra `Stack` en Docker Swarm usando el comando `docker stack`.

```
$ docker stack deploy -c stack.yaml my-spring-boot-app
```

## Información adicional

- Si está utilizando Kubernetes, también puede crear un `Servicio` para exponer su aplicación al mundo exterior.
- Si está utilizando Docker Swarm, también puede crear una "Red" para permitir la comunicación entre sus servicios.

## Recursos para leer más

- [Documentación de referencia de Spring Boot - Contenedorización de aplicaciones de Spring Boot](https://docs.spring.io/spring-boot/docs/current/reference/html/deploying-spring-boot.html# deploying-spring-boot-containerizing )
- [Documentación de Kubernetes - Creación de una implementación](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/# creating-a-deployment)
- [Documentación de Docker: implementar una pila en un enjambre] (https://docs.docker.com/engine/reference/commandline/stack_deploy/# deploy-a-stack-to-a-swarm)