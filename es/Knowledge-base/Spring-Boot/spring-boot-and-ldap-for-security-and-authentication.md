---
title: Spring Boot y LDAP para seguridad y autenticación
description: 
published: true
date: 2023-02-08T04:32:47.387Z
tags: 
editor: markdown
dateCreated: 2023-02-08T04:32:45.758Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot and LDAP for Security and Authentication***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-ldap-for-security-and-authentication)
{.links-list}


# Spring Boot y LDAP para seguridad y autenticación

## Introducción

En este artículo, veremos cómo usar Spring Boot y LDAP para seguridad y autenticación. Exploraremos tres formas diferentes de configurar Spring Boot para usar LDAP para la autenticación:

- mediante el uso de la dependencia `spring-boot-starter-security-ldap`
- configurando Spring Security
- configurando ApacheDS

También veremos cómo usar la función de configuración automática de Spring Boot para configurar un servidor LDAP integrado.

## Configuración de Spring Boot para usar LDAP

Hay tres formas diferentes de configurar Spring Boot para usar LDAP para la autenticación.

### Uso de la dependencia `spring-boot-starter-security-ldap`

La forma más fácil de configurar Spring Boot para usar LDAP para la autenticación es usar la dependencia `spring-boot-starter-security-ldap`. Esta dependencia configurará automáticamente Spring Security para usar un servidor LDAP integrado.

Para usar la dependencia `spring-boot-starter-security-ldap`, agregue la siguiente dependencia a su archivo `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security-ldap</artifactId>
</dependency>
```

### Configuración de Spring Security

Si desea tener más control sobre la configuración del servidor LDAP, puede configurar Spring Security para usar un servidor LDAP. Para hacer esto, debe agregar las siguientes dependencias a su archivo `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-ldap</artifactId>
</dependency>
<dependency>
    <groupId>org.apache.directory.server</groupId>
    <artifactId>apacheds-all</artifactId>
</dependency>
```

También necesita configurar el bean `UserDetailsService`. El bean `UserDetailsService` es responsable de cargar los detalles del usuario desde el servidor LDAP.

```java
@Configuration
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .anyRequest().fullyAuthenticated()
                .and()
            .formLogin();
    }

    @Override
    public void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .ldapAuthentication()
                .userDnPatterns("uid={0},ou=people")
                .groupSearchBase("ou=groups")
                .contextSource()
                    .url("ldap://localhost:10389/dc=springframework,dc=org")
                    .and()
                .passwordCompare()
                    .passwordEncoder(new LdapShaPasswordEncoder())
                    .passwordAttribute("userPassword");
    }
}
```

En el ejemplo de código anterior, hemos configurado `UserDetailsService` para buscar usuarios en el grupo LDAP `ou=personas` y para buscar grupos en el grupo LDAP `ou=groups`. También hemos configurado el codificador de contraseñas para usar el codificador `LdapShaPasswordEncoder`.

### Configuración de ApacheDS

Si desea utilizar un servidor LDAP con más funciones, puede configurar ApacheDS. Para hacer esto, debe agregar la siguiente dependencia a su archivo `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-ldap</artifactId>
</dependency>
<dependency>
    <groupId>org.apache.directory.server</groupId>
    <artifactId>apacheds-all</artifactId>
</dependency>
```

También necesita configurar el bean `UserDetailsService`. El bean `UserDetailsService` es responsable de cargar los detalles del usuario desde el servidor LDAP.

```java
@Configuration
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .anyRequest().fullyAuthenticated()
                .and()
            .formLogin();
    }

    @Override
    public void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .ldapAuthentication()
                .userDnPatterns("uid={0},ou=people")
                .groupSearchBase("ou=groups")
                .contextSource()
                    .url("ldap://localhost:10389/dc=springframework,dc=org")
                    .and()
                .passwordCompare()
                    .passwordEncoder(new LdapShaPasswordEncoder())
                    .passwordAttribute("userPassword");
    }
}
```

En el ejemplo de código anterior, hemos configurado `UserDetailsService` para buscar usuarios en el grupo LDAP `ou=personas` y para buscar grupos en el grupo LDAP `ou=groups`. También hemos configurado el codificador de contraseñas para usar el codificador `LdapShaPasswordEncoder`.

## Uso de la función de configuración automática de Spring Boot

La función de configuración automática de Spring Boot se puede utilizar para configurar un servidor LDAP integrado. Para usar la función de configuración automática, debe agregar la siguiente dependencia a su archivo `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-autoconfigure</artifactId>
</dependency>
```

También necesita configurar el bean `UserDetailsService`. El bean `UserDetailsService` es responsable de cargar los detalles del usuario desde el servidor LDAP.

```java
@Configuration
public class WebSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .anyRequest().fullyAuthenticated()
                .and()
            .formLogin();
    }

    @Override
    public void configure(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .ldapAuthentication()
                .userDnPatterns("uid={0},ou=people")
                .groupSearchBase("ou=groups")
                .contextSource()
                    .url("ldap://localhost:10389/dc=springframework,dc=org")
                    .and()
                .passwordCompare()
                    .passwordEncoder(new LdapShaPasswordEncoder())
                    .passwordAttribute("userPassword");
    }
}
```

En el ejemplo de código anterior, hemos configurado `UserDetailsService` para buscar usuarios en el grupo LDAP `ou=personas` y para buscar grupos en el grupo LDAP `ou=groups`. También hemos configurado el codificador de contraseñas para usar el codificador `LdapShaPasswordEncoder`.

## Conclusión

En este artículo, hemos explorado tres formas diferentes de configurar Spring Boot para usar LDAP para la autenticación. También hemos visto cómo usar la función de configuración automática de Spring Boot para configurar un servidor LDAP integrado.