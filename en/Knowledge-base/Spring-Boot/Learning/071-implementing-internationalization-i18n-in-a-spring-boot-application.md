---
title: 071: Implementing Internationalization (i18n) in a Spring Boot Application
description: 
published: true
date: 2023-02-01T22:36:39.796Z
tags: 
editor: markdown
dateCreated: 2023-02-01T22:36:35.791Z
---

- [071: Implementación de la internacionalización (i18n) en una aplicación Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/071-implementing-internationalization-i18n-in-a-spring-boot-application)
{.links-list}
- [071：在 Spring Boot 应用程序中实现国际化 (i18n)***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/071-implementing-internationalization-i18n-in-a-spring-boot-application)
{.links-list}
- [071: Spring Boot 애플리케이션에서 국제화(i18n) 구현***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/071-implementing-internationalization-i18n-in-a-spring-boot-application)
{.links-list}


# Implementing Internationalization (i18n) in a Spring Boot Application

Internationalization (i18n) is the process of making your application support multiple languages. This can be a complex task, but Spring Boot makes it much easier. In this post, we'll take a look at how to implement i18n in a Spring Boot application.

## What is i18n?

Internationalization (i18n) is the process of making your application support multiple languages. This can be a complex task, but Spring Boot makes it much easier. 

## Why use i18n?

There are many reasons why you might want to add i18n support to your application. Maybe you have users all over the world and want to offer them a localized experience. Or maybe you're just building a personal project and want to learn how to add i18n support. Whatever the reason, i18n is a valuable skill to have.

## How to implement i18n in Spring Boot

Spring Boot makes it easy to add i18n support to your application. In this section, we'll take a look at how to do just that.

### 1. Add the i18n dependencies

First, you need to add the i18n dependencies to your `pom.xml` file:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

### 2. Configure the i18n properties

Next, you need to configure the i18n properties in your `application.properties` file:

```properties
spring.mvc.locale=en
spring.messages.basename=i18n/messages
```

### 3. Create the i18n files

Now you need to create the i18n files. These files will contain the translated messages for your application. You can create these files in `src/main/resources/i18n`.

For example, let's say you want to support English and French. You would create the following files:

- `messages_en.properties`
- `messages_fr.properties`

In these files, you would define the translated messages for your application. For example:

```properties
# messages_en.properties

greeting=Hello
```

```properties
# messages_fr.properties

greeting=Bonjour
```

### 4. Use the i18n messages in your code

Now that you have the i18n files configured, you can use the translated messages in your code. For example, let's say you have a controller with the following method:

```java
@RequestMapping("/greeting")
public String greeting(Model model) {
    model.addAttribute("message", "greeting");
    return "greeting";
}
```

This method will render the `greeting.ftl` template with the `message` attribute set to the `greeting` key from the i18n files. So if the `spring.mvc.locale` property is set to `en`, the `message` attribute will be set to `Hello`. If the `spring.mvc.locale` property is set to `fr`, the `message` attribute will be set to `Bonjour`.

## Conclusion

In this post, we've looked at how to add i18n support to a Spring Boot application. i18n can be a complex task, but Spring Boot makes it much easier. By following the steps in this post, you can add i18n support to your application with ease.