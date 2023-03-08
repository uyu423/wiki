---
title: 052: Building a search engine optimization (SEO) friendly website using Spring Boot and Spring MVC
description: 
published: true
date: 2023-02-02T18:57:31.067Z
tags: 
editor: markdown
dateCreated: 2023-02-02T18:57:26.482Z
---

- [052: Creación de un sitio web compatible con la optimización de motores de búsqueda (SEO) utilizando Spring Boot y Spring MVC***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/052-building-a-search-engine-optimization-seo-friendly-website-using-spring-boot-and-spring-mvc)
{.links-list}
- [052：使用 Spring Boot 和 Spring MVC 构建搜索引擎优化 (SEO) 友好的网站***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/052-building-a-search-engine-optimization-seo-friendly-website-using-spring-boot-and-spring-mvc)
{.links-list}
- [052: Spring Boot 및 Spring MVC를 사용하여 검색 엔진 최적화(SEO) 친화적인 웹 사이트 구축***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/052-building-a-search-engine-optimization-seo-friendly-website-using-spring-boot-and-spring-mvc)
{.links-list}


## Introduction

Search engine optimization (SEO) is the practice of improving the ranking of a website on search engines. The higher the ranking, the more likely people are to find the website.

There are many factors that contribute to a website's ranking, including the quality of the content, the structure of the website, and the way the website is coded.

In this post, we will focus on how to code a website using Spring Boot and Spring MVC that is friendly to search engines.

## What is Spring Boot?

Spring Boot is a framework that makes it easy to create stand-alone, production-grade Spring-based applications.

Spring Boot includes a number of features that make it easy to create and run a web application, including:

- Embedded Tomcat or Jetty server
- Support for Thymeleaf, FreeMarker, and other template engines
- Automatic configuration
- Automatic generation of project documentation

## What is Spring MVC?

Spring MVC is a framework for building web applications. It is built on top of the Spring framework and provides a unified approach to web application development.

Spring MVC includes a number of features that make it easy to develop web applications, including:

- A simple, consistent model for handling requests and responses
- A flexible view resolution mechanism
- Support for multiple view technologies
- A pluggable localization mechanism

## Creating a Spring Boot Web Application

We will use the Spring Initializr to create a Spring Boot web application.

Go to the Spring Initializr website (https://start.spring.io/) and fill in the form to create a new project.

![Spring Initializr](https://i.imgur.com/hm3Y6uq.png)

Select the following options:

- Project: Gradle Project
- Language: Java
- Spring Boot Version: 2.1.4

Click "Generate Project" to download the project.

## Importing the Project into Eclipse

Import the project into Eclipse as a Gradle project.

## Creating a Controller

Controllers are the heart of a Spring MVC application. They are responsible for handling requests and responses.

In our example, we will create a controller that handles requests to the "/" URL.

Create a new class in the com.example.demo package and name it "HelloController.java".

Add the following code to the class:

```java
package com.example.demo;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class HelloController {

    @RequestMapping("/")
    @ResponseBody
    public String index() {
        return "Hello, world!";
    }

}
```

The ```@Controller``` annotation marks the class as a controller.

The ```@RequestMapping``` annotation maps requests to the "/" URL to the index() method.

The ```@ResponseBody``` annotation indicates that the string returned by the index() method should be the body of the response.

## Creating a View

In a Spring MVC application, views are typically template files that are processed by a template engine.

In our example, we will use the Thymeleaf template engine to process a HTML template file.

Create a new directory in the src/main/resources directory and name it "templates".

Create a new file in the templates directory and name it "index.html".

Add the following code to the file:

```html
<!DOCTYPE html>
<html>
    <head>
        <title>Hello, world!</title>
    </head>
    <body>
        <p>Hello, world!</p>
    </body>
</html>
```

## Configuring the Application

Spring Boot applications are typically configured using properties files.

In our example, we will use a properties file to configure the Thymeleaf template engine.

Create a new file in the src/main/resources directory and name it "application.properties".

Add the following code to the file:

```properties
spring.thymeleaf.prefix=classpath:/templates/
spring.thymeleaf.suffix=.html
spring.thymeleaf.mode=HTML5
spring.thymeleaf.encoding=UTF-8
spring.thymeleaf.content-type=text/html
spring.thymeleaf.cache=false
```

## Running the Application

We can run the application from the command line or from Eclipse.

To run the application from the command line, go to the project directory and type the following command:

```
./gradlew bootRun
```

To run the application from Eclipse, right-click on the project and select "Run As -> Spring Boot App".

## Testing the Application

We can test the application by sending a request to the "/" URL.

To test the application from the command line, we can use the curl command.

```
curl http://localhost:8080/
```

To test the application from Eclipse, we can use the built-in browser.

Right-click on the HelloController.java file and select "Run As -> Spring Boot App".

The application will be started and the "/" URL will be opened in the browser.

## Conclusion

In this post, we have seen how to create a search engine optimization (SEO) friendly website using Spring Boot and Spring MVC.

We have seen how to create a controller that handles requests and responses, and how to create a view that is processed by a template engine.

We have also seen how to configure the application using properties files.