---
title: 027: Integración con OAuth 2.0 usando Spring Boot
description: 
published: true
date: 2023-02-03T19:32:37.063Z
tags: 
editor: markdown
dateCreated: 2023-02-03T19:32:35.440Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [027: Integrating with OAuth 2.0 using Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/027-integrating-with-oauth-2-0-using-spring-boot)
{.links-list}


# OAuth 2.0 y Spring Boot

En esta publicación, veremos cómo usar Spring Boot para integrarse con OAuth 2.0.

OAuth 2.0 es un estándar popular para la autorización. Es utilizado por muchas grandes empresas, incluidas Google, Facebook y Twitter.

Spring Boot es un marco Java popular para crear aplicaciones web.

## ¿Qué es OAuth 2.0?

OAuth 2.0 es un estándar de autorización. Permite a un usuario otorgar acceso a una aplicación de terceros a sus datos, sin compartir su contraseña.

Por ejemplo, si usa Google para iniciar sesión en un sitio web de terceros, está usando OAuth 2.0. El sitio web de terceros no necesita su contraseña de Google; solo necesita permiso para acceder a sus datos.

## ¿Cómo funciona OAuth 2.0?

OAuth 2.0 funciona mediante el uso de un token. Un token es un dato que representa el permiso de un usuario para acceder a sus datos.

Los tokens son generados por un servidor de autorización. Cuando un usuario otorga acceso a una aplicación de terceros a sus datos, el servidor de autorización genera un token. Luego, el token se envía a la aplicación de terceros.

La aplicación de terceros puede usar el token para acceder a los datos del usuario.

## ¿Por qué usar OAuth 2.0?

Hay varios beneficios al usar OAuth 2.0:

- Es un estándar: OAuth 2.0 es un estándar muy utilizado, por lo que existen muchas bibliotecas y herramientas disponibles para ello.

- Es seguro: OAuth 2.0 está diseñado para ser seguro. Los tokens son generados por un servidor de autorización, por lo que no pueden ser adivinados por aplicaciones de terceros.

- Es fácil de usar: OAuth 2.0 está diseñado para ser fácil de usar. Los usuarios no necesitan recordar sus contraseñas para cada aplicación que usan.

## Cómo usar OAuth 2.0 con Spring Boot

Spring Boot facilita el uso de OAuth 2.0.

Primero, debe agregar la dependencia OAuth de Spring Security a su proyecto:

```xml
<dependency>
    <groupId>org.springframework.security.oauth</groupId>
    <artifactId>spring-security-oauth2</artifactId>
    <version>2.3.4.RELEASE</version>
</dependency>
```

A continuación, debe configurar el servidor de autorización. El servidor de autorización es responsable de generar tokens.

Spring Boot puede configurar automáticamente un servidor de autorización. Todo lo que necesita hacer es agregar las siguientes propiedades a su archivo application.properties:

```properties
spring.security.oauth2.client.registration.client-id=<your-client-id>
spring.security.oauth2.client.registration.client-secret=<your-client-secret>
spring.security.oauth2.client.provider.oauth2.authorization-uri=https://<your-authorization-server>/oauth2/authorize
spring.security.oauth2.client.provider.oauth2.token-uri=https://<your-authorization-server>/oauth2/token
spring.security.oauth2.client.provider.oauth2.user-info-uri=https://<your-authorization-server>/oauth2/userinfo
```

Reemplace <your-client-id> con el ID de cliente de su aplicación y <your-client-secret> con el secreto de cliente de su aplicación.

Reemplace <your-authorization-server> con la URL de su servidor de autorización.

Spring Boot configurará automáticamente un servidor de autorización con el ID de cliente y el secreto de cliente que proporcionó.

Ahora que el servidor de autorización está configurado, puede comenzar a usarlo.

Primero, necesita obtener un token de acceso. Un token de acceso es un token que le permite acceder a los datos de un usuario.

Para obtener un token de acceso, debe enviar una solicitud POST al servidor de autorización. La solicitud debe incluir los siguientes parámetros:

- client_id: El ID de cliente de su aplicación
- client_secret: El secreto del cliente de su aplicación
- grant_type: El tipo de subvención que estás solicitando. Para OAuth 2.0, debería ser "authorization_code"
- código: El código que recibió del servidor de autorización
- redirect_uri: El URI de redirección de su aplicación

El servidor de autorización responderá con un token de acceso.

Una vez que tenga un token de acceso, puede usarlo para acceder a los datos de un usuario.

Para hacer esto, debe enviar una solicitud GET al servidor de recursos. La solicitud debe incluir los siguientes parámetros:

- access_token: el token de acceso que recibió del servidor de autorización

El servidor de recursos responderá con los datos del usuario.

## Información adicional

- OAuth 2.0 es un estándar de autorización, no un estándar de autenticación. OAuth 2.0 se puede utilizar para la autenticación, pero no está diseñado para ello.

- Spring Boot no es compatible con OAuth 2.0 de fábrica. Debe agregar la dependencia Spring Security OAuth a su proyecto.

- Spring Boot puede configurar automáticamente un servidor de autorización. Todo lo que necesita hacer es agregar la identificación del cliente y el secreto del cliente a su archivo application.properties.