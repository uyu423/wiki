---
title: Microservicios Spring Boot con Netflix OSS
description: 
published: true
date: 2023-02-08T00:32:55.372Z
tags: 
editor: markdown
dateCreated: 2023-02-08T00:32:53.649Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Spring Boot Microservices with Netflix OSS***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-microservices-with-netflix-oss)
{.links-list}


# Microservicios Spring Boot con Netflix OSS

En el pasado, las grandes aplicaciones monolíticas se construían como una sola unidad. Sin embargo, a medida que las aplicaciones crecieron en tamaño y complejidad, se volvieron cada vez más difíciles de mantener. Además, la implementación de estas aplicaciones se volvió más complicada, ya que había que implementar toda la aplicación a la vez.

Para abordar estos problemas, los microservicios se han convertido en un estilo arquitectónico popular para crear aplicaciones. Los microservicios son servicios pequeños e independientes que funcionan juntos para formar una aplicación más grande. Esta arquitectura tiene muchos beneficios, incluidos los siguientes:

- Fácil de implementar y escalar: los microservicios se pueden implementar y escalar de forma independiente, lo que facilita la implementación de nuevas funciones o la escala de servicios según sea necesario.

- Acoplamiento flexible: los servicios son independientes y se pueden cambiar o actualizar sin afectar a otros servicios.

- Resiliente: si un servicio deja de funcionar, los demás pueden seguir funcionando.

Netflix OSS es un conjunto de herramientas y bibliotecas para crear microservicios. En este artículo, aprenderemos a usar Netflix OSS para crear un microservicio Spring Boot.

## Requisitos previos

Antes de comenzar, hay algunas cosas que necesitará:

-Java8
- Maven 3.3.9 o superior

## Crear un proyecto Spring Boot

Comenzaremos creando un proyecto Spring Boot. Para este ejemplo, usaremos Spring Initializr para generar nuestro proyecto.

Vaya a https://start.spring.io/ y seleccione las siguientes opciones:

- Proyecto: Proyecto Maven
- Idioma: Java
- Versión de arranque de primavera: 2.1.3

Haga clic en "Generar proyecto" para descargar el proyecto.

## Agregar dependencias

A continuación, necesitaremos agregar algunas dependencias a nuestro proyecto. Abra el archivo `pom.xml` generado y agregue las siguientes dependencias:

```xml
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-actuator</artifactId>
	</dependency>
	<dependency>
		<groupId>org.springframework.cloud</groupId>
		<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
	</dependency>
</dependencies>
```

La dependencia `spring-boot-starter-actuator` proporciona características para monitorear y administrar nuestra aplicación. La dependencia `spring-cloud-starter-netflix-eureka-client` proporciona integración con la herramienta de descubrimiento de servicios Eureka.

## Configurar Eureka

Eureka es una herramienta de descubrimiento de servicios. Permite que los servicios se registren y sean descubiertos por otros servicios. Usaremos Eureka para descubrir nuestros microservicios.

Primero, necesitaremos agregar alguna configuración a nuestro archivo `application.properties`:

```properties
eureka.instance.hostname=localhost
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```

A continuación, crearemos una clase `@Configuration` y la anotaremos con `@EnableEurekaClient`:

```java
@Configuration
@EnableEurekaClient
public class EurekaConfig {
}
```

## Crear un microservicio

Ahora que tenemos nuestro proyecto configurado, podemos comenzar a crear nuestro microservicio. Para este ejemplo, crearemos un servicio simple que devuelva un saludo.

Primero, crearemos un `GreetingController`:

```java
@RestController
public class GreetingController {

    @GetMapping("/greeting")
    public String greeting() {
        return "Hello, world!";
    }
}
```

A continuación, crearemos una clase `@Configuration` y la anotaremos con `@EnableWebMvc`:

```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {
}
```

Finalmente, crearemos una clase `@SpringBootApplication`:

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

## Generar y ejecutar la aplicación

Ahora que hemos creado nuestro microservicio, podemos compilarlo y ejecutarlo. En su terminal, navegue hasta el directorio del proyecto y ejecute el siguiente comando:

```
mvn spring-boot:run
```

Debería ver el siguiente resultado:

