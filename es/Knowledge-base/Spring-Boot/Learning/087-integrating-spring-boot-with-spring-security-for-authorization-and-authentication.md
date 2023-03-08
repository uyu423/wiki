---
title: 087: Integración de Spring Boot con Spring Security para autorización y autenticación
description: 
published: true
date: 2023-02-05T17:32:21.517Z
tags: 
editor: markdown
dateCreated: 2023-02-05T17:32:16.204Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [087: Integrating Spring Boot with Spring Security for Authorization and Authentication***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/087-integrating-spring-boot-with-spring-security-for-authorization-and-authentication)
{.links-list}


# 087: Integrando Spring Boot con Spring Security para Autorización y Autenticación

En esta publicación, aprenderemos cómo integrar Spring Boot con Spring Security para autorización y autenticación.

## ¿Por qué Spring Security?

Spring Security es un marco de autenticación y autorización potente y altamente personalizable. Es el estándar de facto para proteger las aplicaciones basadas en Spring.

## Lo que necesitarás

- Un editor de texto o IDE
-JDK 8 o posterior
- Experto 3.0+

## Cómo integrar Spring Boot con Spring Security

1. Agregue las dependencias de Spring Security a su archivo `pom.xml`:

```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-security</artifactId>
	</dependency>
</dependencies>
```

2. Cree un archivo `SecurityConfig.java` y anótelo con `@EnableWebSecurity`:

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

}
```

3. Configure la clase `SecurityConfig` para satisfacer sus necesidades. Por ejemplo, es posible que desee agregar una anotación `@Configuration`:

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

}
```

4. También puede agregar `@EnableGlobalMethodSecurity` para habilitar la seguridad a nivel de método:

```java
@Configuration
@EnableWebSecurity
@EnableGlobalMethodSecurity(prePostEnabled = true)
public class SecurityConfig extends WebSecurityConfigurerAdapter {

}
```

5. En la clase `SecurityConfig`, invalide el método `configure(HttpSecurity)` para configurar los ajustes de seguridad:

```java
@Override
protected void configure(HttpSecurity http) throws Exception {
	http
		.authorizeRequests()
			.anyRequest().authenticated()
			.and()
		.formLogin()
			.loginPage("/login")
			.permitAll()
			.and()
		.logout()
			.permitAll();
}
```

6. También puede configurar Spring Security para usar un almacén de autenticación en memoria:

```java
@Override
protected void configure(AuthenticationManagerBuilder auth) throws Exception {
	auth
		.inMemoryAuthentication()
			.withUser("user").password("password").roles("USER");
}
```

## Probando la Integración

1. Para probar la integración, inicie la aplicación y vaya a `http://localhost:8080/login`. Debería ver la página de inicio de sesión:

![Página de inicio de sesión de Spring Security](https://i.imgur.com/zFw8YxG.png)

2. Introduzca el nombre de usuario y la contraseña del método `configure(AuthenticationManagerBuilder)` y haga clic en "Iniciar sesión". Deberías ver la página de "Bienvenida":

![Página de bienvenida de Spring Security](https://i.imgur.com/ZUwLNcu.png)

## ¡Felicidades!

Ha integrado correctamente Spring Boot con Spring Security.