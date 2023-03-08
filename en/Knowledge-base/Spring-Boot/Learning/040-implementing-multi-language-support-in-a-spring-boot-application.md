---
title: 040: Implementing multi-language support in a Spring Boot application
description: 
published: true
date: 2023-02-02T04:04:29.813Z
tags: 
editor: markdown
dateCreated: 2023-02-02T04:04:25.505Z
---

- [040: Implementación de compatibilidad con varios idiomas en una aplicación Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/040-implementing-multi-language-support-in-a-spring-boot-application)
{.links-list}
- [040：在 Spring Boot 应用程序中实现多语言支持***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/040-implementing-multi-language-support-in-a-spring-boot-application)
{.links-list}
- [040: Spring Boot 애플리케이션에서 다국어 지원 구현***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/040-implementing-multi-language-support-in-a-spring-boot-application)
{.links-list}



# Implementing multi-language support in a Spring Boot application

Internationalization (i18n) is the process of developing products or services that can be adapted to specific local languages and cultures, a process known as localization (l10n).

Spring Boot makes it easy to add i18n support to your application with the help of the `spring-boot-starter-data-jpa` and `spring-boot-starter-thymeleaf` starters.

In this post, we'll go over how to add i18n support to a Spring Boot application. We'll cover the following topics:

*   Configuring Spring Boot for i18n
*   Creating language-specific message files
*   Displaying localized messages in your views
*   Switching languages in your application

## Configuring Spring Boot for i18n

First, we need to add the `spring-boot-starter-data-jpa` and `spring-boot-starter-thymeleaf` starters to our `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-thymeleaf</artifactId>
    </dependency>
</dependencies>
```

Next, we need to configure the `MessageSource` bean in our `application.properties` file:

```properties
spring.messages.basename=messages
```

The `MessageSource` bean is responsible for resolving messages from message files. By default, Spring Boot will look for message files in the `src/main/resources` directory.

## Creating language-specific message files

Next, we need to create message files for each language that we want to support. The message file must be named `messages_[lang].properties`, where `[lang]` is the [ISO 639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) code for the language.

For example, if we wanted to support English and French, we would create the following message files:

*   `messages_en.properties`
*   `messages_fr.properties`

Each message file will contain key-value pairs for each message that can be resolved by the `MessageSource` bean. For example, our `messages_en.properties` file might look like this:

```properties
greeting=Hello, world!
```

And our `messages_fr.properties` file might look like this:

```properties
greeting=Bonjour, monde!
```

## Displaying localized messages in your views

Now that we have our message files set up, we can start displaying localized messages in our views.

In Thymeleaf, we can use the `#{...}` syntax to resolve messages from our message files. For example, if we wanted to display the `greeting` message from our `messages_en.properties` file, we could do the following:

```html
<p th:text="#{greeting}">Hello, world!</p>
```

If we wanted to display the `greeting` message from our `messages_fr.properties` file, we could do the following:

```html
<p th:text="#{greeting}">Bonjour, monde!</p>
```

## Switching languages in your application

Now that we can display localized messages in our views, we need a way to switch between languages.

There are many ways to do this, but one simple way is to add a `lang` parameter to our application's `queryString`. For example, if we wanted to switch to the French language, we could do the following:

```
http://localhost:8080/?lang=fr
```

We can then use the `lang` parameter to set the `Locale` in our `LocaleResolver` bean. For example, we could add the following to our `application.properties` file:

```properties
spring.mvc.locale-resolver=org.springframework.web.servlet.i18n.SessionLocaleResolver
```

And then add the following to our `LocaleResolver` bean:

```java
@Bean
public LocaleResolver localeResolver() {
    SessionLocaleResolver localeResolver = new SessionLocaleResolver();
    localeResolver.setDefaultLocale(Locale.ENGLISH);
    return localeResolver;
}
```

Now, when we visit `http://localhost:8080/?lang=fr`, our application will switch to the French language and display the `greeting` message from our `messages_fr.properties` file.

## Conclusion

In this post, we've covered how to add i18n support to a Spring Boot application. We've seen how to configure Spring Boot for i18n, how to create language-specific message files, how to display localized messages in our views, and how to switch languages in our application.