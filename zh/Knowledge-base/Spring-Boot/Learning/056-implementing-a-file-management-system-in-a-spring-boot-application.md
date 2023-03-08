---
title: 056: 在 Spring Boot 应用程序中实现文件管理系统
description: 
published: true
date: 2023-02-03T20:17:31.192Z
tags: 
editor: markdown
dateCreated: 2023-02-03T20:17:29.564Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [056: Implementing a file management system in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/056-implementing-a-file-management-system-in-a-spring-boot-application)
{.links-list}


# 在 Spring Boot 应用程序中实现文件管理系统

Spring Boot 是一个基于 Java 的框架，允许您创建独立的、生产级的 Spring 应用程序。在本文中，我们将向您展示如何在 Spring Boot 应用程序中实现文件管理系统。

## 先决条件

- 一些Java开发经验
- 使用Spring框架的一些经验

## 入门

首先，我们需要创建一个新的 Spring Boot 项目。我们可以使用 [Spring Initializr](https://start.spring.io/) 来做到这一点。

![Spring Initializr](https://i.imgur.com/hmvkF9r.png)

填写项目详情：

- 组：com.example
- 工件：文件管理系统
- 名称：文件管理系统
- 描述：一个用Spring Boot实现的文件管理系统
- 包名：com.example.filemanagementsystem
- 类型：Maven 项目
- 包装：罐
- Java 版本：8
- 选择以下依赖项：
  - 网络
  - 百里香叶
  - 龙目岛

单击“生成项目”以下载项目。

## 项目结构

生成项目后，我们应该具有以下项目结构：

```
.
├── pom.xml
└── src
    └── main
        ├── java
        │   └── com
        │       └── example
        │           └── filemanagementsystem
        │               ├── FileManagementSystemApplication.java
        │               ├── controller
        │               │   └── FileController.java
        │               └── model
        │                   └── File.java
        └── resources
            ├── application.properties
            └── templates
                └── index.html
```

## 实现文件管理系统

现在我们已经设置了一个基本的项目，我们可以开始实现我们的文件管理系统了。

### 创建模型

我们的文件管理系统需要存储有关正在管理的文件的信息。我们可以通过创建一个“文件”模型来做到这一点：

```java
@Data
@Builder
@NoArgsConstructor
@AllArgsConstructor
public class File {

    private String name;
    private String type;
    private long size;
}
```

[Lombok](https://projectlombok.org/) 库中的“@Data”注释将为我们生成 getter、setter 和 toString 方法。 `@Builder` 注释将允许我们使用构建器模式创建 `File` 对象。 `@NoArgsConstructor` 和`@AllArgsConstructor` 注释将分别生成一个无参数构造函数和一个将所有字段作为参数的构造函数。

### 创建控制器

接下来，我们需要创建一个控制器来处理对我们的文件管理系统的请求。我们可以通过创建一个 FileController 来做到这一点：

```java
@Slf4j
@Controller
@RequestMapping("/files")
public class FileController {

    @GetMapping
    public String listFiles(Model model) {
        // TODO: Implement this method
        return "index";
    }

    @PostMapping
    public String uploadFile(@RequestParam("file") MultipartFile file) {
        // TODO: Implement this method
        return "redirect:/files";
    }

    @GetMapping("/{id}")
    public ResponseEntity<Resource> downloadFile(@PathVariable String id) {
        // TODO: Implement this method
        return null;
    }
}
```

来自 Lombok 库的“@Slf4j”注释将为我们生成一个记录器。 `@Controller` 注释会将此类标记为控制器。 `@RequestMapping` 注释会将控制器的所有方法映射到 `/files` 路径。

`listFiles` 方法将处理对 `/files` 路径的 GET 请求。它会将 `Model` 对象作为参数并返回一个字符串，指示应呈现哪个模板。

`uploadFile` 方法将处理对 `/files` 路径的 POST 请求。它将一个“MultipartFile”对象作为参数并返回一个字符串，指示应呈现哪个模板。

`downloadFile` 方法将处理对 `/files/{id}` 路径的 GET 请求。它将一个字符串 id 作为参数并返回一个包含所请求文件的“ResponseEntity”对象。

### 创建模板

我们需要为我们的文件管理系统创建两个模板：一个用于列出文件，一个用于上传文件。我们可以通过在 src/main/resources/templates 目录中创建一个 index.html 文件来做到这一点：

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>File Management System</title>
</head>
<body>
    <h1>File Management System</h1>

    <table>
        <thead>
            <tr>
                <th>Name</th>
                <th>Type</th>
                <th>Size</th>
                <th></th>
            </tr>
        </thead>
        <tbody>
            <tr th:each="file : ${files}">
                <td th:text="${file.name}"></td>
                <td th:text="${file.type}"></td>
                <td th:text="${file.size}"></td>
                <td><a href="/files/[[${file.id}]]">Download</a></td>
            </tr>
        </tbody>
    </table>

    <form method="post" enctype="multipart/form-data">
        <div>
            <label>File:</label>
            <input type="file" name="file"/>
        </div>
        <div>
            <button type="submit">Upload</button>
        </div>
    </form>
</body>
</html>
```

此模板将列出所有已上传的文件并提供用于上传新文件的表单。

### 配置 Spring Boot

我们需要在我们的 application.properties 文件中配置一些东西：

```properties
spring.thymeleaf.mode=HTML5
spring.thymeleaf.encoding=UTF-8
spring.thymeleaf.content-type=text/html
server.port=8080
```

`spring.thymeleaf.mode`、`spring.thymeleaf.encoding` 和 `spring.thymeleaf.content-type` 属性将配置 Thymeleaf 以分别使用 HTML5、UTF-8 编码和 text/html 内容类型。 `server.port` 属性将服务器配置为在端口 8080 上运行。

## 运行应用程序

我们现在可以运行我们的应用程序并对其进行测试。

首先，我们需要构建我们的项目。我们可以通过运行以下命令来完成此操作：

```
$ ./mvnw clean package
```

接下来，我们可以使用以下命令运行我们的应用程序：

```
$ java -jar target/file-management-system-0.0.1-SNAPSHOT.jar
```

我们现在可以通过 http://localhost:8080 访问我们的文件管理系统。

## 结论

在本文中，我们向您展示了如何在 Spring Boot 应用程序中实现文件管理系统。