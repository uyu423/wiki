---
title: 002: Configuración de un proyecto Spring Boot
description: 
published: true
date: 2023-02-03T07:05:23.450Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:05:18.589Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [002: Setting up a Spring Boot project***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/002-setting-up-a-spring-boot-project)
{.links-list}


# Configuración de un proyecto Spring Boot

En esta publicación, veremos cómo configurar un proyecto Spring Boot.

Spring Boot es un marco popular para crear aplicaciones y servicios web. Está construido sobre el marco Spring y facilita la creación de aplicaciones basadas en Spring independientes y de grado de producción.

## Requisitos previos

Antes de comenzar, hay algunas cosas que deberá tener para seguir:

- Java 8 o superior
- Un editor de texto o IDE
- Maven 3.3.9 o superior

## Creando un proyecto

Hay algunas formas diferentes de crear un proyecto Spring Boot. En esta publicación, usaremos [Spring Initializr](https://start.spring.io/) para generar un proyecto.

Dirígete al sitio web de Spring Initializr y completa el formulario con la siguiente información:

- Proyecto: Proyecto Maven
- Idioma: Java
- Versión de arranque de primavera: 2.1.7

Haga clic en el botón "Generar proyecto" y se descargará un archivo zip. Extraiga el contenido del archivo zip en un directorio de su elección.

## Importando el proyecto

En su editor de texto o IDE, importe el proyecto como un proyecto Maven. Si está utilizando Eclipse, puede hacerlo yendo a Archivo -> Importar -> Proyectos existentes de Maven.

## Ejecutando el proyecto

Ahora que el proyecto está configurado, podemos ejecutarlo.

Hay algunas formas diferentes de ejecutar una aplicación Spring Boot. La forma más sencilla es usar el complemento Maven:

```
mvn spring-boot:run
```

Debería ver un resultado similar al siguiente:

```
[INFO] Scanning for projects...
[INFO] 
[INFO] ------------------------------------------------------------------------
[INFO] Building myproject 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] 
[INFO] >>> spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) > test-compile @ myproject >>>
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ myproject ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/user/Documents/workspace-sts-3.9.10.RELEASE/myproject/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ myproject ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] >>> spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) > compile @ myproject >>>
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ myproject ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/user/Documents/workspace-sts-3.9.10.RELEASE/myproject/src/main/resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ myproject ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] >>> spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) > test-compile @ myproject >>>
[INFO] 
[INFO] <<< spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) < test-compile @ myproject <<<
[INFO] 
[INFO] 
[INFO] --- spring-boot-maven-plugin:2.1.7.RELEASE:run (default-cli) @ myproject ---
[INFO] Attaching agents: []

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.1.7.RELEASE)

2019-06-07 23:58:45.583  INFO 86848 --- [           main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port(s): 8080 (http)
2019-06-07 23:58:45.602  INFO 86848 --- [           main] o.apache.catalina.core.StandardService   : Starting service [Tomcat]
2019-06-07 23:58:45.602  INFO 86848 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet engine: [Apache Tomcat/9.0.22]
2019-06-07 23:58:45.697  INFO 86848 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-06-07 23:58:45.697  INFO 86848 --- [ost-startStop-1] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 100 ms
2019-06-07 23:58:46.069  INFO 86848 --- [ost-startStop-1] o.s.s.concurrent.ThreadPoolTaskExecutor  : Initializing ExecutorService 'applicationTaskExecutor'
2019-06-07 23:58:46.145  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.ServletRegistrationBean  : Servlet dispatcherServlet mapped to [/]
2019-06-07 23:58:46.149  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'characterEncodingFilter' to: [/*]
2019-06-07 23:58:46.149  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'hiddenHttpMethodFilter' to: [/*]
2019-06-07 23:58:46.149  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'httpPutFormContentFilter' to: [/*]
2019-06-07 23:58:46.149  INFO 86848 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean   : Mapping filter: 'requestContextFilter' to: [/*]
2019-06-07 23:58:46.839  INFO 86848 --- [           main] o.s.s.concurrent.ThreadPoolTaskExecutor  : Shutting down ExecutorService 'applicationTaskExecutor'
2019-06-07 23:58:46.841  INFO 86848 --- [           main] o.apache.catalina.core.StandardService   : Stopping service [Tomcat]
2019-06-07 23:58:46.857  INFO 86848 --- [           main] ConditionEvaluationReportLoggingListener : 

Error starting ApplicationContext. To display the conditions report re-run your application with 'debug' enabled.
2019-06-07 23:58:46.862 ERROR 86848 --- [           main] o.s.boot.SpringApplication               : Application run failed

org.springframework.boot.context.event.ApplicationFailedEvent[source=org.springframework.boot.SpringApplication@4f4f4f4f]

```

Si ve este resultado, significa que el proyecto está funcionando.