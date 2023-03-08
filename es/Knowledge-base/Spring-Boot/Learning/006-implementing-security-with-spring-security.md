---
title: 006: Implementando seguridad con Spring Security
description: 
published: true
date: 2023-02-03T07:45:38.194Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:45:36.284Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [006: Implementing security with Spring Security***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/006-implementing-security-with-spring-security)
{.links-list}


# Implementando seguridad con Spring Security

Spring Security es un marco que proporciona servicios de autenticación y autorización en aplicaciones Java. Es un marco ampliamente utilizado y proporciona muchas características listas para usar. En esta publicación, veremos cómo implementar la seguridad en una aplicación Spring usando Spring Security.

## Configuración de Spring Security

El primer paso es agregar la dependencia de Spring Security a su proyecto. Si está utilizando Maven, puede agregar la siguiente dependencia a su archivo `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-core</artifactId>
    <version>5.0.0.RELEASE</version>
</dependency>
```

Si está utilizando Gradle, puede agregar la siguiente dependencia a su archivo `build.gradle`:

```groovy
dependencies {
    compile 'org.springframework.security:spring-security-core:5.0.0.RELEASE'
}
```

Una vez que se agrega la dependencia, puede configurar Spring Security agregando una clase `SecurityConfig` y anotándola con `@EnableWebSecurity`. La clase `SecurityConfig` se puede configurar para usar autenticación en memoria o autenticación LDAP. En este ejemplo, utilizaremos la autenticación en memoria.

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
}
```

En el método `configure`, estamos configurando una autenticación en memoria con un usuario que tiene el nombre de usuario `usuario` y la contraseña `contraseña`. El usuario también tiene el rol `USUARIO`.

## Protección de URL

Una vez que haya configurado Spring Security, puede proteger las URL utilizando la anotación `@Secured`. La anotación `@Secured` se puede usar tanto en métodos como en clases. En el siguiente ejemplo, estamos asegurando la URL `/admin` para que solo los usuarios con el rol `ADMIN` puedan acceder a ella.

```java
@Controller
public class AdminController {

    @Secured("ROLE_ADMIN")
    @RequestMapping("/admin")
    public String admin() {
        return "admin";
    }
}
```

Si intenta acceder a la URL `/admin` sin estar autenticado, obtendrá un error `403 Prohibido`.

## Implementando una página de inicio de sesión

Para autenticar a los usuarios, debe implementar una página de inicio de sesión. La página de inicio de sesión se puede implementar utilizando un formulario HTML estándar. En el siguiente ejemplo, estamos usando un formulario HTML simple con un campo de nombre de usuario y contraseña.

```html
<form action="/login" method="POST">
    <input type="text" name="username" />
    <input type="password" name="password" />
    <input type="submit" value="Login" />
</form>
```

Cuando se envía el formulario, se llama a la URL `/login`. La URL `/login` es manejada por Spring Security y el usuario es autenticado. Si la autenticación es exitosa, se redirige al usuario a la URL solicitada originalmente. Si la autenticación no tiene éxito, se redirige al usuario a la página de inicio de sesión.

Para implementar la página de inicio de sesión, debe agregar un `WebSecurityConfigurerAdapter` y anular el método `configure`. En el método `configure`, debe agregar el método `formLogin` y especificar la página de inicio de sesión y la página de éxito de inicio de sesión.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .formLogin()
                .loginPage("/login")
                .defaultSuccessUrl("/");
    }
}
```

En el método `formLogin`, estamos especificando la URL `/login` como la página de inicio de sesión y la URL `/` como la página de éxito de inicio de sesión.

## Cerrar sesión

Spring Security también brinda soporte para cerrar sesión. Para implementar el cierre de sesión, debe agregar el método `logout` al método `configure`. El método `logout` toma `logoutSuccessUrl` como parámetro. `logoutSuccessUrl` es la URL a la que se redirige al usuario después de un cierre de sesión exitoso.

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .logout()
                .logoutSuccessUrl("/login?logout");
    }
}
```

En el método `logout`, estamos especificando la URL `/login?logout` como la URL exitosa de cierre de sesión. Spring Security maneja la URL `logout` y se cierra la sesión del usuario.

## Conclusión

En este post hemos visto cómo implementar la seguridad en una aplicación Spring usando Spring Security. Spring Security es un marco poderoso que proporciona muchas funciones listas para usar.