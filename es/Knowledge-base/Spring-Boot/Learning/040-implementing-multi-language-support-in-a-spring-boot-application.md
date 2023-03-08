---
title: 040: Implementación de compatibilidad con varios idiomas en una aplicación Spring Boot
description: 
published: true
date: 2023-02-02T04:04:27.130Z
tags: 
editor: markdown
dateCreated: 2023-02-02T04:04:25.500Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [040: Implementing multi-language support in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/040-implementing-multi-language-support-in-a-spring-boot-application)
{.links-list}



# Implementación de soporte multilingüe en una aplicación Spring Boot

La internacionalización (i18n) es el proceso de desarrollar productos o servicios que se pueden adaptar a idiomas y culturas locales específicos, un proceso conocido como localización (l10n).

Spring Boot facilita agregar compatibilidad con i18n a su aplicación con la ayuda de los iniciadores `spring-boot-starter-data-jpa` y `spring-boot-starter-thymeleaf`.

En esta publicación, veremos cómo agregar compatibilidad con i18n a una aplicación Spring Boot. Cubriremos los siguientes temas:

* Configuración de Spring Boot para i18n
* Creación de archivos de mensajes específicos del idioma
* Mostrar mensajes localizados en sus vistas
* Cambio de idioma en su aplicación

## Configuración de Spring Boot para i18n

Primero, necesitamos agregar los iniciadores `spring-boot-starter-data-jpa` y `spring-boot-starter-thymeleaf` a nuestro `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-thymeleaf</artifactId>
    </dependency>
</dependencies>
```

A continuación, debemos configurar el bean `MessageSource` en nuestro archivo `application.properties`:

```properties
spring.messages.basename=messages
```

El bean `MessageSource` es responsable de resolver los mensajes de los archivos de mensajes. De forma predeterminada, Spring Boot buscará archivos de mensajes en el directorio `src/main/resources`.

## Creación de archivos de mensajes específicos del idioma

A continuación, debemos crear archivos de mensajes para cada idioma que queramos admitir. El archivo de mensajes debe llamarse `messages_[lang].properties`, donde `[lang]` es el código [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) para el idioma. .

Por ejemplo, si quisiéramos admitir inglés y francés, crearíamos los siguientes archivos de mensajes:

* `messages_en.properties`
* `messages_fr.properties`

Cada archivo de mensaje contendrá pares clave-valor para cada mensaje que puede resolver el bean `MessageSource`. Por ejemplo, nuestro archivo `messages_en.properties` podría verse así:

```properties
greeting=Hello, world!
```

Y nuestro archivo `messages_fr.properties` podría verse así:

```properties
greeting=Bonjour, monde!
```

## Mostrar mensajes localizados en sus vistas

Ahora que tenemos nuestros archivos de mensajes configurados, podemos comenzar a mostrar mensajes localizados en nuestras vistas.

En Thymeleaf, podemos usar la sintaxis `# {.links-list}` para resolver mensajes de nuestros archivos de mensajes. Por ejemplo, si quisiéramos mostrar el mensaje `saludo` de nuestro archivo `messages_en.properties`, podríamos hacer lo siguiente:

```html
<p th:text="#{greeting}">Hello, world!</p>
```

Si quisiéramos mostrar el mensaje de `saludo` de nuestro archivo `messages_fr.properties`, podríamos hacer lo siguiente:

```html
<p th:text="#{greeting}">Bonjour, monde!</p>
```

## Cambiar de idioma en tu aplicación

Ahora que podemos mostrar mensajes localizados en nuestras vistas, necesitamos una forma de cambiar entre idiomas.

Hay muchas maneras de hacer esto, pero una forma simple es agregar un parámetro `lang` a `queryString` de nuestra aplicación. Por ejemplo, si quisiéramos cambiar al idioma francés, podríamos hacer lo siguiente:

```
http://localhost:8080/?lang=fr
```

Luego podemos usar el parámetro `lang` para establecer `Locale` en nuestro bean `LocaleResolver`. Por ejemplo, podríamos agregar lo siguiente a nuestro archivo `application.properties`:

```properties
spring.mvc.locale-resolver=org.springframework.web.servlet.i18n.SessionLocaleResolver
```

Y luego agregue lo siguiente a nuestro bean `LocaleResolver`:

```java
@Bean
public LocaleResolver localeResolver() {
    SessionLocaleResolver localeResolver = new SessionLocaleResolver();
    localeResolver.setDefaultLocale(Locale.ENGLISH);
    return localeResolver;
}
```

Ahora, cuando visitemos `http://localhost:8080/?lang=fr`, nuestra aplicación cambiará al idioma francés y mostrará el mensaje de `saludo` de nuestro archivo `messages_fr.properties`.

## Conclusión

En esta publicación, hemos cubierto cómo agregar soporte i18n a una aplicación Spring Boot. Hemos visto cómo configurar Spring Boot para i18n, cómo crear archivos de mensajes específicos del idioma, cómo mostrar mensajes localizados en nuestras vistas y cómo cambiar de idioma en nuestra aplicación.