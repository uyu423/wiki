---
title: Spring Boot Monitoring with Actuator
description: 
published: true
date: 2023-02-07T15:33:20.888Z
tags: 
editor: markdown
dateCreated: 2023-02-07T15:33:14.979Z
---

- [Monitoreo de resorte de arranque con actuador***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/spring-boot-monitoring-with-actuator)
{.links-list}
- [使用 Actuator 进行 Spring Boot 监控***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/spring-boot-monitoring-with-actuator)
{.links-list}
- [액추에이터를 사용한 스프링 부트 모니터링***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/spring-boot-monitoring-with-actuator)
{.links-list}


# Spring Boot Monitoring with Actuator 

In a production Spring Boot application, it is important to be able to monitor the application to be able to identify and diagnose any issues that may arise. Spring Boot provides a number of features out of the box to help with this, including the Actuator.

The Actuator is a tool that allows you to monitor and manage your Spring Boot application. It provides a number of endpoints that allow you to monitor and manage your application, without having to write any code.

In this article, we will take a look at how to use the Actuator to monitor a Spring Boot application. We will also look at how to use the Actuator to create custom endpoints to expose application-specific information.

## Enabling the Actuator 

To use the Actuator, you first need to add the spring-boot-starter-actuator dependency to your project. This can be done by adding the following dependency to your pom.xml file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

Alternatively, if you are using Gradle, you can add the following dependency to your build.gradle file:

```groovy
dependencies {
    compile('org.springframework.boot:spring-boot-starter-actuator')
}
```

Once you have added the spring-boot-starter-actuator dependency to your project, the Actuator will be enabled by default. By default, the Actuator will only be accessible to users with the role of ‘ADMIN’.

To change this, you can add the following property to your application.properties file:

```properties
management.security.enabled=false
```

This will disable security for the Actuator endpoints. Alternatively, you can add the spring-boot-starter-security dependency to your project to configure security for the Actuator endpoints.

## Actuator Endpoints 

The Actuator exposes a number of endpoints. These endpoints can be used to monitor and manage your application. The endpoints are divided into two groups:

* productionEndpoints: These endpoints are intended for use in production and provide information about the health and state of your application.
* allEndpoints: These endpoints provide information about the health and state of your application, as well as application-specific information.

The allEndpoints group includes all of the productionEndpoints, as well as any custom endpoints that you have created.

The following table lists the productionEndpoints that are provided by the Actuator:

| Endpoint | Description |
| --- | --- |
| /auditevents | This endpoint provides information about application events that have been audited. |
| /beans | This endpoint provides information about the beans that have been created by the Spring container. |
| /configprops | This endpoint provides information about the configuration properties that have been set for your application. |
| /dump | This endpoint can be used to dump the state of your application. This is useful for troubleshooting purposes. |
| /env | This endpoint provides information about the environment variables that have been set for your application. |
| /flyway | This endpoint provides information about the database migrations that have been applied by Flyway. |
| /health | This endpoint provides information about the health of your application. |
| /info | This endpoint provides application-specific information. |
| /liquibase | This endpoint provides information about the database migrations that have been applied by Liquibase. |
| /loggers | This endpoint can be used to configure the logging level for your application. |
| /metrics | This endpoint provides information about the metrics that have been collected for your application. |
| /mappings | This endpoint provides information about the @RequestMapping paths that have been defined for your application. |
| /shutdown | This endpoint can be used to shutdown your application. |
| /trace | This endpoint provides information about the HTTP requests that have been made to your application. |

To access any of these endpoints, you need to append the endpoint to the path of your application. For example, if your application is running on http://localhost:8080, you would access the /health endpoint at http://localhost:8080/health.

## Reading Actuator Endpoints 

To read the information from an Actuator endpoint, you can use a tool such as curl, wget, or a browser.

For example, to read the /health endpoint, you can use curl as follows:

```
$ curl http://localhost:8080/health
```

Alternatively, you can use wget as follows:

```
$ wget http://localhost:8080/health
```

If you use a browser to access the /health endpoint, you will see the following output:

```json
{
    "status": "UP",
    "diskSpace": {
        "status": "UP",
        "total": 499963648,
        "free": 367030272,
        "threshold": 10485760
    },
    "db": {
        "status": "UP",
        "database": "H2",
        "hello": 1
    },
    "redis": {
        "status": "UP"
    }
}
```

The output from the /health endpoint is a JSON document that contains information about the health of your application. The status field indicates the overall health of your application. The diskSpace, db, and redis fields contain information about the health of specific subsystems.

## Creating Custom Endpoints 

In addition to the built-in endpoints, you can also create custom endpoints. To do this, you need to create a class that implements the org.springframework.boot.actuate.endpoint.annotation.Endpoint interface.

For example, the following class defines a custom endpoint that returns a list of users:

```java
@Endpoint(id="users")
public class UserEndpoint {

    private List<User> users;

    @ReadOperation
    public List<User> getUsers() {
        return this.users;
    }

    public void setUsers(List<User> users) {
        this.users = users;
    }

}
```

The @Endpoint annotation is used to annotate the class. The id attribute is used to specify the identifier for the endpoint. This is the identifier that will be used to access the endpoint.

The getUsers() method is annotated with the @ReadOperation annotation. This annotation indicates that the method can be used to read the information from the endpoint.

The setUsers() method is annotated with the @WriteOperation annotation. This annotation indicates that the method can be used to write the information to the endpoint.

To register the endpoint, you need to add the @Component annotation to the class. For example:

```java
@Component
@Endpoint(id="users")
public class UserEndpoint {
    // ...
}
```

Alternatively, you can register the endpoint by adding it to the application context. For example:

```java
@Configuration
public class EndpointConfig {

    @Bean
    public UserEndpoint userEndpoint() {
        return new UserEndpoint();
    }

}
```

Once you have registered the endpoint, you can access it by appending the endpoint identifier to the path of your application. For example, if your application is running on http://localhost:8080, you can access the /users endpoint at http://localhost:8080/users.

##Conclusion

In this article, we have looked at how to use the Actuator to monitor a Spring Boot application. We have also looked at how to use the Actuator to create custom endpoints to expose application-specific information.