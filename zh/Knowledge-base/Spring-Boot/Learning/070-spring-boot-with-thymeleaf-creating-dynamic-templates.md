---
title: 070：使用 Thymeleaf 的 Spring Boot：创建动态模板
description: 
published: true
date: 2023-02-05T04:32:34.652Z
tags: 
editor: markdown
dateCreated: 2023-02-05T04:32:32.926Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [070: Spring Boot with Thymeleaf: Creating Dynamic Templates***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/070-spring-boot-with-thymeleaf-creating-dynamic-templates)
{.links-list}


# 070：使用 Thymeleaf 的 Spring Boot：创建动态模板

在本文中，我们将了解如何将 Thymeleaf 模板引擎与 Spring Boot 结合使用来创建动态 HTML 页面。

Thymeleaf 是一种流行的模板引擎，可以与 Spring MVC 一起使用来创建优雅和动态的 Web 应用程序。 Thymeleaf 的主要目标是将自然模板引入开发环境。

## 什么是 Thymeleaf？

Thymeleaf 是一个基于 Java 的库，它提供了一组用于处理 XML 和 HTML 的工具。 Thymeleaf 的主要目标是将自然模板引入开发环境。

Thymeleaf 的模板化方法不同于其他模板引擎采用的传统方法。使用 Thymeleaf，模板不仅仅是用数据“填充”。相反，Thymeleaf 模板被处理并转换为有效的 HTML 文档。

这意味着 Thymeleaf 模板可以用作 Web 应用程序 UI 的起点，并且可以轻松地与应用程序的后端集成。

## 入门

要开始使用 Thymeleaf，您需要将以下依赖项添加到项目的 pom.xml 文件中：

```xml
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf</artifactId>
    <version>3.0.9.RELEASE</version>
</dependency>
```

## 你好，Thymeleaf！

现在我们已经设置了 Thymeleaf，让我们创建一个简单的模板来查看它的运行情况。

在 `src/main/resources/templates` 目录中创建一个名为 `hello.html` 的新文件并添加以下内容：

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

该模板包含一个简单的 `<h1>` 元素，上面写着“Hello, Thymeleaf!”。

接下来，让我们创建一个将呈现此模板的 Spring Boot 应用程序。

在 `src/main/java` 目录中创建一个名为 `Application.java` 的新文件并添加以下内容：

```java
@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

这是一个基本的 Spring Boot 应用程序。 @SpringBootApplication 注释用于将应用程序类标记为 Spring Boot 应用程序。

接下来，让我们创建一个控制器来呈现“hello.html”模板。

在 `src/main/java` 目录中创建一个名为 `HelloController.java` 的新文件并添加以下内容：

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

该控制器有一个带注释的“@RequestMapping”方法。此方法将 `/` URL 映射到 `hello` 模板。

`hello` 模板期望模型中存在一个 `message` 属性。此属性通过“hello”方法添加到模型中。

现在我们已经设置了控制器和模板，让我们运行我们的应用程序并查看结果。

将“Application”类作为 Java 应用程序运行，并在浏览器中导航到 http://localhost:8080。您应该看到以下输出：

![你好，Thymeleaf！](https://i.imgur.com/ePcUg9x.png)

如您所见，我们的模板已呈现，并且“message”属性用于填充“<h1>”元素。

## 将数据传递给模板

在上一节中，我们看到了如何使用 `Model` 对象将数据传递给模板。

`Model` 对象是一个类似于 Map 的结构，可用于存储需要传递给模板的数据。

除了 `Model` 对象，Thymeleaf 还提供了 `Context` 对象。 `Context` 对象是 `Model` 对象的更强大版本，它提供了类型安全和国际化支持等附加功能。

我们将在下一节中看到如何使用 `Context` 对象。

## 使用上下文对象

正如我们在上一节中看到的，`Model` 对象是一个类似于 Map 的结构，可用于存储需要传递给模板的数据。

`Context` 对象是 `Model` 对象的更强大版本，它提供了类型安全和国际化支持等附加功能。

要使用 `Context` 对象，我们需要将以下依赖项添加到项目的 pom.xml 文件中：

```xml
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf-extras-java8time</artifactId>
    <version>3.0.4.RELEASE</version>
</dependency>
```

此依赖项提供对“上下文”对象的支持。

接下来，让我们创建一个使用 `Context` 对象的模板。

在 `src/main/resources/templates` 目录中创建一个名为 `context.html` 的新文件并添加以下内容：

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

该模板包含一个 <h1> 元素，该元素使用来自 Context 对象的 message 属性。

接下来，让我们创建一个将呈现此模板的控制器。

在 `src/main/java` 目录中创建一个名为 `ContextController.java` 的新文件并添加以下内容：

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

该控制器有一个带注释的“@RequestMapping”方法。此方法将 `/` URL 映射到 `context` 模板。

`context` 模板期望 `message` 属性出现在 `Context` 对象中。此属性通过 `context` 方法添加到 `Context` 对象。

现在我们已经设置了控制器和模板，让我们运行我们的应用程序并查看结果。

将“Application”类作为 Java 应用程序运行，并在浏览器中导航到 http://localhost:8080。您应该看到以下输出：

![你好，Thymeleaf！](https://i.imgur.com/ePcUg9x.png)

如您所见，我们的模板已呈现，并且“message”属性用于填充“<h1>”元素。

## 结论

在本文中，我们了解了如何将 Thymeleaf 模板引擎与 Spring Boot 结合使用来创建动态 HTML 页面。

我们还看到了如何使用 `Model` 和 `Context` 对象将数据传递给模板。

Thymeleaf 是一个强大的模板引擎，可用于创建动态和复杂的 Web 应用程序。