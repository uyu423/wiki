---
title: 004: Building REST APIs with Spring Boot and Spring MVC
description: 
published: true
date: 2023-02-03T07:36:51.581Z
tags: 
editor: markdown
dateCreated: 2023-02-03T07:36:46.725Z
---

- [004: Creación de API REST con Spring Boot y Spring MVC***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/004-building-rest-apis-with-spring-boot-and-spring-mvc)
{.links-list}
- [004：使用 Spring Boot 和 Spring MVC 构建 REST API***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/004-building-rest-apis-with-spring-boot-and-spring-mvc)
{.links-list}
- [004: Spring Boot 및 Spring MVC로 REST API 구축***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/004-building-rest-apis-with-spring-boot-and-spring-mvc)
{.links-list}


#004: Building REST APIs with Spring Boot and Spring MVC

In this post, we'll learn how to build REST APIs with Spring Boot and Spring MVC.

We'll start by creating a simple Spring Boot application. Then, we'll add a controller to expose some REST endpoints. Finally, we'll test our API using Postman.

##Creating a Spring Boot Application

First, we'll need to create a Spring Boot application. We can use the Spring Initializr to do this.

Go to http://start.spring.io/ and select the following options:

- Generate a Maven Project with Java and Spring Boot 2.0
- Packaging: Jar
- Java Version: 8
- Group: com.example
- Artifact: demo
- Name: DemoApplication
- Description: Demo of Spring Boot REST API
- Package Name: com.example.demo

Click Generate Project to download the project.

Extract the zip file and open the project in your favorite IDE.

##Adding a Controller

Next, we'll add a controller to expose some REST endpoints.

First, we'll create a new package called `com.example.demo.controller`. Then, we'll create a new class called `DemoController` within that package.

Our controller will have the following endpoints:

- `GET /`: A welcome message
- `GET /hello`: A greeting
- `POST /greeting`: A greeting with a custom message

Here's the code for our controller:

```java
package com.example.demo.controller;

import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class DemoController {

    @GetMapping("/")
    public String index() {
        return "Welcome to the Spring Boot REST API!";
    }

    @GetMapping("/hello")
    public String hello() {
        return "Hello, Spring Boot!";
    }

    @PostMapping("/greeting")
    public String greeting(@RequestParam(value="name", defaultValue="World") String name) {
        return "Hello, " + name + "!";
    }

}
```

Let's break down what's happening in the code above.

First, we're using the `@RestController` annotation to designate this class as a controller.

Then, we're using the `@GetMapping` and `@PostMapping` annotations to map HTTP GET and POST requests to specific methods in our controller.

Finally, we're using the `@RequestParam` annotation to extract query parameters from the request. In this case, we're extracting the `name` parameter. If the `name` parameter is not specified, we're using the default value of `World`.

##Testing the API

Now that we have our controller set up, let's test our API using Postman.

First, we'll need to start our application. We can do this by running the `DemoApplication` class as a Java application.

Once the application has started, we can send requests to our API using Postman.

Let's send a GET request to the `/` endpoint:

![get-request](https://i.imgur.com/LNcuFtD.png)

As you can see, we get a welcome message in response.

Let's send a GET request to the `/hello` endpoint:

![hello-request](https://i.imgur.com/VywYbnK.png)

As you can see, we get a greeting in response.

Finally, let's send a POST request to the `/greeting` endpoint:

![post-request](https://i.imgur.com/EC4nUg4.png)

As you can see, we get a greeting with a custom message in response.

##Conclusion

In this post, we learned how to build REST APIs with Spring Boot and Spring MVC.

We started by creating a simple Spring Boot application. Then, we added a controller to expose some REST endpoints. Finally, we tested our API using Postman.