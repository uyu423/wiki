---
title: 008: Creación y uso de plantillas con Thymeleaf
description: 
published: true
date: 2023-02-03T08:17:34.664Z
tags: 
editor: markdown
dateCreated: 2023-02-03T08:17:33.080Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [008: Creating and using templates with Thymeleaf***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/008-creating-and-using-templates-with-thymeleaf)
{.links-list}


# Introducción

En esta publicación, discutiremos cómo crear y usar plantillas con Thymeleaf.

Thymeleaf es un moderno motor de plantillas Java del lado del servidor que nos permite crear HTML, XML y otros lenguajes de marcado de una manera bien formada y estructurada.

Es un proyecto de código abierto que tiene la licencia Apache License 2.0.

# ¿Qué es una plantilla?

Una plantilla es un archivo que contiene las partes estáticas de su sitio web o aplicación, así como variables de marcador de posición para contenido dinámico.

Un motor de plantillas es una herramienta que toma sus archivos de plantilla estáticos y reemplaza las variables de marcador de posición con valores reales, lo que da como resultado un archivo que se puede servir a un usuario.

# ¿Por qué usar plantillas?

Las plantillas son una excelente manera de separar las partes estáticas de su sitio web o aplicación de las partes dinámicas.

Esta separación facilita la administración de su código, así como la realización de cambios en las partes estáticas de su sitio sin afectar el contenido dinámico.

También facilita el almacenamiento en caché de las partes estáticas de su sitio, lo que puede mejorar el rendimiento.

# ¿Qué es la hoja de tomillo?

Thymeleaf es un motor de plantillas para Java.

Es un proyecto de código abierto que tiene la licencia Apache License 2.0.

Thymeleaf nos permite crear HTML, XML y otros lenguajes de marcado de forma bien formada y estructurada.

También tiene un excelente soporte para internacionalización (i18n) y localización (l10n).

Thymeleaf se usa en muchos marcos web populares de Java, como Spring MVC, Spring Boot y Vaadin.

# Sintaxis de hoja de tomillo

Thymeleaf tiene dos tipos de sintaxis: estándar y OGNL.

La sintaxis estándar es el modo de sintaxis predeterminado y se utiliza para crear HTML, XML y otros lenguajes de marcas bien formados y estructurados.

La sintaxis OGNL es una extensión de la sintaxis estándar y se utiliza para acceder a objetos en el contexto de Thymeleaf.

# Crear una plantilla

Podemos crear una plantilla de Thymeleaf en cualquier editor de texto.

Para este ejemplo, crearemos una plantilla llamada "hello.html" en el directorio src/main/resources/templates.

hola.html

```html
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Hello, World!</title>
</head>
<body>
    <p th:text="${message}">Hello, World!</p>
</body>
</html>
```

En la plantilla anterior, tenemos una variable llamada "mensaje" que se reemplazará con un valor cuando se procese la plantilla.

# Representar una plantilla

Podemos representar una plantilla de Thymeleaf en una aplicación Java utilizando la clase ThymeleafTemplateEngine.

Primero, necesitamos crear una instancia de ThymeleafTemplateEngine:

```java
ThymeleafTemplateEngine templateEngine = new ThymeleafTemplateEngine();
```

Luego, podemos representar la plantilla pasando el nombre de la plantilla y un mapa de variables al método renderTemplate():

```java
String result = templateEngine.renderTemplate("hello.html", ImmutableMap.of("message", "Hello, World!"));
```

# Conclusión

En esta publicación, hemos aprendido cómo crear y usar plantillas con Thymeleaf.

También hemos aprendido acerca de los diferentes tipos de sintaxis que admite Thymeleaf.

Si desea obtener más información sobre Thymeleaf, consulte los siguientes recursos:

- El sitio web de Thymeleaf: https://www.thymeleaf.org/
- El repositorio Thymeleaf GitHub: https://github.com/thymeleaf/thymeleaf
- La guía del usuario de Thymeleaf: https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html