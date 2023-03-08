---
title: 058: Implementación de seguridad en una aplicación Spring Boot
description: 
published: true
date: 2023-02-04T21:32:30.237Z
tags: 
editor: markdown
dateCreated: 2023-02-04T21:32:24.985Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [058: Implementing Security in a Spring Boot Application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/058-implementing-security-in-a-spring-boot-application)
{.links-list}


# Implementación de seguridad en una aplicación Spring Boot

Como desarrollador de Java, probablemente esté familiarizado con Spring Framework. Spring Boot es una extensión del marco Spring que facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

En esta publicación, veremos cómo implementar la seguridad en una aplicación Spring Boot. Comenzaremos analizando los diferentes tipos de seguridad que se pueden implementar en una aplicación Spring Boot. Luego, veremos cómo configurar y usar el marco Spring Security para asegurar nuestra aplicación.

## Tipos de Seguridad

Hay dos tipos principales de seguridad que se pueden implementar en una aplicación Spring Boot: autenticación y autorización.

La autenticación es el proceso de verificar que un usuario es quien dice ser. La autorización es el proceso de determinar si un usuario tiene acceso a un recurso en particular.

En una aplicación Spring Boot, la autenticación generalmente se maneja mediante un formulario de inicio de sesión. El usuario ingresa su nombre de usuario y contraseña, y Spring Security verifica que las credenciales sean válidas.

La autorización generalmente se maneja mediante la asignación de roles a los usuarios. Por ejemplo, puede tener un rol para administradores y un rol para usuarios normales. Los administradores pueden tener acceso a más recursos que los usuarios normales.

## Configuración de Spring Security

Spring Security es un marco que proporciona servicios de autenticación y autorización. Es fácil de configurar y usar en una aplicación Spring Boot.

Para agregar Spring Security a su aplicación, agregue la siguiente dependencia a su archivo de compilación:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

Una vez que haya agregado la dependencia, Spring Security se habilitará de forma predeterminada. De forma predeterminada, Spring Security utilizará la autenticación en memoria. Esto significa que no hay necesidad de configurar una base de datos o cualquier otro servicio externo.

Para configurar Spring Security, puede agregar una clase @Configuration a su aplicación. Esta clase se puede usar para configurar varios aspectos de Spring Security, como los usuarios que pueden acceder a la aplicación y los roles que tienen.

## Autenticando Usuarios

Cuando un usuario intenta acceder a un recurso protegido, será redirigido a una página de inicio de sesión. En esta página, ingresarán su nombre de usuario y contraseña.

Spring Security luego autenticará al usuario. Si las credenciales son válidas, el usuario será redirigido al recurso al que intentaba acceder. Si las credenciales no son válidas, el usuario será redirigido a una página de error.

## Autorización de usuarios

Una vez que se haya autenticado a un usuario, Spring Security deberá autorizar al usuario antes de que pueda acceder a un recurso protegido.

La autorización generalmente se realiza mediante la asignación de roles a los usuarios. Por ejemplo, puede tener un rol para administradores y un rol para usuarios normales. Los administradores pueden tener acceso a más recursos que los usuarios normales.

Puede configurar los roles que tiene un usuario agregando la anotación @RolesAllowed a un controlador o método de servicio. Por ejemplo:

```java
@Service
public class MyService {

    @RolesAllowed("ADMIN")
    public void doSomething() {
        // ...
    }
}
```

En este ejemplo, solo los usuarios con el rol ADMIN pueden acceder al método doSomething().

## Conclusión

En esta publicación, hemos visto cómo implementar la seguridad en una aplicación Spring Boot. Hemos analizado los diferentes tipos de seguridad que se pueden implementar y hemos visto cómo configurar y usar el marco Spring Security.