---
title: 084: Implementación de un proveedor de autenticación personalizado en Spring Boot
description: 
published: true
date: 2023-02-05T14:32:26.078Z
tags: 
editor: markdown
dateCreated: 2023-02-05T14:32:24.489Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [084: Implementing a Custom Authentication Provider in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/084-implementing-a-custom-authentication-provider-in-spring-boot)
{.links-list}


# Implementación de un proveedor de autenticación personalizado en Spring Boot

Cuando se trata de la autenticación en Spring Boot, hay algunas formas diferentes de hacerlo. En esta publicación, veremos cómo implementar un proveedor de autenticación personalizado.

## ¿Qué es un proveedor de autenticación?

Un proveedor de autenticación es una pieza de software que maneja el proceso de autenticación de un usuario. En el contexto de una aplicación web, esto generalmente significa verificar que el usuario haya proporcionado las credenciales correctas (nombre de usuario y contraseña) y, de ser así, permitirle el acceso a la aplicación.

## ¿Por qué usar un proveedor de autenticación personalizado?

Hay algunas razones por las que es posible que desee utilizar un proveedor de autenticación personalizado:

* Quiere usar un método de autenticación diferente al que Spring Boot proporciona de fábrica (por ejemplo, quiere usar LDAP en lugar de una base de datos).
* Desea agregar funcionalidad adicional al proceso de autenticación (por ejemplo, desea registrar todos los intentos fallidos de inicio de sesión).
* Desea tener más control sobre cómo funciona el proceso de autenticación (por ejemplo, desea poder personalizar los mensajes de error que se muestran al usuario).

## Cómo implementar un proveedor de autenticación personalizado

Implementar un proveedor de autenticación personalizado es bastante simple. Todo lo que necesita hacer es crear una clase que implemente la interfaz org.springframework.security.authentication.AuthenticationProvider.

Aquí hay un ejemplo simple:

```java
public class MyAuthenticationProvider implements AuthenticationProvider {

    @Override
    public Authentication authenticate(Authentication authentication) throws AuthenticationException {
        // TODO: Implement authentication logic here
        return null;
    }

    @Override
    public boolean supports(Class<?> authentication) {
        // TODO: Implement authentication support logic here
        return false;
    }
}
```

Hay dos métodos que deben implementarse:

* `authenticate()`: aquí es donde va la lógica de autenticación real. El método toma un objeto `Autenticación` como parámetro y devuelve un objeto `Autenticación`.
* `supports()`: este método se usa para determinar si `AuthenticationProvider` admite el objeto `Authentication` dado.

## Configuración del proveedor de autenticación

Una vez implementado el `AuthenticationProvider`, el siguiente paso es configurarlo en Spring Boot. Esto se puede hacer agregando lo siguiente al archivo `application.properties`:

```properties
spring.security.authentication-provider.class=com.example.MyAuthenticationProvider
```

## Prueba del proveedor de autenticación

Para probar el proveedor de autenticación, puede usar la anotación `@WithMockUser` en un método de prueba. Esto creará un usuario simulado con el nombre de usuario y la contraseña proporcionados que se pueden usar para autenticarse con el proveedor de autenticación.

Aquí hay un ejemplo simple:

```java
@Test
@WithMockUser(username="test", password="test")
public void testAuthentication() {
    // TODO: Implement authentication test here
}
```

## Conclusión

En esta publicación, analizamos cómo implementar un proveedor de autenticación personalizado en Spring Boot. También hemos visto cómo configurarlo y cómo probarlo.