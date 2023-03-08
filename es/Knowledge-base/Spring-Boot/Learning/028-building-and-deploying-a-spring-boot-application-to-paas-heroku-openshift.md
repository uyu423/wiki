---
title: 028: Creación e implementación de una aplicación Spring Boot para PaaS (Heroku, OpenShift)
description: 
published: true
date: 2023-02-03T20:32:44.244Z
tags: 
editor: markdown
dateCreated: 2023-02-03T20:32:39.159Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [028: Building and deploying a Spring Boot application to PaaS (Heroku, OpenShift)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/028-building-and-deploying-a-spring-boot-application-to-paas-heroku-openshift)
{.links-list}


# 028: Construcción e implementación de una aplicación Spring Boot para PaaS (Heroku, OpenShift)

En esta publicación, aprenderemos cómo crear e implementar una aplicación Spring Boot en un proveedor de plataforma como servicio (PaaS). En particular, nos centraremos en dos proveedores populares de PaaS, Heroku y OpenShift.

Crear e implementar aplicaciones Spring Boot para proveedores de PaaS es una excelente manera de poner en marcha su aplicación rápidamente. Los proveedores de PaaS manejan toda la infraestructura y la configuración de implementación por usted, para que pueda concentrarse en desarrollar su aplicación.

## Requisitos previos

Antes de comenzar, hay algunas cosas que necesitará:

* Una cuenta PaaS. Puede registrarse para obtener una cuenta gratuita de Heroku en [heroku.com](https://www.heroku.com/). Para OpenShift, puede registrarse para obtener una cuenta gratuita en [openshift.com](https://www.openshift.com/).
* Un editor de texto o IDE. Usaremos [Visual Studio Code](https://code.visualstudio.com/) en esta publicación, pero puede usar cualquier editor que desee.
* [JDK 8](https://adoptopenjdk.net/) o posterior.
* [Maven](https://maven.apache.org/) 3.3.9 o posterior.

## Creando una aplicación Spring Boot

Comencemos por crear una aplicación Spring Boot simple. Usaremos [Spring Initializr](https://start.spring.io/) para generar el proyecto.

Vaya a [Spring Initializr](https://start.spring.io/) y seleccione las siguientes opciones:

* Generar un `Proyecto Maven`
* Usar `Java 8`
* Usar `Spring Boot 2.2.2`
* Envase: `Tarro`
* Tipo: `Web`
* Artefacto: `demostración`

Haga clic en 'Generar proyecto' y se descargará un archivo 'demo.zip'. Extraiga el contenido del archivo zip en un directorio de su computadora.

Abra el proyecto en Visual Studio Code y debería ver la siguiente estructura del proyecto:

```
demo
├── pom.xml
└── src
    └── main
        ├── java
        │   └── com
        │       └── example
        │           └── demo
        │               └── DemoApplication.java
        └── resources
            └── application.properties
```

El archivo `pom.xml` es el archivo de configuración del proyecto Maven. El directorio `src/main/java` contiene el código fuente de Java para la aplicación. El directorio `src/main/resources` contiene archivos de configuración de la aplicación.

Abra el archivo `DemoApplication.java` y agregue el siguiente `@RestController`:

```java
package com.example.demo;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class DemoApplication {

    @GetMapping("/")
    public String home() {
        return "Hello, world!";
    }

}
```

Este `@RestController` expone un extremo `/` que devuelve la cadena `¡Hola, mundo!`.

## Ejecutando la aplicación localmente

Ejecutemos la aplicación localmente para asegurarnos de que funciona. En la terminal, navegue hasta el directorio `demo` y ejecute el siguiente comando:

```
mvn spring-boot:run
```

Esto iniciará la aplicación en su máquina local. Puede acceder a la aplicación en [http://localhost:8080](http://localhost:8080). Deberías ver la cadena `¡Hola, mundo!`.

## Implementación de la aplicación en Heroku

Ahora que tenemos una aplicación que funciona, implementémosla en Heroku.

Heroku usa [Git](https://git-scm.com/) para la implementación, por lo que lo primero que debemos hacer es inicializar un repositorio de Git en el directorio `demo`. En la terminal, ejecute los siguientes comandos:

```
git init
git add .
git commit -m "Initial commit"
```

Esto inicializará un repositorio de Git y realizará la confirmación inicial.

A continuación, necesitamos crear una aplicación Heroku. En la terminal, ejecute el siguiente comando:

```
heroku create
```

Esto creará una nueva aplicación Heroku y agregará un control remoto a su repositorio Git.

Ahora podemos implementar la aplicación en Heroku. En la terminal, ejecute el siguiente comando:

```
git push heroku master
```

Esto enviará el código al control remoto de Heroku y activará una implementación.

Una vez completada la implementación, puede ver la aplicación en la URL proporcionada por Heroku. Deberías ver la cadena `¡Hola, mundo!`.

## Implementación de la aplicación en OpenShift

OpenShift usa [Git](https://git-scm.com/) para la implementación, por lo que lo primero que debemos hacer es inicializar un repositorio de Git en el directorio `demo`. En la terminal, ejecute los siguientes comandos:

```
git init
git add .
git commit -m "Initial commit"
```

Esto inicializará un repositorio de Git y realizará la confirmación inicial.

A continuación, debemos crear un nuevo proyecto OpenShift. Un proyecto OpenShift es una agrupación lógica de recursos. Usaremos la consola web de OpenShift para crear el proyecto.

Inicie sesión en la [consola web de OpenShift](https://console.openshift.com/) y haga clic en `Crear proyecto`. Introduzca `demo` para el nombre del proyecto y haga clic en `Crear`.

Una vez que se ha creado el proyecto, podemos implementar la aplicación en OpenShift. En la terminal, ejecute el siguiente comando:

```
git push openshift master
```

Esto enviará el código al control remoto de OpenShift y activará una implementación.

Una vez completada la implementación, puede ver la aplicación en la URL proporcionada por OpenShift. Deberías ver la cadena `¡Hola, mundo!`.