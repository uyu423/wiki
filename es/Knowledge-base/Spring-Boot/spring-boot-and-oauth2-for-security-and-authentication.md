---
title: Spring Boot y OAuth2 para seguridad y autenticación
description: 
published: true
date: 2023-02-08T03:32:23.090Z
tags: 
editor: markdown
dateCreated: 2023-02-08T03:32:21.472Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot and OAuth2 for Security and Authentication***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-oauth2-for-security-and-authentication)
{.links-list}


# Spring Boot y OAuth2 para seguridad y autenticación

Spring Boot Security OAuth2 Stack proporciona una manera conveniente de agregar protección OAuth2 a sus aplicaciones Spring Boot. En este artículo, exploraremos el uso de Spring Boot y OAuth2 para proteger una API REST simple. También agregaremos una capa de seguridad a nuestra API REST con Spring Security y JWT.

## ¿Qué es OAuth2?

OAuth2 es un marco de autorización que permite que las aplicaciones obtengan acceso limitado a cuentas de usuario en un servicio HTTP. Funciona delegando la autenticación del usuario al servicio que aloja la cuenta del usuario y autorizando a las aplicaciones de terceros a acceder a la cuenta del usuario. OAuth2 proporciona un punto final de autorización único y un punto final de token único.

## ¿Qué es Spring Boot?

Spring Boot es un marco basado en Java que se utiliza para crear aplicaciones basadas en Spring independientes y de grado de producción. Es un marco de convención sobre configuración que proporciona una amplia gama de características no funcionales, como servidores integrados, seguridad, métricas, controles de estado, etc.

## ¿Qué es Spring Security?

Spring Security es un marco que proporciona autenticación, autorización y protección contra ataques comunes. Ofrece una amplia gama de mecanismos de autenticación, como la autenticación basada en formularios, la autenticación básica HTTP, etc.

## ¿Qué es JWT?

JWT (JSON Web Token) es un medio compacto y seguro para URL de representar reclamos que se transferirán entre dos partes. Las notificaciones en un JWT se codifican como un objeto JSON que se utiliza como carga útil de una estructura JSON Web Signature (JWS) o como texto sin formato de una estructura JSON Web Encryption (JWE), lo que permite que las notificaciones se firmen digitalmente o se integren. protegido con un Código de Autenticación de Mensaje (MAC) y/o encriptado.

## Configuración del proyecto

Comenzaremos configurando un proyecto Spring Boot simple con las siguientes dependencias:

- Red de arranque de primavera
- Seguridad de arranque de primavera
- Seguridad Spring Boot OAuth2
- Resorte de seguridad JWT

El proyecto se puede crear usando Spring Initializr con las dependencias antes mencionadas.

## Configuración de OAuth2

Configuraremos nuestra aplicación para usar OAuth2 para la autenticación. OAuth2 es un marco de autorización que permite que las aplicaciones obtengan acceso limitado a cuentas de usuario en un servicio HTTP.

Tendremos que crear un bean OAuth2ClientProperties y configurarlo con las propiedades de nuestro cliente OAuth2. También necesitaremos crear un bean ResourceServerProperties y configurarlo con las propiedades de nuestro servidor de recursos.

## Configuración de Spring Security

Configuraremos Spring Security para asegurar nuestra API REST. Tendremos que crear un WebSecurityConfigurerAdapter y anular el método configure(HttpSecurity). En este método, configuraremos las reglas de seguridad para nuestra aplicación.

También necesitaremos crear un JwtAuthenticationFilter y configurarlo para realizar la autenticación JWT.

## Prueba de la aplicación

Podemos probar nuestra aplicación enviando una solicitud POST al punto final /login con un nombre de usuario y una contraseña válidos. Si la autenticación es exitosa, deberíamos recibir una respuesta JSON con un token JWT.

Podemos usar este token para acceder a los recursos protegidos de nuestra aplicación enviando una solicitud GET al punto final /userinfo con el token en el encabezado de Autorización.

## Conclusión

En este artículo, hemos visto cómo usar Spring Boot y OAuth2 para asegurar una API REST simple. También hemos visto cómo usar Spring Security y JWT para agregar una capa de seguridad a nuestra API REST.