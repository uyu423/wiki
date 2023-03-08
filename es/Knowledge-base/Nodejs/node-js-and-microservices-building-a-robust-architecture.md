---
title: Node.js y Microservicios: Construyendo una Arquitectura Robusta
description: 
published: true
date: 2023-02-15T06:55:44.729Z
tags: 
editor: markdown
dateCreated: 2023-02-15T06:55:43.122Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Node.js and Microservices: Building a Robust Architecture***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-microservices-building-a-robust-architecture)
{.links-list}


# Node.js y Microservicios: Construyendo una Arquitectura Robusta

En la era de la computación en la nube, existe una creciente necesidad de aplicaciones que puedan implementarse en múltiples servidores. Aquí es donde entran los microservicios. Los microservicios son una forma de crear aplicaciones como un conjunto de servicios pequeños e independientes que se pueden implementar y escalar de forma independiente.

Node.js es una plataforma popular para crear microservicios. Es liviano y eficiente, y tiene un gran ecosistema de bibliotecas y herramientas.

En este artículo, veremos cómo crear una arquitectura de microservicios con Node.js. Comenzaremos con una aplicación monolítica simple y la dividiremos en un conjunto de microservicios. Luego veremos cómo implementar y escalar nuestros microservicios.

## Monolítico vs Microservicios

Antes de sumergirnos en Node.js y los microservicios, demos un paso atrás y entendamos la diferencia entre arquitecturas monolíticas y de microservicios.

Una aplicación monolítica es aquella que se construye como una sola unidad grande. Todos los componentes de la aplicación están estrechamente acoplados y dependen unos de otros. Las aplicaciones monolíticas normalmente se implementan como un solo proceso en un solo servidor.

Una arquitectura de microservicios es aquella en la que la aplicación se construye como un conjunto de pequeños servicios independientes. Estos servicios están débilmente acoplados y se pueden implementar y escalar de forma independiente. Los microservicios generalmente se implementan como un conjunto de procesos pequeños y aislados en un conjunto de servidores.

Hay algunos beneficios clave de usar una arquitectura de microservicios:

* **Escalabilidad**: los microservicios se pueden implementar y escalar de forma independiente, por lo que es fácil escalar partes específicas de la aplicación según sea necesario.

* **Aislamiento**: cada microservicio se ejecuta en su propio proceso, por lo que si un microservicio falla, no afecta a los demás.

* **Flexibilidad**: los microservicios se pueden escribir en diferentes lenguajes de programación e implementarse en diferentes servidores, para que pueda elegir la herramienta adecuada para el trabajo.

## Rompiendo el monolito

Ahora que hemos visto los beneficios de los microservicios, veamos cómo dividir una aplicación monolítica en un conjunto de microservicios.

Nuestra aplicación monolítica de ejemplo es una simple lista de tareas pendientes. Tiene una interfaz de usuario para crear y administrar tareas pendientes y un backend para almacenar los datos. El backend es una base de datos relacional simple.

El primer paso es identificar los diferentes componentes de la aplicación. En nuestro ejemplo de lista de tareas pendientes, tenemos algunos componentes obvios:

* La interfaz de usuario
* La base de datos de back-end
* Los datos de la lista de tareas pendientes

Podemos desglosar aún más estos componentes en servicios más pequeños. Por ejemplo, la interfaz de usuario se puede dividir en un servicio de front-end que maneja HTML y CSS, y un servicio de back-end que maneja los datos.

La base de datos back-end se puede dividir en un servicio de base de datos que maneja los datos y un servicio de almacenamiento que maneja los archivos.

Y los datos de la lista de tareas pendientes se pueden dividir en un servicio de tareas que maneja los elementos de tareas pendientes y un servicio de usuario que maneja los datos del usuario.

Ahora tenemos un conjunto de servicios pequeños e independientes que podemos implementar y escalar de forma independiente.

## Implementación de microservicios

Ahora que tenemos nuestros microservicios, veamos cómo implementarlos.

Hay algunas formas diferentes de implementar microservicios. Lo más habitual es utilizar un orquestador de contenedores, como Docker Swarm o Kubernetes.

Otra opción es utilizar una plataforma sin servidor, como AWS Lambda o Azure Functions. Las plataformas sin servidor son una buena opción para los microservicios que no tienen mucho tráfico o que solo se necesitan ocasionalmente.

En nuestro ejemplo de lista de tareas pendientes, implementaremos nuestros microservicios mediante Docker Swarm. Crearemos un archivo docker-compose.yml que define nuestros servicios:

```yaml
version: "3"

services:
  frontend:
    image: frontend:latest
    ports:
      - "80:80"
    deploy:
      replicas: 2
      update_config:
        parallelism: 2
        delay: 10s
  backend:
    image: backend:latest
    ports:
      - "8080:8080"
    deploy:
      replicas: 2
      update_config:
        parallelism: 2
        delay: 10s
  database:
    image: database:latest
    ports:
      - "3306:3306"
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
  storage:
    image: storage:latest
    ports:
      - "9000:9000"
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
  task:
    image: task:latest
    ports:
      - "8081:8081"
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
  user:
    image: user:latest
    ports:
      - "8082:8082"
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
```

Luego podemos implementar nuestros servicios usando el siguiente comando:

```
$ docker stack deploy -c docker-compose.yml todo
```

## Microservicios escalables

Una vez que se implementan nuestros microservicios, podemos ampliarlos o reducirlos según sea necesario. Por ejemplo, podemos escalar el servicio frontend de dos réplicas a cuatro réplicas:

```
$ docker service scale todo_frontend=4
```

También podemos escalar el servicio de back-end a una réplica:

```
$ docker service scale todo_backend=1
```

## Conclusión

En este artículo, analizamos cómo crear una arquitectura de microservicios con Node.js. Hemos visto cómo dividir una aplicación monolítica en un conjunto de servicios pequeños e independientes y cómo implementar y escalar estos servicios.

Si bien los microservicios ofrecen muchos beneficios, también presentan algunos desafíos. Por ejemplo, administrar un conjunto de servicios pequeños e independientes puede ser complejo. Y la comunicación entre servicios puede agregar latencia a la aplicación.

A pesar de estos desafíos, los microservicios son una forma poderosa de crear aplicaciones escalables y resistentes. Y Node.js es una gran plataforma para crear microservicios.