---
title: 029: Using Spring Boot with Apache Camel
description: 
published: true
date: 2023-02-03T21:32:20.369Z
tags: 
editor: markdown
dateCreated: 2023-02-03T21:32:15.349Z
---

- [029: Uso de Spring Boot con Apache Camel***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/029-using-spring-boot-with-apache-camel)
{.links-list}
- [029：将 Spring Boot 与 Apache Camel 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/029-using-spring-boot-with-apache-camel)
{.links-list}
- [029: Apache Camel에서 Spring Boot 사용***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/029-using-spring-boot-with-apache-camel)
{.links-list}


# Using Spring Boot with Apache Camel

With the release of Camel 2.0, a new set of annotations were introduced to make Camel easier to use with the Spring Framework. In this post, we'll take a look at how to use Spring Boot with Camel.

We'll start with a simple example that routes an HTTP request to a log. First, we'll need to add the following dependencies to our `pom.xml`:

```xml
<dependency>
    <groupId>org.apache.camel</groupId>
    <artifactId>camel-spring-boot-starter</artifactId>
    <version>2.22.0</version>
</dependency>
```

Now we can create a `@Configuration` class that sets up Camel:

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

Finally, we'll need a `application.properties` file to configure the Jetty server:

```properties
server.port=8080
```

That's it! We can now run our application and hit `http://localhost:8080/myapp` with a browser or `curl`. We should see the request logged in the console.

Of course, this example is very simple. Camel provides a huge number of components that can be used to build more complex applications. For more information on using Camel with Spring Boot, check out the [documentation](http://camel.apache.org/spring-boot.html).