---
title: Validación de entrada con Spring Boot
description: 
published: true
date: 2023-02-07T04:32:29.101Z
tags: 
editor: markdown
dateCreated: 2023-02-07T04:32:27.466Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Validating Input with Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/validating-input-with-spring-boot)
{.links-list}


# Validación de entrada con Spring Boot

La validación de la entrada es una parte crítica de cualquier aplicación. No hacerlo puede dar lugar a todo tipo de problemas de seguridad y estabilidad.

Spring Boot proporciona varias formas de validar la entrada. En este artículo, veremos algunos de los métodos más populares.

## JSR-303

La solicitud de especificación de Java 303, o JSR-303, es una especificación para la validación en Java. Es una opción popular para la validación de entrada en aplicaciones Spring Boot.

Para usar JSR-303, primero debemos agregar la siguiente dependencia a nuestro `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

Entonces podemos crear un `@Controller` con una anotación `@Valid` en nuestro mapeo de solicitud:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

La anotación `@Valid` activará la validación de entrada. También podemos usar la anotación `@Validated` para activar la validación en campos específicos:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Validated({FirstGroup.class, SecondGroup.class}) @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

También podemos validar los argumentos del método:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @RequestParam("id") Long id) {
        // ...
    }

}
```

JSR-303 ofrece una serie de funciones potentes, pero puede ser bastante detallado.

## Validador de Hibernate

Hibernate Validator es un marco de validación compatible con JSR-303. Es una opción popular para la validación de entrada en aplicaciones Spring Boot.

Para usar Hibernate Validator, primero debemos agregar la siguiente dependencia a nuestro `pom.xml`:

```xml
<dependency>
    <groupId>org.hibernate</groupId>
    <artifactId>hibernate-validator</artifactId>
</dependency>
```

Entonces podemos crear un `@Controller` con una anotación `@Valid` en nuestro mapeo de solicitud:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

La anotación `@Valid` activará la validación de entrada. También podemos usar la anotación `@Validated` para activar la validación en campos específicos:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Validated({FirstGroup.class, SecondGroup.class}) @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

También podemos validar los argumentos del método:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @RequestParam("id") Long id) {
        // ...
    }

}
```

Hibernate Validator ofrece una serie de funciones potentes, pero puede ser bastante detallado.

## Validación de primavera

Spring Validation es un marco de validación que se basa en JSR-303 e Hibernate Validator. Es una opción popular para la validación de entrada en aplicaciones Spring Boot.

Para usar Spring Validation, primero debemos agregar la siguiente dependencia a nuestro `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```

Entonces podemos crear un `@Controller` con una anotación `@Valid` en nuestro mapeo de solicitud:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

La anotación `@Valid` activará la validación de entrada. También podemos usar la anotación `@Validated` para activar la validación en campos específicos:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Validated({FirstGroup.class, SecondGroup.class}) @ModelAttribute MyForm form, BindingResult bindingResult) {
        // ...
    }

}
```

También podemos validar los argumentos del método:

```java
@Controller
public class MyController {

    @RequestMapping("/")
    public String home(@Valid @RequestParam("id") Long id) {
        // ...
    }

}
```

Spring Validation ofrece una serie de funciones potentes, pero puede ser bastante detallado.

## Conclusión

Hay varias formas de validar la entrada en las aplicaciones Spring Boot. En este artículo, hemos analizado algunos de los métodos más populares.