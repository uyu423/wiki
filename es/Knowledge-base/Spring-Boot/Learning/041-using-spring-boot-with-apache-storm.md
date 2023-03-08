---
title: 041: Uso de Spring Boot con Apache Storm
description: 
published: true
date: 2023-02-04T07:32:19.549Z
tags: 
editor: markdown
dateCreated: 2023-02-04T07:32:17.924Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [041: Using Spring Boot with Apache Storm***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/041-using-spring-boot-with-apache-storm)
{.links-list}


# Uso de Spring Boot con Apache Storm

En esta publicación, aprenderemos cómo usar Spring Boot con Apache Storm. Cubriremos los siguientes temas:

* ¿Qué es Apache Storm?
* ¿Qué es Spring Boot?
* Cómo usar Spring Boot con Apache Storm

## ¿Qué es Apache Storm?

Apache Storm es un sistema de computación en tiempo real distribuido gratuito y de código abierto. Storm facilita el procesamiento confiable de flujos ilimitados de datos, haciendo para el procesamiento en tiempo real lo que Hadoop hizo para el procesamiento por lotes.

¡Storm es simple, se puede usar con cualquier lenguaje de programación y es muy divertido de usar!

## ¿Qué es Spring Boot?

Spring Boot es un marco para crear fácilmente aplicaciones basadas en Spring independientes y de grado de producción que puede "simplemente ejecutar". Tomamos una opinión obstinada de la plataforma Spring y las bibliotecas de terceros para que pueda comenzar con el mínimo esfuerzo. La mayoría de las aplicaciones de Spring Boot necesitan muy poca configuración de Spring.

## Cómo usar Spring Boot con Apache Storm

Ahora que sabemos qué son Storm y Spring Boot, veamos cómo usarlos juntos.

Lo primero que necesitamos es una dependencia de Maven para Storm:

```xml
<dependency>
    <groupId>org.apache.storm</groupId>
    <artifactId>storm-core</artifactId>
    <version>1.1.1</version>
    <scope>provided</scope>
</dependency>
```

También necesitamos una dependencia para Spring Boot:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

Ahora podemos crear una aplicación Spring Boot:

```java
@SpringBootApplication
public class StormApplication {

    public static void main(String[] args) {
        SpringApplication.run(StormApplication.class, args);
    }

}
```

Ahora podemos crear una topología Storm en nuestra aplicación:

```java
@Component
public class MyTopology {

    @Autowired
    private TopologyBuilder topologyBuilder;

    @PostConstruct
    public void init() {
        // ...
    }

}
```

¡Y eso es! Ahora tenemos una topología Storm en funcionamiento dentro de nuestra aplicación Spring Boot.

## Información adicional

* Para obtener más información sobre Apache Storm, consulte el [sitio web de Apache Storm] (https://storm.apache.org/).
* Para obtener más información sobre Spring Boot, consulte el [sitio web de Spring Boot] (https://projects.spring.io/spring-boot/).