---
title: 069: Personalización de Spring Boot CLI para desarrollo avanzado
description: 
published: true
date: 2023-02-05T03:32:26.881Z
tags: 
editor: markdown
dateCreated: 2023-02-05T03:32:21.535Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [069: Customizing the Spring Boot CLI for Advanced Development***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/069-customizing-the-spring-boot-cli-for-advanced-development)
{.links-list}


# Personalización de Spring Boot CLI para desarrollo avanzado

Spring Boot CLI es una gran herramienta para iniciar rápidamente aplicaciones Spring. Le permite crear aplicaciones independientes basadas en Spring que se pueden ejecutar desde la línea de comandos sin necesidad de un servidor web.

En esta publicación, veremos cómo personalizar Spring Boot CLI para un desarrollo avanzado. Cubriremos cómo instalar la CLI, cómo crear y ejecutar aplicaciones Spring Boot y cómo personalizar la CLI para sus propias necesidades de desarrollo.

## Instalación de la CLI de Spring Boot

Spring Boot CLI es una herramienta de línea de comandos que se puede usar para crear y ejecutar rápidamente aplicaciones Spring Boot. Está disponible como un archivo JAR ejecutable independiente o como un paquete Homebrew.

Para instalar Spring Boot CLI, primero descargue la última versión de CLI del sitio web de Spring Boot. Luego, descomprima el archivo descargado y agregue el directorio `spring-boot-cli/bin` a su `RUTA`.

Alternativamente, si está utilizando Homebrew, puede instalar Spring Boot CLI ejecutando el siguiente comando:

```
$ brew tap pivotal/tap
$ brew install springboot
```

## Creación de una aplicación Spring Boot

Ahora que tenemos Spring Boot CLI instalado, creemos una aplicación Spring Boot simple. Comenzaremos creando un nuevo directorio para nuestro proyecto:

```
$ mkdir my-app
$ cd my-app
```

A continuación, crearemos un nuevo archivo llamado `application.properties` en nuestro directorio de proyectos. Este archivo contendrá la configuración de nuestra aplicación Spring Boot. Estableceremos la propiedad `spring.main.banner-mode` en `off` para que el banner de Spring Boot no se muestre cuando se ejecute nuestra aplicación:

```
spring.main.banner-mode=off
```

Ahora, podemos crear nuestra aplicación Spring Boot. Usaremos el comando `spring` para crear una nueva clase `@SpringBootApplication`:

```
$ spring init -n com.example.myapp -d web my-app.jar
```

Esto creará un nuevo archivo `my-app.jar` en nuestro directorio de proyectos. Podemos ejecutar nuestra aplicación ejecutando el siguiente comando:

```
$ java -jar my-app.jar
```

Nuestra aplicación se iniciará y estará accesible en `http://localhost:8080`.

## Personalización de la CLI de Spring Boot

Spring Boot CLI proporciona una serie de opciones para personalizar su comportamiento. Estas opciones se pueden especificar en la línea de comando o en el archivo de configuración `spring`.

El archivo de configuración `spring` es un archivo YAML que Spring Boot CLI lee cuando se inicia. Este archivo se puede usar para especificar opciones para el comando `spring`, como el directorio del proyecto predeterminado y el nombre del paquete predeterminado.

Para crear un archivo de configuración `spring`, cree un nuevo archivo llamado `.spring-configuration.yaml` en su directorio de inicio. Spring Boot CLI leerá el contenido de este archivo cuando se inicie.

Aquí hay un archivo de configuración `spring` de ejemplo:

```yaml
spring:
  project:
    default-project-dir: ~/projects
  package:
    default-package-name: com.example
```

Este archivo establece el directorio del proyecto predeterminado en `~/projects` y el nombre del paquete predeterminado en `com.example`.

Ahora, cuando creamos una nueva aplicación Spring Boot, el comando `spring` usará estos valores predeterminados:

```
$ spring init my-app
```

Esto creará una nueva aplicación Spring Boot en el directorio `~/projects/my-app` con un nombre de paquete `com.example`.

También podemos especificar opciones en la línea de comando `spring`. Por ejemplo, podemos usar la opción `--project-dir` para establecer el directorio del proyecto:

```
$ spring init --project-dir=~/my-app my-app
```

Esto creará una nueva aplicación Spring Boot en el directorio `~/my-app`.

## Conclusión

En esta publicación, analizamos cómo personalizar Spring Boot CLI para un desarrollo avanzado. Hemos cubierto cómo instalar la CLI, cómo crear y ejecutar aplicaciones Spring Boot y cómo personalizar la CLI para sus propias necesidades de desarrollo.