```
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.1.3.RELEASE)

2019-03-29 13:48:41.537  INFO 14073 --- [           main] c.e.a.Application                    : Starting Application on my-macbook-pro.local with PID 14073 (/Users/jdoe/projects/spring-boot-microservices/target/classes started by jdoe in /Users/jdoe/projects/spring-boot-microservices)
2019-03-29 13:48:41.541  INFO 14073 --- [           main] c.e.a.Application                    : No active profile set, falling back to default profiles: default
2019-03-29 13:48:42.591  INFO 14073 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2019-03-29 13:48:42.604  INFO 14073 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2019-03-29 13:48:42.604  INFO 14073 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.17]
2019-03-29 13:48:42.617  INFO 14073 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-03-29 13:48:42.618  INFO 14073 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1735 ms
2019-03-29 13:48:42.791  INFO 14073 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2019-03-29 13:48:42.917  INFO 14073 --- [           main] c.n.eureka.cluster. PeersRefreshScheduler : Starting...
2019-03-29 13:48:42.932  INFO 14073 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8080 (http) with context path ''
2019-03-29 13:48:42.935  INFO 14073 --- [           main] c.e.a.Application                    : Started Application in 1.948 seconds (JVM running for 2.485)
```

Ahora puede acceder al servicio en http://localhost:8080/saludo.

## Configurar el microservicio

Ahora que nuestro microservicio está en funcionamiento, debemos configurarlo. Comenzaremos agregando una propiedad `spring.application.name` a nuestro archivo `application.properties`:

```properties
spring.application.name=greeting-service
```

Esta propiedad establece el nombre de nuestro servicio. Será utilizado por Eureka para identificar nuestro servicio.

A continuación, agregaremos una propiedad `server.port`:

```properties
server.port=8081
```

Esta propiedad establece el puerto en el que se ejecutará nuestro servicio. De forma predeterminada, Spring Boot se ejecutará en el puerto 8080. Sin embargo, podemos cambiar esto configurando la propiedad `server.port`.

## Registrar el microservicio con Eureka

Ahora que nuestro microservicio está configurado, debemos registrarlo con Eureka. Para hacer esto, agregaremos una anotación `@EnableEurekaClient` a nuestra clase `Application`:

```java
@SpringBootApplication
@EnableEurekaClient
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

Esta anotación le dice a Spring que registre nuestro microservicio con Eureka.

## Generar y ejecutar la aplicación

Ahora que hemos registrado nuestro microservicio con Eureka, podemos compilarlo y ejecutarlo. En su terminal, navegue hasta el directorio del proyecto y ejecute el siguiente comando:

```
mvn spring-boot:run
```

Debería ver el siguiente resultado:

```
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.1.3.RELEASE)

2019-03-29 13:54:45.264  INFO 29122 --- [           main] c.e.a.Application                    : Starting Application on my-macbook-pro.local with PID 29122 (/Users/jdoe/projects/spring-boot-microservices/target/classes started by jdoe in /Users/jdoe/projects/spring-boot-microservices)
2019-03-29 13:54:45.266  INFO 29122 --- [           main] c.e.a.Application                    : No active profile set, falling back to default profiles: default
2019-03-29 13:54:46.318  INFO 29122 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8081 (http)
2019-03-29 13:54:46.330  INFO 29122 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2019-03-29 13:54:46.331  INFO 29122 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.17]
2019-03-29 13:54:46.344  INFO 29122 --- [           main] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-03-29 13:54:46.345  INFO 29122 --- [           main] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1773 ms
2019-03-29 13:54:46.522  INFO 29122 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2019-03-29 13:54:46.643  INFO 29122 --- [           main] c.n.eureka.cluster. PeersRefreshScheduler : Starting...
2019-03-29 13:54:46.657  INFO 29122 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port(s): 8081 (http) with context path ''
2019-03-29 13:54:46.660  INFO 29122 --- [           main] c.e.a.Application                    : Started Application in 1.965 seconds (JVM running for 2.502)
```

Ahora puede acceder al servicio en http://localhost:8081/saludo.

## Probar el microservicio

Ahora que nuestro microservicio está en funcionamiento, podemos probarlo. En tu terminal, ejecuta el siguiente comando:

```
curl http://localhost:8081/greeting
```

Debería ver el siguiente resultado:

```
Hello, world!
```

## Conclusión

En este artículo, aprendimos a usar Netflix OSS para crear un microservicio Spring Boot. También aprendimos cómo registrar el microservicio con Eureka y cómo probarlo.