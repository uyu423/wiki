---
title: 029: Uso de Spring Boot con Apache Camel
description: 
published: true
date: 2023-02-03T21:32:17.006Z
tags: 
editor: markdown
dateCreated: 2023-02-03T21:32:15.351Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [029: Using Spring Boot with Apache Camel***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/029-using-spring-boot-with-apache-camel)
{.links-list}


# Uso de Spring Boot con Apache Camel

Con el lanzamiento de Camel 2.0, se introdujo un nuevo conjunto de anotaciones para facilitar el uso de Camel con Spring Framework. En esta publicación, veremos cómo usar Spring Boot con Camel.

Comenzaremos con un ejemplo simple que enruta una solicitud HTTP a un registro. Primero, necesitaremos agregar las siguientes dependencias a nuestro `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-spring-boot-starter</artifactId>
    <version>2.22.0</version>
</dependency>
```

Ahora podemos crear una clase `@Configuration` que configura Camel:

```java
@Configuration
public class MyRouteBuilder extends RouteBuilder {

    @Override
    public void configure() {
        from("jetty:http://0.0.0.0:8080/myapp")
            .to("log:requests");
    }
}
```

Finalmente, necesitaremos un archivo `application.properties` para configurar el servidor Jetty:

```properties
server.port=8080
```

¡Eso es todo! Ahora podemos ejecutar nuestra aplicación y presionar `http://localhost:8080/myapp` con un navegador o `curl`. Deberíamos ver la solicitud registrada en la consola.

Por supuesto, este ejemplo es muy simple. Camel proporciona una gran cantidad de componentes que se pueden usar para crear aplicaciones más complejas. Para obtener más información sobre el uso de Camel con Spring Boot, consulte la [documentación] (http://camel.apache.org/spring-boot.html).