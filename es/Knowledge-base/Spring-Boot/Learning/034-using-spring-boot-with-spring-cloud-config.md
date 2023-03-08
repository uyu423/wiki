---
title: 034: Uso de Spring Boot con Spring Cloud Config
description: 
published: true
date: 2023-02-04T02:32:36.860Z
tags: 
editor: markdown
dateCreated: 2023-02-04T02:32:31.605Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [034: Using Spring Boot with Spring Cloud Config***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/034-using-spring-boot-with-spring-cloud-config)
{.links-list}


# Usar Spring Boot con Spring Cloud Config

Spring Cloud Config proporciona soporte del lado del servidor y del cliente para la configuración externalizada en un sistema distribuido. El servidor de configuración se puede usar fácilmente con aplicaciones Spring Boot a través de la anotación @EnableConfigServer.

En esta publicación, veremos cómo usar el servidor de configuración con una aplicación Spring Boot. También veremos cómo usar el cliente de configuración para conectarse al servidor de configuración y obtener la configuración.

## Configuración del servidor de configuración

Lo primero que debemos hacer es configurar el servidor de configuración. Podemos hacer esto usando la anotación @EnableConfigServer en nuestra aplicación Spring Boot:

```java
@SpringBootApplication
@EnableConfigServer
public class ConfigServerApplication {

    public static void main(String[] args) {
        SpringApplication.run(ConfigServerApplication.class, args);
    }
}
```

Esto habilitará el servidor de configuración en nuestra aplicación. De forma predeterminada, el servidor de configuración proporcionará la configuración desde un archivo ubicado en la ruta de clases de la aplicación.

También podemos configurar el servidor de configuración para obtener la configuración de un repositorio de Git. Por ejemplo, podemos agregar lo siguiente a nuestro archivo application.properties:

```properties
spring.cloud.config.server.git.uri=https://github.com/spring-cloud/spring-cloud-config
spring.cloud.config.server.git.searchPaths=config-repo
```

Esto le indicará al servidor de configuración que obtenga la configuración del repositorio spring-cloud-config GitHub, en el directorio config-repo.

## Configuración del cliente de configuración

Ahora que tenemos configurado nuestro servidor de configuración, podemos configurar nuestro cliente de configuración. El cliente de configuración es una aplicación Spring Boot que obtiene la configuración del servidor de configuración.

Podemos configurar el cliente de configuración usando la anotación @EnableConfigClient:

```java
@SpringBootApplication
@EnableConfigClient
public class ConfigClientApplication {

    public static void main(String[] args) {
        SpringApplication.run(ConfigClientApplication.class, args);
    }
}
```

Esto habilitará el Config Client en nuestra aplicación. De forma predeterminada, el cliente de configuración se conectará al servidor de configuración en http://localhost:8888.

También podemos configurar el cliente de configuración para conectarse a un servidor de configuración diferente. Por ejemplo, podemos agregar lo siguiente a nuestro archivo application.properties:

```properties
spring.cloud.config.uri=http://config-server:8888
```

Esto le indicará al cliente de configuración que se conecte al servidor de configuración en http://config-server:8888.

## Obtener configuración

Una vez que hayamos configurado nuestro servidor de configuración y nuestro cliente de configuración, podemos obtener la configuración del servidor de configuración. Config Client obtendrá la configuración y la pondrá a disposición de nuestra aplicación.

Por ejemplo, podemos agregar lo siguiente a nuestro archivo application.properties:

```properties
spring.cloud.config.name=my-app
```

Esto le indicará a Config Client que obtenga la configuración para la aplicación my-app. La configuración estará disponible para nuestra aplicación a través de Spring Environment.

También podemos obtener la configuración para perfiles específicos. Por ejemplo, podemos agregar lo siguiente a nuestro archivo application.properties:

```properties
spring.cloud.config.name=my-app
spring.cloud.config.profile=dev
```

Esto le indicará a Config Client que obtenga la configuración para la aplicación my-app con el perfil de desarrollador. La configuración estará disponible para nuestra aplicación a través de Spring Environment.

## Conclusión

En esta publicación, hemos visto cómo usar el servidor de configuración con una aplicación Spring Boot. También hemos visto cómo usar el cliente de configuración para conectarse al servidor de configuración y obtener la configuración.