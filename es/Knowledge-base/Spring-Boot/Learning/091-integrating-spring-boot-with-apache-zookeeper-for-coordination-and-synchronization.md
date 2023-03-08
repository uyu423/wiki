---
title: 091: Integración de Spring Boot con Apache Zookeeper para coordinación y sincronización
description: 
published: true
date: 2023-02-05T21:32:22.382Z
tags: 
editor: markdown
dateCreated: 2023-02-05T21:32:20.811Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [091: Integrating Spring Boot with Apache Zookeeper for Coordination and Synchronization***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/091-integrating-spring-boot-with-apache-zookeeper-for-coordination-and-synchronization)
{.links-list}


# 091: Integrando Spring Boot con Apache Zookeeper para Coordinación y Sincronización

Apache Zookeeper es un servicio de coordinación distribuida para sistemas distribuidos. Se utiliza para gestionar grandes sistemas distribuidos. Spring Boot es un marco Java popular para desarrollar microservicios.

En esta publicación, aprenderemos cómo integrar Spring Boot con Apache Zookeeper. Usaremos Zookeeper para coordinar y sincronizar nuestros microservicios Spring Boot.

## Instalación de Apache Zookeeper

Antes de que podamos comenzar a usar Zookeeper, debemos instalarlo. Podemos instalar Zookeeper usando Homebrew en macOS:

```
$ brew install zookeeper
```

O podemos descargar la versión binaria de Zookeeper desde el [sitio web de Apache Zookeeper] (https://zookeeper.apache.org/).

## Iniciando Apache Zookeeper

Una vez instalado Zookeeper, podemos iniciarlo usando el siguiente comando:

```
$ zookeeper-server-start /usr/local/etc/kafka/zookeeper.properties
```

## Creación de un proyecto Spring Boot

Podemos crear un proyecto Spring Boot usando [Spring Initializr](https://start.spring.io/). Usaremos las siguientes dependencias:

* Internet
* Actuador
* Lombok

## Configuración de Spring Boot

Necesitamos configurar nuestra aplicación Spring Boot para usar Zookeeper. Podemos hacer esto agregando las siguientes propiedades a nuestro archivo `application.properties`:

```properties
spring.cloud.zookeeper.connect-string=localhost:2181
spring.cloud.zookeeper.discovery.instance-id=${spring.application.name}
spring.cloud.zookeeper.discovery.root=/${spring.application.name}
spring.cloud.zookeeper.discovery.service-name=${spring.application.name}
spring.cloud.zookeeper.discovery.enabled=true
```

## Creación de un servicio Spring Boot

Podemos crear un servicio Spring Boot usando la anotación `@SpringBootApplication`:

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## Agregar un controlador de descanso

Podemos agregar un controlador Rest a nuestro servicio usando la anotación `@RestController`:

```java
@RestController
public class GreetingController {

    @GetMapping("/greeting")
    public String greeting() {
        return "Hello, world!";
    }

}
```

## Probando el Servicio

Podemos probar nuestro servicio enviando una solicitud `GET` al punto final `/saludo`:

```
$ curl localhost:8080/greeting
Hello, world!
```

## Registrando el Servicio con Zookeeper

Una vez que nuestro servicio esté en funcionamiento, debemos registrarlo con Zookeeper. Podemos hacer esto usando la anotación `@DiscoveryClient`:

```java
@SpringBootApplication
@DiscoveryClient
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

## Acceso al Servicio desde otro Servicio

Una vez registrado nuestro servicio en Zookeeper, podemos acceder a él desde otro servicio. Podemos hacer esto inyectando un `DiscoveryClient` en nuestro controlador:

```java
@RestController
public class GreetingController {

    @Autowired
    private DiscoveryClient discoveryClient;

    @GetMapping("/greeting")
    public String greeting() {
        List<ServiceInstance> instances = discoveryClient.getInstances("greeting-service");
        if (instances.isEmpty()) {
            return "Hello, world!";
        }
        String url = instances.get(0).getUri().toString();
        return "Hello, world! (from " + url + ")";
    }

}
```

## Conclusión

En esta publicación, aprendimos cómo integrar Spring Boot con Apache Zookeeper. Usamos Zookeeper para coordinar y sincronizar nuestros microservicios Spring Boot.