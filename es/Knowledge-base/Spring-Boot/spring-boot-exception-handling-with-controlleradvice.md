---
title: Manejo de excepciones de Spring Boot con ControllerAdvice
description: 
published: true
date: 2023-02-07T17:32:29.141Z
tags: 
editor: markdown
dateCreated: 2023-02-07T17:32:27.534Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Exception Handling with ControllerAdvice***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-exception-handling-with-controlleradvice)
{.links-list}



# Introducción

Los desarrolladores se enfrentan a muchos tipos diferentes de errores al crear aplicaciones. Estos errores pueden ser causados por la entrada del usuario, por problemas con el código o por problemas con el servidor o la base de datos.

En este artículo, veremos cómo manejar los errores en Spring Boot. Comenzaremos con una breve descripción general de los diferentes tipos de errores que pueden ocurrir y luego analizaremos cómo manejarlos usando la anotación @ControllerAdvice.

# Tipos de errores

Hay tres tipos principales de errores que pueden ocurrir al crear una aplicación Spring Boot:

* **Errores de validación:** Estos ocurren cuando la entrada del usuario no coincide con el formato esperado. Por ejemplo, si un usuario intenta enviar un formulario con una dirección de correo electrónico no válida, se producirá un error de validación.

* **Errores de vinculación:** Estos ocurren cuando falla el proceso de vinculación de datos. Esto puede suceder si la entrada del usuario tiene un formato incorrecto o si hay una discrepancia de tipo entre la entrada y el objeto de destino.

* **Otros errores:** Estos incluyen todos los demás tipos de errores, como errores de la base de datos, errores del servidor, etc.

# Manejo de errores

En Spring Boot, los errores se pueden manejar mediante la anotación @ControllerAdvice. Esta anotación se puede utilizar para definir un controlador de errores global para todos los controladores.

La anotación @ControllerAdvice se puede usar para manejar errores de validación y enlace. Para manejar otros tipos de errores, puede usar la anotación @ExceptionHandler.

# Errores de validación

Los errores de validación se pueden manejar mediante la anotación @ControllerAdvice. En el siguiente ejemplo, usamos la anotación @ControllerAdvice para manejar los errores de validación:

```java
@ControllerAdvice
public class ValidationErrorHandler {

    @InitBinder
    public void initBinder(WebDataBinder binder) {
        binder.addValidators(new UserValidator());
    }

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<?> handleValidationErrors(MethodArgumentNotValidException ex) {
        // ...
    }

}
```

En el ejemplo anterior, usamos la anotación @InitBinder para registrar un validador para la clase Usuario. También usamos la anotación @ExceptionHandler para manejar los errores de validación.

# Errores de enlace

Los errores de vinculación se pueden manejar mediante la anotación @ControllerAdvice. En el siguiente ejemplo, usamos la anotación @ControllerAdvice para manejar los errores de vinculación:

```java
@ControllerAdvice
public class BindingErrorHandler {

    @ExceptionHandler(BindException.class)
    public ResponseEntity<?> handleBindingErrors(BindException ex) {
        // ...
    }

}
```

En el ejemplo anterior, usamos la anotación @ExceptionHandler para controlar los errores de vinculación.

# Otros errores

Se pueden manejar otros tipos de errores usando la anotación @ExceptionHandler. En el siguiente ejemplo, usamos la anotación @ExceptionHandler para manejar los errores de la base de datos:

```java
@ControllerAdvice
public class DatabaseErrorHandler {

    @ExceptionHandler(DataAccessException.class)
    public ResponseEntity<?> handleDatabaseErrors(DataAccessException ex) {
        // ...
    }

}
```

En el ejemplo anterior, usamos la anotación @ExceptionHandler para manejar los errores de la base de datos.

# Conclusión

En este artículo, hemos visto cómo manejar los errores en Spring Boot. Comenzamos con una breve descripción general de los diferentes tipos de errores que pueden ocurrir y luego analizamos cómo manejarlos mediante la anotación @ControllerAdvice.