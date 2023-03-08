---
title: Administración de imágenes de Docker: etiquetado y envío a un registro
description: 
published: true
date: 2023-02-01T21:43:22.575Z
tags: 
editor: markdown
dateCreated: 2023-02-01T21:43:18.427Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Docker Image Management: Tagging and Pushing to a Registry***English** document is available*](/en/Knowledge-base/Docker/docker-image-management-tagging-and-pushing-to-a-registry)
{.links-list}



# Gestión de imágenes de Docker: etiquetado y envío a un registro

Las imágenes de Docker son la base para crear contenedores. De forma predeterminada, las imágenes se extraen de Docker Hub, que es un registro público administrado por Docker, Inc. Sin embargo, también puede ejecutar su propio registro e insertar imágenes en él.

Este artículo cubre dos métodos para administrar imágenes de Docker: etiquetar y enviar a un registro.

## Etiquetado de imágenes

Puede etiquetar imágenes con `docker tag`. Esto es útil para etiquetar imágenes con números de versión, por ejemplo. Para etiquetar una imagen, utilice la siguiente sintaxis:

```
docker tag <image> <tag>
```

Por ejemplo, para etiquetar la imagen `nginx` con la etiqueta `1.7.9`, ejecutaría el siguiente comando:

```
docker tag nginx 1.7.9
```

El etiquetado es importante para administrar imágenes porque le permite especificar una versión específica de una imagen cuando ejecuta un contenedor. Por defecto se utiliza la etiqueta `latest`, que corresponde a la versión más reciente de la imagen.

## Empujar imágenes a un registro

Una vez que haya etiquetado una imagen, puede enviarla a un registro. Puede usar el comando `docker push` para enviar una imagen a un registro. La sintaxis de este comando es la siguiente:

```
docker push <registry>/<repository>/<image>
```

Por ejemplo, para enviar la imagen `nginx` a Docker Hub, usaría el siguiente comando:

```
docker push nginx
```

Empujar imágenes a un registro es una forma de compartir imágenes con otros. Al enviar una imagen a un registro, la pone a disposición de otros para que la extraigan y la utilicen.

## Resumen

En este artículo, aprendió sobre dos métodos para administrar imágenes de Docker: etiquetar y enviar a un registro. Etiquetar imágenes es una forma de etiquetarlas con números de versión u otra información. Enviar imágenes a un registro es una forma de compartirlas con otros.