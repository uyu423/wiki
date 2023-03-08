---
title: 064: Personalización de la configuración de Tomcat integrada en Spring Boot
description: 
published: true
date: 2023-02-02T16:23:33.376Z
tags: 
editor: markdown
dateCreated: 2023-02-02T16:23:28.851Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [064: Customizing the Embedded Tomcat Configuration in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/064-customizing-the-embedded-tomcat-configuration-in-spring-boot)
{.links-list}


# Personalización de la configuración de Tomcat integrada en Spring Boot

Spring Boot proporciona una serie de funciones que se pueden usar para personalizar la configuración integrada de Tomcat. En esta publicación, veremos algunas de las opciones de configuración más importantes.

## Configuración del puerto HTTP

Lo primero que debería hacer es cambiar el puerto HTTP en el que se ejecuta Tomcat. De manera predeterminada, Tomcat se ejecutará en el puerto 8080, pero puede cambiar esto configurando la propiedad ```server.port``` en su archivo application.properties:

```properties
server.port=8081
```

## Configuración del tiempo de espera de la sesión de Tomcat

Otra personalización común es cambiar el tiempo de espera de la sesión. De manera predeterminada, Tomcat usará un tiempo de espera de sesión de 30 minutos, pero puede cambiar esto configurando la propiedad ```server.session-timeout```:

```properties
server.session-timeout=1
```

## Configuración del registro de acceso de Tomcat

Tomcat también creará un registro de acceso que contiene información sobre todas las solicitudes que se realizan al servidor. De forma predeterminada, este registro se encuentra en el directorio ```logs```, pero puede cambiar la ubicación configurando la propiedad ```server.tomcat.accesslog.directory```:

```properties
server.tomcat.accesslog.directory=/var/log/tomcat
```

## Configuración de la codificación URI de Tomcat

De forma predeterminada, Tomcat utilizará el conjunto de caracteres ISO-8859-1 para la codificación de URI. Sin embargo, puede cambiar esto configurando la propiedad ```server.tomcat.uri-encoding```:

```properties
server.tomcat.uri-encoding=UTF-8
```

## Configuración del conector Tomcat

Tomcat usa un conector para recibir solicitudes y enviar respuestas. De forma predeterminada, Tomcat utilizará el conector AJP, pero puede cambiar esto configurando la propiedad ```server.tomcat.protocol-header```:

```properties
server.tomcat.protocol-header=org.apache.coyote.http11.Http11NioProtocol
```

## Configuración de la ruta de contexto de Tomcat

La ruta de contexto es la ruta que se utiliza para acceder a su aplicación. De forma predeterminada, está configurado en ```/```, pero puede cambiarlo configurando la propiedad ```server.context-path```:

```properties
server.context-path=/myapp
```

## Configuración de Tomcat SSL

Tomcat también es compatible con SSL para comunicaciones seguras. Para configurar SSL, deberá configurar ```server.ssl.key-store```, ```server.ssl.key-store-password```, ```server.ssl.key-alias propiedades ``` y ```server.ssl.key-alias-password```. Para obtener más información sobre la configuración de SSL en Tomcat, consulte [Cómo configurar SSL de Tomcat] (https://tomcat.apache.org/tomcat-8.5-doc/ssl-howto.html).

## Conclusión

En esta publicación, analizamos algunas de las formas más importantes de personalizar la configuración integrada de Tomcat en Spring Boot. Al cambiar algunas propiedades simples, puede cambiar la forma en que se ejecuta Tomcat para que se adapte mejor a sus necesidades.