---
title: Spring Tool Suite: el entorno de desarrollo definitivo
description: 
published: true
date: 2023-02-06T05:32:27.950Z
tags: 
editor: markdown
dateCreated: 2023-02-06T05:32:26.242Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Tool Suite: The Ultimate Development Environment***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-tool-suite-the-ultimate-development-environment)
{.links-list}

      

# Spring Tool Suite: el entorno de desarrollo definitivo

Con tantas opciones y configuraciones diferentes disponibles, configurar un entorno de desarrollo puede ser una tarea abrumadora, especialmente para aquellos que son nuevos en el mundo de TI. Sin embargo, hay una herramienta que puede facilitar mucho este proceso: Spring Tool Suite (STS).

STS es un IDE basado en Eclipse que está especialmente diseñado para desarrollar aplicaciones Spring. Viene con una amplia gama de características que pueden mejorar en gran medida la experiencia del desarrollador, que incluyen:

- Plantillas de proyecto para crear nuevos proyectos Spring Boot, MVC y Batch.
- Generación automática de metadatos del proyecto (por ejemplo, archivos pom.xml).
- Soporte integrado para la recarga dinámica de clases y recursos de Java.
- Integración con herramientas de construcción populares como Maven y Gradle.
- Una vista de consola para ver la salida de los registros de la aplicación.

Además, STS proporciona una gran cantidad de complementos que pueden agregar aún más funciones, como:

- CLI de Spring Cloud: le permite desarrollar, probar e implementar aplicaciones de Spring Cloud en su máquina local.
- Spring Cloud Data Flow: una herramienta para construir canalizaciones de datos utilizando Spring Cloud Streams.
- Spring Cloud Security: agrega funciones de seguridad a las aplicaciones de Spring Cloud.

Con todas estas características, STS puede ser un activo poderoso para cualquier desarrollador, independientemente de su nivel de experiencia. En este artículo, veremos más de cerca cómo comenzar con STS y algunas de sus características más útiles.

## Instalación de STS

STS se puede descargar desde el [sitio web de Spring Tools] (https://spring.io/tools). Hay dos versiones disponibles:

- La edición **Estándar**, que incluye las funciones principales de STS.
- La edición **Ultimate**, que incluye todas las funciones de la edición estándar, además de complementos adicionales para desarrollar aplicaciones nativas de la nube.

Para este artículo, utilizaremos la edición Ultimate. Una vez que haya descargado el archivo ZIP, extráigalo a la ubicación que elija e inicie el ejecutable STS.

## Crear un nuevo proyecto

Cuando inicie STS por primera vez, se le presentará la pantalla de bienvenida. Desde aquí, puede optar por crear un nuevo proyecto, importar un proyecto existente o abrir un proyecto desde un directorio.

Vamos a crear un nuevo proyecto, así que seleccione la opción "Crear un nuevo proyecto Spring Starter".

![Pantalla de bienvenida de STS](https://i.imgur.com/l7qE4Vx.png)

En la siguiente pantalla, se le pedirá que proporcione cierta información sobre el proyecto, como el nombre y la ubicación. También puede elegir qué herramienta de compilación desea usar (Maven o Gradle) y qué tipo de proyecto desea crear.

Para este ejemplo, crearemos un proyecto Spring Boot basado en Maven. Una vez que haya ingresado la información necesaria, haga clic en el botón "Finalizar".

![Pantalla de nuevo proyecto](https://i.imgur.com/DY6rNcu.png)

 STS ahora creará el proyecto y lo abrirá en el IDE.

## Explorando el IDE

El STS IDE se basa en Eclipse, por lo que si está familiarizado con ese IDE, debe sentirse como en casa. Sin embargo, hay algunas características específicas de STS que vale la pena mencionar.

### Tablero de inicio de primavera

Una de las características más útiles de STS es Spring Boot Dashboard. Esta es una vista especial que brinda acceso rápido a las funciones de Spring Boot más utilizadas.

![Panel de arranque Spring](https://i.imgur.com/uY0A8tV.png)

Desde el tablero, puede ver y administrar las dependencias de su aplicación, iniciar y detener la aplicación, ver los registros de la aplicación y mucho más.

### Frijoles primaverales

Otra característica útil de STS es la vista Spring Boot Beans. Esta vista muestra todos los beans que están definidos en su aplicación, así como sus dependencias.

![Frijoles primaverales](https://i.imgur.com/Lzq3G8I.png)

Esta puede ser una herramienta valiosa para depurar su aplicación, ya que puede ayudarlo a comprender cómo encajan las diferentes piezas de su aplicación.

### Aplicaciones Spring Boot

La vista Spring Boot Apps es otra característica específica de STS que puede ser muy útil al desarrollar aplicaciones Spring Boot.

![Aplicaciones Spring Boot](https://i.imgur.com/DxvkVrA.png)

Esta vista muestra todas las aplicaciones Spring Boot que se ejecutan en su máquina local, así como sus puertos de depuración y JMX. Esto puede ser muy útil cuando necesita conectarse a una aplicación remota con fines de depuración o supervisión.

## Conclusión

En este artículo, hemos analizado algunas de las características más útiles del IDE de Spring Tool Suite. También hemos visto cómo instalar STS y crear un nuevo proyecto Spring Boot.

Si bien esta es solo una breve introducción a lo que STS tiene para ofrecer, debería darle una buena idea de cómo esta poderosa herramienta puede ayudarlo a desarrollar aplicaciones Spring de manera más efectiva.