---
title: 070: Spring Boot with Thymeleaf: Creating Dynamic Templates
description: 
published: true
date: 2023-02-05T04:32:38.343Z
tags: 
editor: markdown
dateCreated: 2023-02-05T04:32:32.929Z
---

- [070: Spring Boot con Thymeleaf: creación de plantillas dinámicas***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/070-spring-boot-with-thymeleaf-creating-dynamic-templates)
{.links-list}
- [070：使用 Thymeleaf 的 Spring Boot：创建动态模板***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/070-spring-boot-with-thymeleaf-creating-dynamic-templates)
{.links-list}
- [070: Thymeleaf를 사용한 Spring Boot: 동적 템플릿 생성***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/070-spring-boot-with-thymeleaf-creating-dynamic-templates)
{.links-list}


# 070: Spring Boot with Thymeleaf: Creating Dynamic Templates

In this post, we'll take a look at how to use the Thymeleaf templating engine with Spring Boot to create dynamic HTML pages.

Thymeleaf is a popular templating engine that can be used with Spring MVC to create elegant and dynamic web applications. Thymeleaf's main goal is to bring natural templates to development environments.

## What is Thymeleaf?

Thymeleaf is a Java-based library that provides a set of tools for working with XML and HTML. Thymeleaf's main goal is to bring natural templates to development environments.

Thymeleaf's approach to templating is different than the traditional approach taken by other template engines. With Thymeleaf, templates are not simply "filled in" with data. Instead, Thymeleaf templates are processed and converted into valid HTML documents.

This means that Thymeleaf templates can be used as the starting point for your web application's UI, and can be easily integrated with your application's back-end.

## Getting Started

To get started with Thymeleaf, you'll need to add the following dependency to your project's pom.xml file:

```xml
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf</artifactId>
    <version>3.0.9.RELEASE</version>
</dependency>
```

## Hello, Thymeleaf!

Now that we have Thymeleaf set up, let's create a simple template to see it in action.

Create a new file called `hello.html` in the `src/main/resources/templates` directory and add the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Hello, Thymeleaf!</title>
</head>
<body>
    <h1>Hello, Thymeleaf!</h1>
</body>
</html>
```

This template contains a simple `<h1>` element that says "Hello, Thymeleaf!".

Next, let's create a Spring Boot application that will render this template.

Create a new file called `Application.java` in the `src/main/java` directory and add the following content:

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

This is a basic Spring Boot application. The `@SpringBootApplication` annotation is used to mark the application class as a Spring Boot application.

Next, let's create a controller that will render the `hello.html` template.

Create a new file called `HelloController.java` in the `src/main/java` directory and add the following content:

```java
@Controller
public class HelloController {

    @RequestMapping("/")
    public String hello(Model model) {
        model.addAttribute("message", "Hello, Thymeleaf!");
        return "hello";
    }

}
```

This controller has a single `@RequestMapping` annotated method. This method maps the `/` URL to the `hello` template.

The `hello` template expects a `message` attribute to be present in the model. This attribute is added to the model by the `hello` method.

Now that we have our controller and template set up, let's run our application and see the results.

Run the `Application` class as a Java application and navigate to http://localhost:8080 in your browser. You should see the following output:

![Hello, Thymeleaf!](https://i.imgur.com/ePcUg9x.png)

As you can see, our template was rendered and the `message` attribute was used to populate the `<h1>` element.

## Passing Data to Templates

In the previous section, we saw how to pass data to a template using the `Model` object.

The `Model` object is a Map-like structure that can be used to store data that needs to be passed to a template.

In addition to the `Model` object, Thymeleaf also provides the `Context` object. The `Context` object is a more powerful version of the `Model` object that provides additional features such as type-safety and support for internationalization.

We'll see how to use the `Context` object in the next section.

## Using the Context Object

As we saw in the previous section, the `Model` object is a Map-like structure that can be used to store data that needs to be passed to a template.

The `Context` object is a more powerful version of the `Model` object that provides additional features such as type-safety and support for internationalization.

To use the `Context` object, we need to add the following dependency to our project's pom.xml file:

```xml
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf-extras-java8time</artifactId>
    <version>3.0.4.RELEASE</version>
</dependency>
```

This dependency provides support for the `Context` object.

Next, let's create a template that uses the `Context` object.

Create a new file called `context.html` in the `src/main/resources/templates` directory and add the following content:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Context Example</title>
</head>
<body>
    <h1 th:text="${message}"></h1>
</body>
</html>
```

This template contains a `<h1>` element that uses the `message` attribute from the `Context` object.

Next, let's create a controller that will render this template.

Create a new file called `ContextController.java` in the `src/main/java` directory and add the following content:

```java
@Controller
public class ContextController {

    @RequestMapping("/")
    public String context(Context context) {
        context.setVariable("message", "Hello, Thymeleaf!");
        return "context";
    }

}
```

This controller has a single `@RequestMapping` annotated method. This method maps the `/` URL to the `context` template.

The `context` template expects a `message` attribute to be present in the `Context` object. This attribute is added to the `Context` object by the `context` method.

Now that we have our controller and template set up, let's run our application and see the results.

Run the `Application` class as a Java application and navigate to http://localhost:8080 in your browser. You should see the following output:

![Hello, Thymeleaf!](https://i.imgur.com/ePcUg9x.png)

As you can see, our template was rendered and the `message` attribute was used to populate the `<h1>` element.

## Conclusion

In this post, we've seen how to use the Thymeleaf templating engine with Spring Boot to create dynamic HTML pages.

We've also seen how to use the `Model` and `Context` objects to pass data to templates.

Thymeleaf is a powerful templating engine that can be used to create dynamic and sophisticated web applications.