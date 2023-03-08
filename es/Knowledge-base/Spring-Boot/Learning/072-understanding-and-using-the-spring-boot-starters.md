---
title: 072: Comprensión y uso de los arrancadores Spring Boot
description: 
published: true
date: 2023-02-05T05:32:15.539Z
tags: 
editor: markdown
dateCreated: 2023-02-05T05:32:13.935Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [072: Understanding and Using the Spring Boot Starters***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/072-understanding-and-using-the-spring-boot-starters)
{.links-list}


# 072: Comprensión y uso de los arrancadores Spring Boot

Spring Boot Starters es un conjunto de descriptores de dependencia convenientes que se pueden incluir en su aplicación. Al incluir uno de estos en su proyecto, obtiene un conjunto de dependencias bien configuradas y listas para usar que puede usar para poner en marcha su proyecto de forma rápida y sencilla.

En esta publicación, veremos qué son los Spring Boot Starters, cómo funcionan y cómo puede usarlos en sus propios proyectos.

## ¿Qué son los Spring Boot Starters?

Spring Boot Starters es un conjunto de descriptores de dependencia que se pueden incluir en su proyecto. Estos descriptores definen un conjunto de dependencias bien configuradas y listas para usar que se pueden usar para poner en marcha su proyecto de forma rápida y sencilla.

Los Spring Boot Starters se dividen en dos grupos: Core Starters y Web Starters. Los Core Starters son las dependencias que se requieren para cualquier aplicación Spring Boot. Los Web Starters son las dependencias que se requieren para cualquier aplicación Spring Boot que exponga una interfaz web.

## ¿Cómo funcionan los Spring Boot Starters?

Spring Boot Starters funciona proporcionando un conjunto de dependencias bien configuradas y listas para usar. Estas dependencias se pueden utilizar para poner en marcha su proyecto de forma rápida y sencilla.

Incluir un Spring Boot Starter en su proyecto incluirá automáticamente cualquier dependencia que requiera ese Starter. Por ejemplo, incluir el iniciador `spring-boot-starter-web` en su proyecto incluirá automáticamente el iniciador `spring-boot-starter-tomcat`, ya que el iniciador `spring-boot-starter-web` depende del `spring -boot-starter-tomcat` Arrancador.

## ¿Cómo puedo usar Spring Boot Starters en mi propio proyecto?

Incluir un Spring Boot Starter en su propio proyecto es fácil. Simplemente agregue la dependencia adecuada al archivo `pom.xml` de su proyecto.

Por ejemplo, para incluir el iniciador `spring-boot-starter-web` en su proyecto, agregaría la siguiente dependencia a su archivo `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

## Conclusión

En esta publicación, hemos analizado qué son los Spring Boot Starters, cómo funcionan y cómo puede usarlos en sus propios proyectos.