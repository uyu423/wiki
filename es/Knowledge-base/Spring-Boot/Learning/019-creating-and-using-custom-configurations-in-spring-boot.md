---
title: 019: Creación y uso de configuraciones personalizadas en Spring Boot
description: 
published: true
date: 2023-02-03T11:32:32.385Z
tags: 
editor: markdown
dateCreated: 2023-02-03T11:32:30.811Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [019: Creating and using custom configurations in Spring Boot***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/019-creating-and-using-custom-configurations-in-spring-boot)
{.links-list}


# Creación y uso de configuraciones personalizadas en Spring Boot

Al desarrollar una aplicación Spring Boot, es posible que deba crear y usar configuraciones personalizadas. Esto se puede hacer creando un archivo llamado `application.yml` en la carpeta `src/main/resources`.

En este archivo, puede especificar cualquier valor de configuración personalizado. Por ejemplo, podría especificar el puerto en el que se ejecutará su aplicación:

```yaml
server:
  port: 8080
```

También puede especificar múltiples valores de configuración bajo una sola clave. Por ejemplo, podría especificar tanto el puerto como la ruta de contexto:

```yaml
server:
  port: 8080
  context-path: /myapp
```

Si necesita usar más de un archivo de configuración, puede especificar los archivos que se cargarán usando la propiedad `spring.config.location`:

```yaml
spring:
  config:
    location: classpath:application.yml,classpath:custom.yml
```

En el ejemplo anterior, el archivo `application.yml` se cargará primero, seguido del archivo `custom.yml`.

También es posible especificar la propiedad `spring.config.location` utilizando propiedades del sistema o variables de entorno. Por ejemplo, podría establecer la propiedad del sistema `spring.config.location` al iniciar su aplicación:

```
java -jar myapp.jar --spring.config.location=classpath:application.yml,classpath:custom.yml
```

Alternativamente, puede configurar la variable de entorno `SPRING_CONFIG_LOCATION`:

```
SPRING_CONFIG_LOCATION=classpath:application.yml,classpath:custom.yml java -jar myapp.jar
```

## Especificando valores de configuración

Hay muchas formas de especificar valores de configuración en Spring Boot. La forma más común es usar el archivo `application.yml`, como se muestra en la sección anterior.

Otra forma de especificar los valores de configuración es utilizar las propiedades del sistema o las variables de entorno. Por ejemplo, podría establecer la propiedad del sistema `server.port` al iniciar su aplicación:

```
java -jar myapp.jar --server.port=8080
```

Alternativamente, puede configurar la variable de entorno `SERVER_PORT`:

```
SERVER_PORT=8080 java -jar myapp.jar
```

También puede especificar valores de configuración utilizando las propiedades del sistema Java. Por ejemplo, podría establecer la propiedad del sistema `server.port` en su archivo `application.yml`:

```yaml
server:
  port: ${SERVER_PORT}
```

## Acceder a los valores de configuración

Una vez que haya especificado sus valores de configuración, puede acceder a ellos en su código usando la anotación `@Value`:

```java
@Value("${server.port}")
private int port;
```

En el ejemplo anterior, la variable `port` se completará con el valor de la propiedad de configuración `server.port`.

Si necesita acceder a múltiples valores de configuración, puede crear una clase anotada `@ConfigurationProperties`:

```java
@ConfigurationProperties(prefix = "server")
public class ServerProperties {

    private int port;
    private String contextPath;

    // getters and setters
}
```

En el ejemplo anterior, las variables `port` y `contextPath` se completarán con los valores de las propiedades de configuración `server.port` y `server.context-path`, respectivamente.

Luego puede inyectar una instancia de la clase `ServerProperties` en su código:

```java
@Autowired
private ServerProperties serverProperties;
```

## Conclusión

En este artículo, ha aprendido a crear y usar configuraciones personalizadas en Spring Boot. También aprendió cómo especificar valores de configuración y cómo acceder a ellos en su código.