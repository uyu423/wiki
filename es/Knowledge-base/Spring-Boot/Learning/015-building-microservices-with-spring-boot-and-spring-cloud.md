---
title: 015: Creación de microservicios con Spring Boot y Spring Cloud
description: 
published: true
date: 2023-02-03T09:36:34.539Z
tags: 
editor: markdown
dateCreated: 2023-02-03T09:36:32.952Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [015: Building microservices with Spring Boot and Spring Cloud***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/015-building-microservices-with-spring-boot-and-spring-cloud)
{.links-list}


# Introducción

Los microservicios son un estilo arquitectónico popular para crear aplicaciones nativas de la nube. Son unidades pequeñas y autónomas que se pueden implementar de forma independiente y se pueden combinar en aplicaciones complejas.

Spring Boot es un marco popular para crear microservicios. Facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción que se pueden "simplemente ejecutar".

Spring Cloud es un ecosistema de herramientas de código abierto para crear microservicios. Proporciona bibliotecas para patrones comunes utilizados en sistemas distribuidos, como descubrimiento de servicios, disyuntores y seguimiento distribuido.

En esta publicación, aprenderemos cómo crear microservicios con Spring Boot y Spring Cloud. Comenzaremos con un ejemplo simple de un microservicio "hola mundo", luego agregaremos el descubrimiento de servicios y el equilibrio de carga con Spring Cloud Netflix Eureka y Ribbon. Finalmente, agregaremos el rastreo distribuido con Spring Cloud Sleuth.

# Creación de un microservicio "Hello World"

Comencemos por crear un microservicio simple "hola mundo". Usaremos Spring Initializr para generar un proyecto con las siguientes dependencias:

- Internet
- Actuador

La dependencia web agrega soporte para crear aplicaciones web con Spring MVC. La dependencia Actuator agrega soporte para monitorear y administrar nuestra aplicación.

Una vez generado el proyecto, podemos abrirlo en nuestro IDE y agregar un controlador simple:

```java
@RestController
public class HelloController {

    @RequestMapping("/")
    public String hello() {
        return "Hello, world!";
    }

}
```

Este controlador tiene un punto final único que devuelve un "¡Hola, mundo!" mensaje.

Para ejecutar nuestra aplicación, podemos usar el complemento Spring Boot Maven:

```
./mvnw spring-boot:run
```

Una vez que la aplicación está en funcionamiento, podemos acceder al punto final "hello world" en http://localhost:8080/.

# Adición de detección de servicios

En una arquitectura de microservicios, los servicios generalmente se implementan en un grupo de nodos. Cuando se implementa un servicio, debe registrarse con un servidor de detección de servicios para que otros servicios puedan encontrarlo.

Spring Cloud Netflix Eureka es un popular servidor de descubrimiento de servicios. Para agregar Eureka a nuestro proyecto, podemos agregar la siguiente dependencia:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

Una vez que se agrega la dependencia, podemos habilitar el servidor Eureka agregando la anotación @EnableEurekaServer a nuestra clase de aplicación principal:

```java
@SpringBootApplication
@EnableEurekaServer
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

Ahora podemos iniciar nuestra aplicación y acceder al panel de Eureka en http://localhost:8761/.

# Adición de equilibrio de carga

En una arquitectura de microservicios, es común que un servicio se implemente en varios nodos. Cuando se invoca un servicio, se utiliza un balanceador de carga para enrutar la solicitud a uno de los nodos.

Spring Cloud Netflix Ribbon es un equilibrador de carga popular. Para agregar Ribbon a nuestro proyecto, podemos agregar la siguiente dependencia:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-ribbon</artifactId>
</dependency>
```

Una vez que se agrega la dependencia, podemos configurar Ribbon agregando la anotación @RibbonClient a nuestra clase de aplicación principal:

```java
@SpringBootApplication
@EnableEurekaServer
@RibbonClient(name = "hello-service")
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

Esta anotación configura un cliente Ribbon para el servicio "hello-service".

# Adición de seguimiento distribuido

En una arquitectura de microservicios, puede ser difícil solucionar problemas porque las solicitudes se pueden enrutar a través de múltiples servicios. El rastreo distribuido puede ayudar al rastrear las solicitudes a medida que fluyen por el sistema.

Spring Cloud Sleuth es un marco de seguimiento distribuido popular. Para agregar Sleuth a nuestro proyecto, podemos agregar la siguiente dependencia:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-sleuth</artifactId>
</dependency>
```

Una vez que se agrega la dependencia, Sleuth se configurará automáticamente para rastrear solicitudes.

# Conclusión

En esta publicación, hemos aprendido cómo crear microservicios con Spring Boot y Spring Cloud. Comenzamos con un simple microservicio "hola mundo" y agregamos detección de servicios, equilibrio de carga y seguimiento distribuido.