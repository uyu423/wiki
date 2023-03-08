---
title: Spring Boot Initializer para la creación de proyectos
description: 
published: true
date: 2023-02-07T21:32:33.417Z
tags: 
editor: markdown
dateCreated: 2023-02-07T21:32:31.782Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Initializer for Project Creation***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-initializer-for-project-creation)
{.links-list}


# Spring Boot Initializer para la creación de proyectos

Desarrollar un nuevo proyecto puede llevar mucho tiempo, especialmente cuando se empieza desde cero. Spring Boot facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción que puede "simplemente ejecutar". Proporciona un sistema de compilación flexible y un servidor de aplicaciones que se pueden configurar fácilmente.

En este artículo, le mostraremos cómo usar Spring Boot Initializr para crear un nuevo proyecto Spring Boot. Spring Boot Initializr es una aplicación web que puede generar un proyecto Spring Boot. Proporciona opciones para seleccionar las dependencias que necesita para el proyecto.

## ¿Qué es Spring Boot Initializr?

Spring Boot Initializr es una aplicación web que puede generar un proyecto Spring Boot. Proporciona opciones para seleccionar las dependencias que necesita para el proyecto.

El proyecto generado incluye las dependencias seleccionadas y se puede compilar con la herramienta de compilación Gradle o Maven. También incluye los archivos de configuración necesarios para el servidor de aplicaciones (si lo hay) y la herramienta de compilación.

## ¿Cómo usar Spring Boot Initializr?

Para usar Spring Boot Initializr, debe acceder a la aplicación web Initializr. Puede hacerlo visitando el sitio web de Spring Boot Initializr: https://start.spring.io/

![Inicializar arranque de resorte](https://i.imgur.com/HLgHZzg.png)

En el sitio web de Initializr, puede seleccionar las dependencias que necesita para el proyecto. Por ejemplo, si necesita usar JPA para acceder a la base de datos, puede seleccionar la dependencia "JPA".

![Dependencias de Spring Boot Initializr](https://i.imgur.com/pz4UHfz.png)

Después de seleccionar las dependencias, puede generar el proyecto. El proyecto se generará como un archivo ZIP.

## ¿Cómo crear un proyecto Spring Boot?

Ahora que hemos visto cómo usar Spring Boot Initializr, creemos un proyecto Spring Boot.

Usaremos el sitio web de Initializr para generar un proyecto Spring Boot con las siguientes dependencias:

- Internet
- JPA
- mysql

![Dependencias de Spring Boot Initializr](https://i.imgur.com/pz4UHfz.png)

Después de seleccionar las dependencias, podemos generar el proyecto. El proyecto se generará como un archivo ZIP.

## ¿Cómo importar el proyecto a Eclipse?

Ahora que hemos generado el proyecto, vamos a importarlo a Eclipse.

En Eclipse, seleccione Archivo -> Importar -> Proyectos Maven existentes.

![Importar proyecto Maven a Eclipse](https://i.imgur.com/Vywzo8I.png)

En el cuadro de diálogo "Importar proyecto Maven", seleccione el proyecto "spring-boot-mysql-example" que acabamos de generar.

![Importar proyecto Maven](https://i.imgur.com/pz4UHfz.png)

Haga clic en "Finalizar" para importar el proyecto.

El proyecto se importará a Eclipse.

## ¿Cómo ejecutar el proyecto?

Ahora que hemos importado el proyecto, vamos a ejecutarlo.

Haga clic derecho en el proyecto y seleccione "Ejecutar como -> Aplicación Java".

![Ejecutar aplicación Java](https://i.imgur.com/7lFWoqo.png)

En el cuadro de diálogo "Aplicación Java", seleccione la clase "Aplicación" y haga clic en "Aceptar".

![Aplicación Java](https://i.imgur.com/pz4UHfz.png)

El proyecto se ejecutará en el servidor Tomcat integrado.

Puede acceder a la aplicación en http://localhost:8080/.

## Conclusión

En este artículo, le mostramos cómo usar Spring Boot Initializr para crear un nuevo proyecto Spring Boot. Spring Boot Initializr es una aplicación web que puede generar un proyecto Spring Boot. Proporciona opciones para seleccionar las dependencias que necesita para el proyecto.