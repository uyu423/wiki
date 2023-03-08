---
title: 022: Implementación del manejo de excepciones en una aplicación Spring Boot
description: 
published: true
date: 2023-02-03T14:32:37.858Z
tags: 
editor: markdown
dateCreated: 2023-02-03T14:32:36.264Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [022: Implementing exception handling in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/022-implementing-exception-handling-in-a-spring-boot-application)
{.links-list}


# Implementando el Manejo de Excepciones en una Aplicación Spring Boot

El manejo de excepciones es una parte crítica de cualquier aplicación. En una aplicación Spring Boot, hay algunas formas de implementar el manejo de excepciones.

En esta publicación, repasaremos algunos de los conceptos básicos del manejo de excepciones en una aplicación Spring Boot. Comenzaremos con un ejemplo simple, luego repasaremos algunos temas más avanzados.

## Manejo básico de excepciones

La forma más sencilla de manejar las excepciones en una aplicación Spring Boot es usar la anotación @ControllerAdvice. Esta anotación se puede usar en una clase para manejar excepciones globalmente.

Por ejemplo, digamos que tenemos un controlador simple que devuelve una lista de usuarios:

```java
@RestController
public class UserController {
 
    @GetMapping("/users")
    public List<User> getUsers() {
        // ...
    }
}
```

Si hay un error al obtener la lista de usuarios, podemos usar la anotación @ControllerAdvice para manejar la excepción:

```java
@ControllerAdvice
public class ExceptionHandlerController {
 
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleException(Exception ex) {
        // ...
    }
}
```

En el ejemplo anterior, usamos la anotación @ExceptionHandler para manejar cualquier excepción que ocurra en nuestro controlador. También usamos la anotación @ControllerAdvice para asegurarnos de que nuestro controlador de excepciones se aplique globalmente.

## Manejo avanzado de excepciones

En algunos casos, es posible que desee tener más control sobre cómo se manejan las excepciones. Por ejemplo, es posible que desee devolver una respuesta diferente para diferentes tipos de excepciones.

En Spring Boot, puede usar la anotación @ExceptionHandler para manejar tipos específicos de excepciones. Por ejemplo, digamos que tenemos un controlador que devuelve una lista de usuarios:

```java
@RestController
public class UserController {
 
    @GetMapping("/users")
    public List<User> getUsers() {
        // ...
    }
}
```

Si hay un error al obtener la lista de usuarios, podemos usar la anotación @ExceptionHandler para manejar la excepción:

```java
@ControllerAdvice
public class ExceptionHandlerController {
 
    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<ErrorResponse> handleUserNotFoundException(UserNotFoundException ex) {
        // ...
    }
 
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleException(Exception ex) {
        // ...
    }
}
```

En el ejemplo anterior, usamos la anotación @ExceptionHandler para manejar tipos específicos de excepciones. También usamos la anotación @ControllerAdvice para asegurarnos de que nuestro controlador de excepciones se aplique globalmente.

## Conclusión

El manejo de excepciones es una parte crítica de cualquier aplicación. En una aplicación Spring Boot, hay algunas formas de implementar el manejo de excepciones.

En esta publicación, hemos repasado algunos de los conceptos básicos del manejo de excepciones en una aplicación Spring Boot. Comenzamos con un ejemplo simple, luego repasamos algunos temas más avanzados.