---
title: 070: Spring Boot con Thymeleaf: creación de plantillas dinámicas
description: 
published: true
date: 2023-02-05T04:32:34.610Z
tags: 
editor: markdown
dateCreated: 2023-02-05T04:32:32.931Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [070: Spring Boot with Thymeleaf: Creating Dynamic Templates***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/070-spring-boot-with-thymeleaf-creating-dynamic-templates)
{.links-list}


# 070: Spring Boot con Thymeleaf: Creando Plantillas Dinámicas

En esta publicación, veremos cómo usar el motor de plantillas de Thymeleaf con Spring Boot para crear páginas HTML dinámicas.

Thymeleaf es un motor de plantillas popular que se puede usar con Spring MVC para crear aplicaciones web elegantes y dinámicas. El objetivo principal de Thymeleaf es traer plantillas naturales a los entornos de desarrollo.

## ¿Qué es la hoja de tomillo?

Thymeleaf es una biblioteca basada en Java que proporciona un conjunto de herramientas para trabajar con XML y HTML. El objetivo principal de Thymeleaf es traer plantillas naturales a los entornos de desarrollo.

El enfoque de Thymeleaf para las plantillas es diferente al enfoque tradicional adoptado por otros motores de plantillas. Con Thymeleaf, las plantillas no se "rellenan" simplemente con datos. En su lugar, las plantillas de Thymeleaf se procesan y convierten en documentos HTML válidos.

Esto significa que las plantillas de Thymeleaf se pueden usar como punto de partida para la interfaz de usuario de su aplicación web y se pueden integrar fácilmente con el back-end de su aplicación.

## Empezando

Para comenzar con Thymeleaf, deberá agregar la siguiente dependencia al archivo pom.xml de su proyecto:

```xml
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf</artifactId>
    <version>3.0.9.RELEASE</version>
</dependency>
```

## ¡Hola, hoja de tomillo!

Ahora que hemos configurado Thymeleaf, creemos una plantilla simple para verlo en acción.

Cree un nuevo archivo llamado `hello.html` en el directorio `src/main/resources/templates` y agregue el siguiente contenido:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello, Thymeleaf!</title>
</head>
<body>
    <h1>Hello, Thymeleaf!</h1>
</body>
</html>
```

Esta plantilla contiene un simple elemento `<h1>` que dice "¡Hola, Thymeleaf!".

A continuación, creemos una aplicación Spring Boot que represente esta plantilla.

Cree un nuevo archivo llamado `Application.java` en el directorio `src/main/java` y agregue el siguiente contenido:

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

Esta es una aplicación Spring Boot básica. La anotación `@SpringBootApplication` se usa para marcar la clase de aplicación como una aplicación Spring Boot.

A continuación, vamos a crear un controlador que represente la plantilla `hello.html`.

Cree un nuevo archivo llamado `HelloController.java` en el directorio `src/main/java` y agregue el siguiente contenido:

```java
@Controller
public class HelloController {

    @RequestMapping("/")
    public String hello(Model model) {
        model.addAttribute("message", "Hello, Thymeleaf!");
        return "hello";
    }

}
```

Este controlador tiene un único método anotado `@RequestMapping`. Este método asigna la URL `/` a la plantilla `hello`.

La plantilla `hola` espera que el atributo `mensaje` esté presente en el modelo. Este atributo se agrega al modelo mediante el método `hola`.

Ahora que tenemos nuestro controlador y plantilla configurados, ejecutemos nuestra aplicación y veamos los resultados.

Ejecute la clase `Application` como una aplicación Java y navegue hasta http://localhost:8080 en su navegador. Debería ver el siguiente resultado:

![¡Hola, Thymeleaf!](https://i.imgur.com/ePcUg9x.png)

Como puede ver, nuestra plantilla se representó y el atributo `message` se usó para completar el elemento `<h1>`.

## Pasar datos a plantillas

En la sección anterior, vimos cómo pasar datos a una plantilla usando el objeto `Modelo`.

El objeto 'Modelo' es una estructura similar a un mapa que se puede usar para almacenar datos que deben pasarse a una plantilla.

Además del objeto 'Modelo', Thymeleaf también proporciona el objeto 'Contexto'. El objeto 'Contexto' es una versión más potente del objeto 'Modelo' que proporciona funciones adicionales, como seguridad de tipo y compatibilidad con la internacionalización.

Veremos cómo usar el objeto `Context` en la siguiente sección.

## Uso del objeto de contexto

Como vimos en la sección anterior, el objeto 'Modelo' es una estructura similar a un mapa que se puede usar para almacenar datos que deben pasarse a una plantilla.

El objeto 'Contexto' es una versión más potente del objeto 'Modelo' que proporciona funciones adicionales, como seguridad de tipo y compatibilidad con la internacionalización.

Para usar el objeto `Context`, necesitamos agregar la siguiente dependencia al archivo pom.xml de nuestro proyecto:

```xml
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf-extras-java8time</artifactId>
    <version>3.0.4.RELEASE</version>
</dependency>
```

Esta dependencia proporciona soporte para el objeto `Context`.

A continuación, vamos a crear una plantilla que utilice el objeto `Contexto`.

Cree un nuevo archivo llamado `context.html` en el directorio `src/main/resources/templates` y agregue el siguiente contenido:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Context Example</title>
</head>
<body>
    <h1 th:text="${message}"></h1>
</body>
</html>
```

Esta plantilla contiene un elemento `<h1>` que usa el atributo `message` del objeto `Context`.

A continuación, creemos un controlador que represente esta plantilla.

Cree un nuevo archivo llamado `ContextController.java` en el directorio `src/main/java` y agregue el siguiente contenido:

```java
@Controller
public class ContextController {

    @RequestMapping("/")
    public String context(Context context) {
        context.setVariable("message", "Hello, Thymeleaf!");
        return "context";
    }

}
```

Este controlador tiene un único método anotado `@RequestMapping`. Este método asigna la URL `/` a la plantilla `context`.

La plantilla `contexto` espera que un atributo `mensaje` esté presente en el objeto `Contexto`. Este atributo se agrega al objeto `Context` mediante el método `context`.

Ahora que tenemos nuestro controlador y plantilla configurados, ejecutemos nuestra aplicación y veamos los resultados.

Ejecute la clase `Application` como una aplicación Java y navegue hasta http://localhost:8080 en su navegador. Debería ver el siguiente resultado:

![¡Hola, Thymeleaf!](https://i.imgur.com/ePcUg9x.png)

Como puede ver, nuestra plantilla se representó y el atributo `message` se usó para completar el elemento `<h1>`.

## Conclusión

En esta publicación, hemos visto cómo usar el motor de plantillas de Thymeleaf con Spring Boot para crear páginas HTML dinámicas.

También hemos visto cómo usar los objetos 'Modelo' y 'Contexto' para pasar datos a las plantillas.

Thymeleaf es un potente motor de plantillas que se puede utilizar para crear aplicaciones web dinámicas y sofisticadas.