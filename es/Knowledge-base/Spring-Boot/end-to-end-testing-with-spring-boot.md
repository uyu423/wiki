---
title: Pruebas de extremo a extremo con Spring Boot
description: 
published: true
date: 2023-02-01T17:40:25.584Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:40:23.582Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [End-to-end Testing with Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/end-to-end-testing-with-spring-boot)
{.links-list}


# Pruebas de extremo a extremo con Spring Boot

Al crear aplicaciones web, las pruebas de extremo a extremo (E2E) son una parte clave del proceso de desarrollo. Por definición, las pruebas E2E son un tipo de prueba que cubre toda la aplicación, de principio a fin.

En una aplicación web tradicional, el código front-end haría una solicitud al servidor back-end, que luego procesaría la solicitud y devolvería una respuesta. Con una aplicación Spring Boot, el código front-end aún realiza una solicitud, pero el servidor back-end ahora es una aplicación Spring Boot.

Las pruebas E2E son importantes porque permiten a los desarrolladores probar toda la aplicación, desde la interfaz de usuario (UI) hasta el servidor back-end. También permite a los desarrolladores probar cómo funciona la aplicación cuando se implementa en un entorno de producción.

Hay muchos marcos de prueba de E2E diferentes disponibles, pero para este artículo nos centraremos en Spring Boot y el marco de prueba de E2E que proporciona.

## ¿Qué es Spring Boot?

Spring Boot es un marco que permite a los desarrolladores crear e implementar rápidamente aplicaciones basadas en Spring. Proporciona una serie de funciones que facilitan el desarrollo y la implementación, como:

- Servidor Tomcat integrado
- Configuración automática
- Plantillas de inicio

Spring Boot es una excelente opción para desarrollar pruebas E2E porque facilita la creación e implementación de una aplicación basada en Spring.

## ¿Qué es el marco de prueba de E2E?

El marco de prueba de E2E es un conjunto de herramientas que permite a los desarrolladores crear y ejecutar rápidamente pruebas de E2E. Se basa en el marco de pruebas JUnit y proporciona una serie de funciones que facilitan las pruebas E2E, como:

- Una anotación @SpringBootTest que se puede usar para configurar la aplicación Spring Boot para la prueba
- Una anotación @WebIntegrationTest que se puede usar para configurar el servidor web para la prueba
- Una anotación @MockBean que se puede usar para simular beans en el contexto de la aplicación Spring

El marco de prueba de E2E es una excelente opción para desarrollar pruebas de E2E porque facilita la creación y ejecución de pruebas de E2E.

## Crear una prueba E2E

Veamos ahora cómo crear una prueba E2E utilizando el marco de prueba E2E. Probaremos una aplicación Spring Boot simple que tiene un punto final único que devuelve una lista de usuarios.

Lo primero que debemos hacer es crear una nueva clase de prueba JUnit y anotarla con @SpringBootTest:

```java
@SpringBootTest
public class UserControllerTest {

}
```

La anotación @SpringBootTest se usa para configurar la aplicación Spring Boot para la prueba.

A continuación, debemos crear un método de prueba y anotarlo con @Test:

```java
@Test
public void testGetUsers() {

}
```

La anotación @Test se utiliza para marcar un método como método de prueba.

En el método de prueba, necesitamos crear una instancia de UserController e invocar el método getUsers():

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
}
```

El método getUsers() devuelve una lista de usuarios, por lo que podemos afirmar que la lista no está vacía:

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
    assertThat(users).isNotEmpty();
}
```

También podemos afirmar que la lista contiene el número esperado de usuarios:

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
    assertThat(users).hasSize(2);
}
```

Finalmente, podemos afirmar que la lista contiene los usuarios esperados:

```java
@Test
public void testGetUsers() {
    UserController userController = new UserController();
    List<User> users = userController.getUsers();
    assertThat(users)
        .contains(new User("user1@example.com", "User 1"),
                  new User("user2@example.com", "User 2"));
}
```

La prueba E2E completa se muestra a continuación:

```java
@SpringBootTest
public class UserControllerTest {

    @Test
    public void testGetUsers() {
        UserController userController = new UserController();
        List<User> users = userController.getUsers();
        assertThat(users)
            .contains(new User("user1@example.com", "User 1"),
                      new User("user2@example.com", "User 2"));
    }
}
```

## Ejecutando la prueba E2E

Para ejecutar la prueba E2E, simplemente necesitamos ejecutar la clase de prueba como una prueba JUnit:

```java
@SpringBootTest
public class UserControllerTest {

    @Test
    public void testGetUsers() {
        UserController userController = new UserController();
        List<User> users = userController.getUsers();
        assertThat(users)
            .contains(new User("user1@example.com", "User 1"),
                      new User("user2@example.com", "User 2"));
    }
}
```

## Conclusión

En este artículo, hemos visto cómo crear y ejecutar una prueba E2E utilizando el marco de prueba E2E. También hemos visto cómo usar las anotaciones @SpringBootTest y @Test para configurar la aplicación Spring Boot y marcar un método como método de prueba.