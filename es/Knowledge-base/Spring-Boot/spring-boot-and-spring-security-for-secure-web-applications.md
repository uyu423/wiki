---
title: Spring Boot y Spring Security para aplicaciones web seguras
description: 
published: true
date: 2023-02-06T03:17:41.931Z
tags: 
editor: markdown
dateCreated: 2023-02-06T03:17:40.318Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot and Spring Security for Secure Web Applications***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-spring-security-for-secure-web-applications)
{.links-list}


# Spring Boot y Spring Security para aplicaciones web seguras

Desarrollar una aplicación web segura es una prioridad para cualquier organización. En este artículo, veremos cómo usar Spring Boot y Spring Security para crear una aplicación web simple y segura.

Primero crearemos una aplicación Spring Boot con una configuración de seguridad básica. Luego agregaremos algunas funciones de Spring Security para proteger nuestra aplicación.

## Creación de una aplicación Spring Boot

Comenzaremos creando una aplicación Spring Boot. Spring Boot facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción que puede "simplemente ejecutar".

Usaremos [Spring Initializr](https://start.spring.io/) para crear nuestro proyecto. Seleccionaremos las siguientes dependencias:

- Internet
- Seguridad

Llamaremos a nuestro proyecto `secure-web-app`.

Una vez que se genera el proyecto, podemos importarlo a nuestro IDE favorito y ejecutarlo como una aplicación Spring Boot.

## Configuración básica de seguridad

Spring Security es un marco que proporciona autenticación, autorización y protección contra ataques comunes.

De forma predeterminada, Spring Security no está configurado. Podemos agregar una configuración básica agregando lo siguiente a nuestro archivo `application.properties`:

```
spring.security.user.name=user
spring.security.user.password=password
```

Esto creará un usuario con el nombre de usuario `usuario` y la contraseña `contraseña`.

También podemos agregar una configuración más completa creando un archivo `SecurityConfig.java`.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic();
    }
}
```

Esto configurará Spring Security para requerir autenticación para todas las solicitudes y para usar el formulario de inicio de sesión y la autenticación HTTP básica.

## Adición de funciones de seguridad de Spring

Ahora que tenemos una configuración básica de Spring Security, podemos agregar algunas características adicionales.

### Protección CSRF

La falsificación de solicitud entre sitios (CSRF) es un tipo de ataque que ocurre cuando un usuario malintencionado engaña a una víctima para que envíe una solicitud a una aplicación web en la que está conectado.

Spring Security proporciona protección CSRF de forma predeterminada. Podemos configurarlo agregando lo siguiente a nuestro archivo `SecurityConfig.java`:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .csrf().disable()
            ...
    }
}
```

Esto deshabilitará la protección CSRF.

### Cabeceras de seguridad

También podemos agregar encabezados de seguridad a nuestras respuestas para ayudar a protegernos contra ataques comunes.

Podemos agregar lo siguiente a nuestro archivo `SecurityConfig.java`:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .headers()
                .contentSecurityPolicy("script-src 'self'");
    }
}
```

Esto agregará el encabezado `Content-Security-Policy` a nuestras respuestas.

También podemos agregar el encabezado `Strict-Transport-Security` para hacer cumplir HTTPS:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .requiresChannel()
                .requestMatchers(r -> r.getHeader("X-Forwarded-Proto") != null)
                .requiresSecure();
    }
}
```

Esto requerirá HTTPS para todas las solicitudes que contengan el encabezado `X-Forwarded-Proto`.

### Proveedores de autenticación

Spring Security admite múltiples proveedores de autenticación. Podemos agregar soporte para proveedores adicionales anulando el método `configure(AuthenticationManagerBuilder)`:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .inMemoryAuthentication()
                .withUser("user").password("password").roles("USER");
    }

    ...
}
```

Esto configurará un proveedor de autenticación en memoria con un solo usuario.

También podemos agregar soporte para [autenticación basada en JDBC] (https://docs.spring.io/spring-security/site/docs/current/reference/html5/# jc-authentication-jdbc).

## Conclusión

En este artículo, hemos visto cómo usar Spring Boot y Spring Security para crear una aplicación web simple y segura. También hemos agregado algunas funciones de seguridad adicionales para ayudar a proteger nuestra aplicación.