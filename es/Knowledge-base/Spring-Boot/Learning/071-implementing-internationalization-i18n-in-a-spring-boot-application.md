---
title: 071: Implementación de la internacionalización (i18n) en una aplicación Spring Boot
description: 
published: true
date: 2023-02-01T22:36:37.380Z
tags: 
editor: markdown
dateCreated: 2023-02-01T22:36:35.789Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [071: Implementing Internationalization (i18n) in a Spring Boot Application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/071-implementing-internationalization-i18n-in-a-spring-boot-application)
{.links-list}


# Implementando la internacionalización (i18n) en una aplicación Spring Boot

La internacionalización (i18n) es el proceso de hacer que su aplicación admita varios idiomas. Esta puede ser una tarea compleja, pero Spring Boot lo hace mucho más fácil. En esta publicación, veremos cómo implementar i18n en una aplicación Spring Boot.

## ¿Qué es i18n?

La internacionalización (i18n) es el proceso de hacer que su aplicación admita varios idiomas. Esta puede ser una tarea compleja, pero Spring Boot lo hace mucho más fácil.

## ¿Por qué usar i18n?

Hay muchas razones por las que podría querer agregar compatibilidad con i18n a su aplicación. Tal vez tengas usuarios en todo el mundo y quieras ofrecerles una experiencia localizada. O tal vez solo está creando un proyecto personal y desea aprender a agregar compatibilidad con i18n. Cualquiera que sea la razón, i18n es una habilidad valiosa para tener.

## Cómo implementar i18n en Spring Boot

Spring Boot facilita agregar compatibilidad con i18n a su aplicación. En esta sección, veremos cómo hacerlo.

### 1. Agregue las dependencias i18n

Primero, debe agregar las dependencias i18n a su archivo `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

### 2. Configurar las propiedades de i18n

A continuación, debe configurar las propiedades de i18n en su archivo `application.properties`:

```properties
spring.mvc.locale=en
spring.messages.basename=i18n/messages
```

### 3. Crea los archivos i18n

Ahora necesita crear los archivos i18n. Estos archivos contendrán los mensajes traducidos para su aplicación. Puede crear estos archivos en `src/main/resources/i18n`.

Por ejemplo, supongamos que desea admitir inglés y francés. Usted crearía los siguientes archivos:

- `mensajes_en.propiedades`
- `mensajes_fr.propiedades`

En estos archivos, definiría los mensajes traducidos para su aplicación. Por ejemplo:

```properties
# messages_en.properties

greeting=Hello
```

```properties
# messages_fr.properties

greeting=Bonjour
```

### 4. Usa los mensajes i18n en tu código

Ahora que tiene los archivos i18n configurados, puede usar los mensajes traducidos en su código. Por ejemplo, supongamos que tiene un controlador con el siguiente método:

```java
@RequestMapping("/greeting")
public String greeting(Model model) {
    model.addAttribute("message", "greeting");
    return "greeting";
}
```

Este método generará la plantilla `saludo.ftl` con el atributo `mensaje` establecido en la clave `saludo` de los archivos i18n. Entonces, si la propiedad `spring.mvc.locale` se establece en `en`, el atributo `message` se establecerá en `Hello`. Si la propiedad `spring.mvc.locale` se establece en `fr`, el atributo `message` se establecerá en `Bonjour`.

## Conclusión

En esta publicación, hemos visto cómo agregar compatibilidad con i18n a una aplicación Spring Boot. i18n puede ser una tarea compleja, pero Spring Boot lo hace mucho más fácil. Siguiendo los pasos de esta publicación, puede agregar soporte i18n a su aplicación con facilidad.