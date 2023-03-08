---
title: 086: Implementación de una aplicación Spring Boot en Kubernetes
description: 
published: true
date: 2023-02-05T16:32:17.668Z
tags: 
editor: markdown
dateCreated: 2023-02-05T16:32:16.110Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [086: Deploying a Spring Boot Application to Kubernetes***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/086-deploying-a-spring-boot-application-to-kubernetes)
{.links-list}


# 086: Implementación de una aplicación Spring Boot en Kubernetes

Kubernetes es un sistema de código abierto para automatizar la implementación, el escalado y la gestión de aplicaciones en contenedores.

Spring Boot es un marco Java popular para crear aplicaciones web y microservicios.

En esta publicación, le mostraremos cómo implementar una aplicación Spring Boot en Kubernetes.

## Requisitos previos

- Un clúster de Kubernetes
- Una aplicación Spring Boot

## Implementación de la aplicación

1. Cree una implementación de Kubernetes para su aplicación.

   ```
   apiVersión: apps/v1
   tipo: Despliegue
   metadatos:
     nombre: myapp-implementación
   Especificaciones:
     réplicas: 3
     selector:
       etiquetas de coincidencia:
         aplicación: mi aplicación
     plantilla:
       metadatos:
         etiquetas:
           aplicación: mi aplicación
       Especificaciones:
         contenedores:
         - nombre: myapp-contenedor
           imagen: myapp-imagen
           puertos:
           - puerto contenedor: 8080
   ```

2. Cree un servicio de Kubernetes para su aplicación.

   ```
   apiVersión: v1
   tipo: Servicio
   metadatos:
     nombre: myapp-servicio
   Especificaciones:
     tipo: equilibrador de carga
     puertos:
     - puerto: 80
       puerto de destino: 8080
     selector:
       aplicación: mi aplicación
   ```

3. Aplique la implementación y el servicio a su clúster de Kubernetes.

   ```
   kubectl apply -f myapp-deployment.yaml
   kubectl apply -f myapp-service.yaml
   ```

4. Verifique que la implementación y el servicio se estén ejecutando.

   ```
   kubectl obtener implementación
   servicio de obtención de kubectl
   ```

¡Su aplicación ahora está implementada en Kubernetes!

## Información adicional

- [Documentación de Kubernetes](https://kubernetes.io/docs/)
- [Documentación de Spring Boot] (https://spring.io/projects/spring-boot)