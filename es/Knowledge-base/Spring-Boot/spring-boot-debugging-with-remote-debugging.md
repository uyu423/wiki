---
title: Depuración de Spring Boot con depuración remota
description: 
published: true
date: 2023-02-02T20:57:31.800Z
tags: 
editor: markdown
dateCreated: 2023-02-02T20:57:27.236Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Debugging with Remote Debugging***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-debugging-with-remote-debugging)
{.links-list}


# Introducción

Los desarrolladores a menudo necesitan depurar su código para encontrar y corregir errores. Las aplicaciones Spring Boot se pueden depurar de varias maneras, incluido el uso de un depurador remoto. En este artículo, exploraremos cómo depurar aplicaciones Spring Boot usando un depurador remoto.

# ¿Qué es la depuración remota?

La depuración remota es un proceso que permite a un desarrollador depurar un programa que se ejecuta en una máquina remota. Para hacer esto, el desarrollador debe tener acceso a la máquina remota y poder conectarse a ella mediante un depurador.

# Cómo depurar una aplicación Spring Boot usando un depurador remoto

Hay algunos pasos que deben seguirse para depurar una aplicación Spring Boot usando un depurador remoto. Veremos cada uno de estos pasos en detalle.

## 1. Asegúrese de que la aplicación se esté ejecutando en modo de depuración

El primer paso es asegurarse de que la aplicación Spring Boot se esté ejecutando en modo de depuración. Esto se puede hacer agregando la siguiente línea al archivo application.properties:

```
spring.boot.devtools.remote.debug=true
```

## 2. Inicie el depurador remoto

El siguiente paso es iniciar el depurador remoto. Esto se puede hacer ejecutando el siguiente comando:

```
java -Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8000,suspend=n -jar myapp.jar
```

Reemplace myapp.jar con el nombre de su aplicación Spring Boot.

## 3. Conectarse al depurador remoto

El paso final es conectarse al depurador remoto. Esto se puede hacer usando un depurador como Eclipse o IntelliJ. En Eclipse, vaya a la perspectiva Depurar y seleccione Aplicación Java remota. En la pestaña Conectar, seleccione el proyecto que contiene la aplicación Spring Boot. En la pestaña Conectar, seleccione el proyecto que contiene la aplicación Spring Boot. En la pestaña Conectar, seleccione el proyecto que contiene la aplicación Spring Boot. En la pestaña Conectar, seleccione el proyecto que contiene la aplicación Spring Boot. En la pestaña Conectar, seleccione el proyecto que contiene la aplicación Spring Boot.

En IntelliJ, vaya a Ejecutar > Editar configuraciones. En la pestaña Remoto, seleccione el proyecto que contiene la aplicación Spring Boot. En la pestaña Conectar, seleccione el proyecto que contiene la aplicación Spring Boot.

# Conclusión

En este artículo, hemos explorado cómo depurar una aplicación Spring Boot usando un depurador remoto. También hemos repasado los pasos que deben seguirse para hacer esto.