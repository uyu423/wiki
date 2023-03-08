---
title: Implementación de Spring Boot en Cloud Foundry
description: 
published: true
date: 2023-02-02T14:57:41.415Z
tags: 
editor: markdown
dateCreated: 2023-02-02T14:57:39.819Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Deployment on Cloud Foundry***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-deployment-on-cloud-foundry)
{.links-list}


# Implementación de Spring Boot en Cloud Foundry

Los desarrolladores que buscan implementar aplicaciones basadas en Spring Boot en Cloud Foundry tienen algunas opciones diferentes. En este artículo, veremos algunas de estas opciones y analizaremos las ventajas y desventajas de cada una.

## Envasado en tarro

Una opción para empaquetar una aplicación Spring Boot es empaquetarla como un archivo jar. Este es el enfoque recomendado en la documentación de Spring Boot.

Para empaquetar una aplicación Spring Boot como un jar, deberá usar el complemento `spring-boot-maven-plugin`. Este complemento empaquetará su aplicación como un archivo jar ejecutable. A continuación, puede implementar este archivo jar en Cloud Foundry mediante el comando `cf push`.

Una de las ventajas de empaquetar su aplicación como un jar es que puede ejecutarla fácilmente localmente usando el comando `java -jar`. Esto puede ser útil para fines de depuración.

Otra ventaja de empaquetar como un jar es que puede especificar cualquier variable de entorno que necesite su aplicación en el archivo `manifest.yml`. Esto puede ser útil si desea evitar la codificación rígida de cualquier valor específico del entorno en su código.

## El embalaje como guerra

Otra opción para empaquetar una aplicación Spring Boot es empaquetarla como un archivo war. Este no es el enfoque recomendado en la documentación de Spring Boot, pero es una opción.

Para empaquetar una aplicación Spring Boot como una guerra, deberá usar la dependencia `spring-boot-starter-web`. Esta dependencia incluirá todas las bibliotecas necesarias para empaquetar su aplicación como una guerra.

Luego puede implementar este archivo war en Cloud Foundry usando el comando `cf push`. Una ventaja de empaquetar como una guerra es que puede especificar cualquier variable de entorno que necesite su aplicación en el archivo `manifest.yml`. Esto puede ser útil si desea evitar la codificación rígida de cualquier valor específico del entorno en su código.

## Uso del paquete de compilación Java de Cloud Foundry

Cloud Foundry proporciona un paquete de compilación Java que se puede usar para implementar aplicaciones Spring Boot. Este paquete de compilación detectará que su aplicación es una aplicación Spring Boot y la configurará en consecuencia.

Para usar el paquete de compilación Java de Cloud Foundry, deberá especificar `java_buildpack` como el paquete de compilación para su aplicación en el archivo `manifest.yml`. Luego puede implementar su aplicación usando el comando `cf push`.

Una ventaja de usar el paquete de compilación Java de Cloud Foundry es que no necesita empaquetar su aplicación en un archivo jar o war. El paquete de compilación lo hará por usted.

Otra ventaja de usar el paquete de compilación Java de Cloud Foundry es que puede especificar cualquier variable de entorno que necesite su aplicación en el archivo `manifest.yml`. Esto puede ser útil si desea evitar la codificación rígida de cualquier valor específico del entorno en su código.

## Uso de los conectores Spring Cloud

Spring Cloud Connectors proporciona una capa de abstracción que le permite usar cualquier servicio de Cloud Foundry con una aplicación Spring. Esto puede resultar útil si desea utilizar un servicio que actualmente no es compatible con el paquete de compilación Java de Cloud Foundry.

Para usar Spring Cloud Connectors, deberá agregar la dependencia `spring-cloud-spring-service-connector` a su proyecto. Luego puede implementar su aplicación usando el comando `cf push`.

Una ventaja de usar Spring Cloud Connectors es que no necesita empaquetar su aplicación en un archivo jar o war. El paquete de compilación lo hará por usted.

Otra ventaja de usar Spring Cloud Connectors es que puede especificar cualquier variable de entorno que su aplicación necesite en el archivo `manifest.yml`. Esto puede ser útil si desea evitar la codificación rígida de cualquier valor específico del entorno en su código.

## Conclusión

Hay algunas opciones diferentes para implementar aplicaciones Spring Boot en Cloud Foundry. Cada opción tiene sus propias ventajas y desventajas. Depende de usted decidir qué opción es la mejor para su aplicación.