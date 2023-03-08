---
title: Depuración con Spring Boot DevTools
description: 
published: true
date: 2023-02-07T02:32:31.447Z
tags: 
editor: markdown
dateCreated: 2023-02-07T02:32:29.840Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Debugging with Spring Boot DevTools***English** document is available*](/en/Knowledge-base/Spring-Boot/debugging-with-spring-boot-devtools)
{.links-list}


# Depuración con Spring Boot DevTools

Spring Boot viene con una serie de excelentes funciones para ayudar a los desarrolladores con sus aplicaciones. DevTools es una de esas características. Puede ayudar con la depuración, la recarga y más.

## ¿Qué es DevTools?

DevTools es un conjunto de herramientas que pueden ayudar con el desarrollo. Puede hacer cosas como recargar su aplicación sin reiniciar el servidor y reiniciar automáticamente el servidor cuando se cambian los archivos. También puede ayudar con la depuración, permitiéndole depurar su aplicación en su IDE.

## Configuración de herramientas de desarrollo

Para usar DevTools, deberá agregarlo a su proyecto. Puede hacer esto agregándolo a sus dependencias. Por ejemplo, en Maven, lo agregaría a su `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
    </dependency>
</dependencies>
```

O, si está usando Gradle, lo agregaría a su `build.gradle`:

```groovy
dependencies {
    compile 'org.springframework.boot:spring-boot-devtools'
}
```

## Uso de las herramientas de desarrollo

Una vez que haya configurado DevTools en su proyecto, puede comenzar a usarlo.

### Recargando su aplicación

Una de las características más útiles de DevTools es la capacidad de recargar su aplicación sin reiniciar el servidor. Para hacer esto, simplemente presione `Ctrl+F9` (o `Cmd+F9` en macOS) en su IDE. Esto activará un reinicio completo de su aplicación.

Si solo desea reiniciar el servidor, puede presionar `Ctrl+Shift+F9` (o `Cmd+Shift+F9` en macOS). Esto solo reiniciará el servidor y no la aplicación.

### Depurando tu aplicación

Otra característica útil de DevTools es la capacidad de depurar su aplicación en su IDE. Para hacer esto, debe iniciar su aplicación en modo de depuración. Puede hacer esto pasando el indicador `--debug` a la CLI `spring-boot`:

```
$ spring-boot --debug
```

O bien, puede establecer la propiedad `spring.boot.debug` en su `application.properties`:

```properties
spring.boot.debug=true
```

Una vez que su aplicación se ejecuta en modo de depuración, puede adjuntarle un depurador. Por ejemplo, en IntelliJ IDEA, puede hacer esto yendo a `Ejecutar > Adjuntar depurador al proceso local`.

## Conclusión

DevTools es una gran herramienta que puede ayudar con el desarrollo. Puede hacer cosas como recargar su aplicación sin reiniciar el servidor y reiniciar automáticamente el servidor cuando se cambian los archivos. También puede ayudar con la depuración, permitiéndole depurar su aplicación en su IDE.