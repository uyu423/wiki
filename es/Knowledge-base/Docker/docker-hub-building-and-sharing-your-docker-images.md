---
title: Docker Hub: crear y compartir sus imágenes de Docker
description: 
published: true
date: 2023-02-14T01:17:24.381Z
tags: 
editor: markdown
dateCreated: 2023-02-14T01:17:17.201Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Docker Hub: Building and Sharing Your Docker Images***English** document is available*](/en/Knowledge-base/Docker/docker-hub-building-and-sharing-your-docker-images)
{.links-list}


# Docker Hub: creación y uso compartido de sus imágenes de Docker

Docker Hub es un servicio de registro basado en la nube para crear y compartir imágenes de Docker. Con Docker Hub, puede compilar, probar e implementar sus aplicaciones con facilidad.

Docker Hub ofrece un plan gratuito y un plan profesional de pago. Con el plan gratuito, puede crear repositorios públicos ilimitados, pero está limitado a un repositorio privado. Con el plan Pro, puede crear un número ilimitado de repositorios públicos y privados.

Hay dos formas de enviar imágenes a Docker Hub:

1. El comando **docker push**

2. La **interfaz web de Docker Hub**

## El comando de inserción de la ventana acoplable

El comando **docker push** inserta imágenes en un registro de Docker. Un registro de Docker es un host que almacena y entrega imágenes.

El comando **docker push** requiere que especifique el nombre de la imagen y la etiqueta. Por ejemplo, para enviar una imagen con la etiqueta "más reciente" a Docker Hub, usaría el siguiente comando:

```
docker push <username>/<image>:<tag>
```

Reemplace <username> con su nombre de usuario de Docker Hub, <image> con el nombre de la imagen y <tag> con la etiqueta.

## La interfaz web de Docker Hub

La interfaz web de Docker Hub es una aplicación basada en web que puede usar para insertar, extraer y administrar sus imágenes de Docker.

Para enviar una imagen a Docker Hub mediante la interfaz web, primero inicie sesión en su cuenta de Docker Hub. Luego, haga clic en el botón **Crear repositorio**.

Ingrese el nombre del repositorio y una descripción, luego haga clic en el botón **Crear**.

A continuación, haga clic en el botón **Subir archivo**.

Seleccione la imagen que desea cargar, luego haga clic en el botón **Cargar**.

Finalmente, haga clic en el botón **Publicar**.

Su imagen ahora se envía a su repositorio en Docker Hub.

## Conclusión

Docker Hub es una excelente manera de compartir sus imágenes de Docker con el mundo. Con Docker Hub, puede compilar, probar e implementar sus aplicaciones con facilidad.