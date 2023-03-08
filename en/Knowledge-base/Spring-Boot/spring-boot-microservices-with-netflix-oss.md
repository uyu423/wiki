---
title: Spring Boot Microservices with Netflix OSS
description: 
published: true
date: 2023-02-08T00:32:59.553Z
tags: 
editor: markdown
dateCreated: 2023-02-08T00:32:53.651Z
---

- [Microservicios Spring Boot con Netflix OSS***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-microservices-with-netflix-oss)
{.links-list}
- [带有 Netflix OSS 的 Spring Boot 微服务***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-microservices-with-netflix-oss)
{.links-list}
- [Netflix OSS를 사용한 Spring Boot 마이크로서비스***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-microservices-with-netflix-oss)
{.links-list}


# Spring Boot Microservices with Netflix OSS

In the past, large monolithic applications were built as a single unit. However, as the applications grew in size and complexity, they became increasingly difficult to maintain. In addition, the deployment of these applications became more complicated, as the entire application had to be deployed at once.

To address these issues, microservices have become a popular architectural style for building applications. Microservices are small, self-contained services that work together to form a larger application. This architecture has many benefits, including the following:

- Easy to deploy and scale: Microservices can be deployed and scaled independently, which makes it easy to deploy new features or scale services as needed.

- Loose coupling: Services are independent and can be changed or updated without affecting other services.

- Resilient: If one service goes down, the others can continue to run.

Netflix OSS is a set of tools and libraries for building microservices. In this article, we'll learn how to use Netflix OSS to build a Spring Boot microservice.

## Prerequisites

Before we get started, there are a few things you'll need:

- Java 8
- Maven 3.3.9 or higher

## Create a Spring Boot project

We'll start by creating a Spring Boot project. For this example, we'll be using the Spring Initializr to generate our project.

Go to https://start.spring.io/ and select the following options:

- Project: Maven Project
- Language: Java
- Spring Boot Version: 2.1.3

Click "Generate Project" to download the project.

## Add dependencies

Next, we'll need to add some dependencies to our project. Open the generated `pom.xml` file and add the following dependencies:

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

The `spring-boot-starter-actuator` dependency provides features for monitoring and managing our application. The `spring-cloud-starter-netflix-eureka-client` dependency provides integration with the Eureka service discovery tool.

## Configure Eureka

Eureka is a service discovery tool. It allows services to register themselves and be discovered by other services. We'll use Eureka to discover our microservices.

First, we'll need to add some configuration to our `application.properties` file:

```properties
eureka.instance.hostname=localhost
eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false
```

Next, we'll create a `@Configuration` class and annotate it with `@EnableEurekaClient`:

```java
@Configuration
@EnableEurekaClient
public class EurekaConfig {
}
```

## Create a microservice

Now that we have our project set up, we can start creating our microservice. For this example, we'll create a simple service that returns a greeting.

First, we'll create a `GreetingController`:

```java
@RestController
public class GreetingController {

    @GetMapping("/greeting")
    public String greeting() {
        return "Hello, world!";
    }
}
```

Next, we'll create a `@Configuration` class and annotate it with `@EnableWebMvc`:

```java
@Configuration
@EnableWebMvc
public class WebConfig implements WebMvcConfigurer {
}
```

Finally, we'll create a `@SpringBootApplication` class:

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

## Build and run the application

Now that we have our microservice created, we can build and run it. In your terminal, navigate to the project directory and run the following command:

```
mvn spring-boot:run
```

You should see the following output:

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

You can now access the service at http://localhost:8080/greeting.

## Configure the microservice

Now that our microservice is up and running, we need to configure it. We'll start by adding a `spring.application.name` property to our `application.properties` file:

```properties
spring.application.name=greeting-service
```

This property sets the name of our service. It will be used by Eureka to identify our service.

Next, we'll add a `server.port` property:

```properties
server.port=8081
```

This property sets the port that our service will run on. By default, Spring Boot will run on port 8080. However, we can change this by setting the `server.port` property.

## Register the microservice with Eureka

Now that our microservice is configured, we need to register it with Eureka. To do this, we'll add a `@EnableEurekaClient` annotation to our `Application` class:

```java
@SpringBootApplication
@EnableEurekaClient
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```

This annotation tells Spring to register our microservice with Eureka.

## Build and run the application

Now that we've registered our microservice with Eureka, we can build and run it. In your terminal, navigate to the project directory and run the following command:

```
mvn spring-boot:run
```

You should see the following output:

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

You can now access the service at http://localhost:8081/greeting.

## Test the microservice

Now that our microservice is up and running, we can test it. In your terminal, run the following command:

```
curl http://localhost:8081/greeting
```

You should see the following output:

```
Hello, world!
```

## Conclusion

In this article, we've learned how to use Netflix OSS to build a Spring Boot microservice. We've also learned how to register the microservice with Eureka and how to test it.