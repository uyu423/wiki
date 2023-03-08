---
title: 096: Implementación de un sistema de manejo de errores personalizado en Spring Boot
description: 
published: true
date: 2023-02-06T01:32:35.398Z
tags: 
editor: markdown
dateCreated: 2023-02-06T01:32:33.711Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [096: Implementing a Custom Error Handling System in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/096-implementing-a-custom-error-handling-system-in-spring-boot)
{.links-list}


# Implementando un Sistema de Manejo de Errores Personalizado en Spring Boot

Es importante contar con un sistema de manejo de errores completo y bien definido para cualquier aplicación web. Esto es especialmente cierto para las aplicaciones creadas con el marco Spring Boot.

En esta publicación, veremos cómo implementar un sistema de manejo de errores personalizado en Spring Boot. Cubriremos los siguientes temas:

1. ¿Qué es Spring Boot?
2. ¿Cuáles son los beneficios de usar Spring Boot?
3. ¿Cuáles son las características del framework Spring Boot?
4. ¿Cómo implementar un sistema de manejo de errores personalizado en Spring Boot?

## ¿Qué es Spring Boot?

Spring Boot es un marco basado en Java que se utiliza para crear microservicios y aplicaciones web. Está desarrollado por Pivotal Software y es miembro de la familia Spring de frameworks.

Spring Boot está diseñado para simplificar el proceso de creación e implementación de aplicaciones basadas en Spring. Proporciona una serie de funciones, como la configuración automática y las plantillas de inicio, que facilitan el inicio de Spring.

## ¿Cuáles son los beneficios de usar Spring Boot?

Hay una serie de beneficios al usar Spring Boot, incluidos los siguientes:

- Spring Boot facilita la creación de aplicaciones basadas en Spring independientes y de nivel de producción.
- Spring Boot proporciona una serie de funciones, como la configuración automática y las plantillas de inicio, que facilitan el inicio de Spring.
- Spring Boot es obstinado, lo que significa que proporciona un conjunto de valores predeterminados que son adecuados para la mayoría de las aplicaciones. Esto hace que sea más fácil comenzar con Spring Boot, ya que no tiene que preocuparse por configurar todo usted mismo.

## ¿Cuáles son las características del framework Spring Boot?

Spring Boot proporciona una serie de funciones que lo convierten en una opción atractiva para crear microservicios y aplicaciones web. Estas características incluyen:

- Configuración automática: Spring Boot configura automáticamente beans y propiedades en función de las dependencias que encuentra en el classpath. Esto hace que sea más fácil comenzar con Spring Boot, ya que no tiene que preocuparse por configurar todo usted mismo.
- Plantillas de inicio: Spring Boot proporciona una serie de plantillas de inicio que se pueden usar para crear un nuevo proyecto. Estas plantillas de inicio incluyen todo lo que necesita para comenzar, como las dependencias y los scripts de compilación.
- Interfaz de línea de comandos: Spring Boot incluye una interfaz de línea de comandos que se puede usar para ejecutar comandos, como iniciar y detener la aplicación.
- Actuador: Spring Boot incluye un actuador que se puede usar para monitorear y administrar la aplicación.

## ¿Cómo implementar un sistema de manejo de errores personalizado en Spring Boot?

Hay varias formas de implementar un sistema de manejo de errores personalizado en Spring Boot. En esta sección, veremos dos de los enfoques más comunes:

- Usando una anotación @ControllerAdvice
- Crear un controlador de errores personalizado

### Usar una anotación @ControllerAdvice

Una forma de implementar un sistema de manejo de errores personalizado en Spring Boot es usar la anotación @ControllerAdvice. Esta anotación se puede utilizar para definir un controlador de errores global para todos los controladores de la aplicación.

El siguiente es un ejemplo de cómo usar la anotación @ControllerAdvice:

```java
@ControllerAdvice
public class GlobalExceptionHandler {
 
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ErrorResponse> handleException(Exception ex) {
 
        ErrorResponse error = new ErrorResponse();
        error.setMessage(ex.getMessage());
        error.setStatusCode(HttpStatus.INTERNAL_SERVER_ERROR.value());
 
        return new ResponseEntity<>(error, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

En el ejemplo anterior, hemos definido un controlador de errores global que se invocará para todas las excepciones. Este controlador creará una instancia de la clase ErrorResponse y la devolverá al cliente.

### Creación de un controlador de errores personalizado

Otra forma de implementar un sistema de manejo de errores personalizado en Spring Boot es crear un controlador de errores personalizado. Este controlador se puede usar para manejar errores para controladores específicos en la aplicación.

El siguiente es un ejemplo de cómo crear un controlador de errores personalizado:

```java
@RestController
public class ErrorController extends AbstractErrorController {
 
    @Override
    public String getErrorPath() {
        return "/error";
    }
 
    @RequestMapping("/error")
    public ResponseEntity<ErrorResponse> error(HttpServletRequest request) {
 
        ErrorResponse error = new ErrorResponse();
        error.setMessage(request.getAttribute("javax.servlet.error.message").toString());
        error.setStatusCode(Integer.valueOf(request.getAttribute("javax.servlet.error.status_code").toString()));
 
        return new ResponseEntity<>(error, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

En el ejemplo anterior, hemos definido un controlador de errores personalizado que se invocará para todas las solicitudes que den como resultado un error. Este controlador creará una instancia de la clase ErrorResponse y la devolverá al cliente.

## Conclusión

En esta publicación, hemos analizado cómo implementar un sistema de manejo de errores personalizado en Spring Boot. Hemos cubierto los siguientes temas:

1. ¿Qué es Spring Boot?
2. ¿Cuáles son los beneficios de usar Spring Boot?
3. ¿Cuáles son las características del framework Spring Boot?
4. ¿Cómo implementar un sistema de manejo de errores personalizado en Spring Boot?