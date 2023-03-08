---
title: Debugging with Spring Boot DevTools
description: 
published: true
date: 2023-02-07T02:32:35.765Z
tags: 
editor: markdown
dateCreated: 2023-02-07T02:32:29.841Z
---

- [Depuración con Spring Boot DevTools***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/debugging-with-spring-boot-devtools)
{.links-list}
- [使用 Spring Boot DevTools 进行调试***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/debugging-with-spring-boot-devtools)
{.links-list}
- [Spring Boot DevTools로 디버깅***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/debugging-with-spring-boot-devtools)
{.links-list}


# Debugging with Spring Boot DevTools

Spring Boot comes with a number of great features to help developers with their applications. DevTools is one of those features. It can help with debugging, reloading, and more.

## What is DevTools?

DevTools is a set of tools that can help with development. It can do things like reload your application without restarting the server, and automatically restart the server when files are changed. It can also help with debugging, by allowing you to debug your application in your IDE.

## Setting up DevTools

To use DevTools, you will need to add it to your project. You can do this by adding it to your dependencies. For example, in Maven, you would add it to your `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
    </dependency>
</dependencies>
```

Or, if you are using Gradle, you would add it to your `build.gradle`:

```groovy
dependencies {
    compile 'org.springframework.boot:spring-boot-devtools'
}
```

## Using DevTools

Once you have DevTools configured in your project, you can start using it.

### Reloading your application

One of the most useful features of DevTools is the ability to reload your application without restarting the server. To do this, you can simply hit `Ctrl+F9` (or `Cmd+F9` on macOS) in your IDE. This will trigger a full restart of your application.

If you only want to restart the server, you can hit `Ctrl+Shift+F9` (or `Cmd+Shift+F9` on macOS). This will only restart the server, and not the application.

### Debugging your application

Another useful feature of DevTools is the ability to debug your application in your IDE. To do this, you need to start your application in debug mode. You can do this by passing the `--debug` flag to the `spring-boot` CLI:

```
$ spring-boot --debug
```

Or, you can set the `spring.boot.debug` property in your `application.properties`:

```properties
spring.boot.debug=true
```

Once your application is running in debug mode, you can attach a debugger to it. For example, in IntelliJ IDEA, you can do this by going to `Run > Attach Debugger to Local Process`.

## Conclusion

DevTools is a great tool that can help with development. It can do things like reload your application without restarting the server, and automatically restart the server when files are changed. It can also help with debugging, by allowing you to debug your application in your IDE.