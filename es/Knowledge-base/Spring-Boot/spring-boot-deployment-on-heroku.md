---
title: Implementación de Spring Boot en Heroku
description: 
published: true
date: 2023-02-07T12:32:31.884Z
tags: 
editor: markdown
dateCreated: 2023-02-07T12:32:29.660Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Deployment on Heroku***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-deployment-on-heroku)
{.links-list}


# Implementación de Spring Boot en Heroku

Heroku es una plataforma en la nube como servicio (PaaS) que admite varios lenguajes de programación. Uno de estos lenguajes es Java. En este artículo, discutiremos cómo implementar una aplicación Spring Boot en Heroku.

## ¿Qué es Spring Boot?

Spring Boot es un marco basado en Java que se utiliza para crear microservicios. Está desarrollado por Pivotal Team y es un proyecto gratuito y de código abierto.

## ¿Qué es Heroku?

Heroku es una plataforma en la nube como servicio (PaaS) que admite varios lenguajes de programación.

Heroku es una plataforma como servicio (PaaS) que permite a los desarrolladores implementar, administrar y escalar sus aplicaciones. Heroku es simple y fácil de usar y ofrece un plan gratuito para aplicaciones pequeñas.

## Requisitos previos

Antes de comenzar, necesitará lo siguiente:

- Una cuenta de Heroku
- Un editor de texto
-JDK 8 o superior
- Maven 3.3.9 o superior

## Creación de una aplicación Spring Boot

Primero, deberá crear una aplicación Spring Boot. Puede hacer esto usando Spring Initializr.

Spring Initializr es una aplicación web que le permite crear una aplicación Spring Boot. Generará una estructura de proyecto para usted y agregará las dependencias requeridas.

Para crear una aplicación Spring Boot, vaya a https://start.spring.io/ y seleccione lo siguiente:

- Idioma: Java
- Versión de arranque de primavera: 2.4.4
- Proyecto: Proyecto Maven
- Envase: Tarro
- Versión Java: 8
- Grupo: com.heroku
- Artefacto: demostración

Haga clic en Generar proyecto para descargar el proyecto.

## Crear un perfil

Procfile es un archivo de texto que contiene los comandos que ejecuta la aplicación al iniciarse. El Procfile debe colocarse en el directorio raíz de su aplicación.

Cree un archivo llamado Procfile (sin ninguna extensión) y agréguele la siguiente línea.

    web: java -jar target/demo-0.0.1-SNAPSHOT.jar

## Creación de una aplicación Heroku

Una vez que haya creado el Procfile, puede crear una aplicación Heroku.

Inicie sesión en su cuenta de Heroku y haga clic en Nuevo -> Crear nueva aplicación.

Ingrese la siguiente informacion:

- Nombre de la aplicación: demostración
- Región: Europa

Haga clic en Crear aplicación.

## Implementación de la aplicación en Heroku

Una vez que se crea la aplicación, puede implementar la aplicación Spring Boot en Heroku.

Heroku usa Git para la implementación, por lo que deberá enviar su código a un repositorio de Heroku Git.

Primero, deberá agregar el repositorio Heroku Git como un control remoto a su repositorio local. Para hacer esto, ejecute el siguiente comando:

    $ heroku git:remoto -una demostración

Luego, puede enviar su código al repositorio de Heroku Git usando el siguiente comando:

    $ git empujar heroku maestro

Una vez que se envía el código, Heroku compilará e implementará la aplicación.

Puede ver los registros con el siguiente comando:

    $ registros de heroku --tail

## Conclusión

En este artículo, hemos discutido cómo implementar una aplicación Spring Boot en Heroku.