---
title: 047: 在 Spring Boot 应用程序中实现文件上传
description: 
published: true
date: 2023-02-04T13:32:32.037Z
tags: 
editor: markdown
dateCreated: 2023-02-04T13:32:26.495Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [047: Implementing a file upload in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/047-implementing-a-file-upload-in-a-spring-boot-application)
{.links-list}


# 在 Spring Boot 应用程序中实现文件上传

在这篇文章中，我们将看看如何在 Spring Boot 应用程序中实现文件上传。

我们将从查看 @ConfigurationProperties 注释以及如何使用它来配置 Spring Boot 中的文件上传开始。然后我们将创建一个简单的 HTML 表单，允许用户选择要上传的文件。最后，我们将实现一个控制器来处理文件上传并将文件保存到服务器上的目录中。

## 在 Spring Boot 中配置文件上传

Spring Boot 提供了许多可用于在 Spring Boot 应用程序中配置文件上传的属性。这些属性以 ```spring.servlet.multipart.``` 为前缀。

最重要的属性是```spring.servlet.multipart.enabled```。此属性必须设置为 ```true``` 以在 Spring Boot 中启用文件上传。

下一个属性是 ```spring.servlet.multipart.file-size-threshold```。此属性指定将存储在内存中的文件的大小阈值。大于此阈值的文件将写入磁盘上的临时文件。

我们要看的最后一个属性是```spring.servlet.multipart.location```。此属性指定服务器上将存储上传文件的位置。此位置必须是应用程序运行时用户可写的目录。

## 为文件上传创建一个 HTML 表单

现在我们已经为文件上传配置了 Spring Boot，我们需要创建一个 HTML 表单，允许用户选择要上传的文件。

表单应该有一个```文件```输入字段和一个```提交```按钮。 ```file``` 输入字段应将 ```multiple``` 属性设置为 ```true```。这将允许用户选择多个文件进行上传。

```form``` 元素的```action``` 属性应设置为将处理文件上传的控制器的 URL。 ```method``` 属性应设置为 ```POST```。

## 实现文件上传控制器

现在我们有了一个上传文件的表单，我们需要实现一个处理文件上传的控制器。

控制器应该有一个 ```@PostMapping``` 注释，值为 ```/upload```。这会将 URL ```/upload``` 映射到控制器方法。

控制器方法应该有一个 ```@RequestParam``` 注释，值为 ```file```。这会将 ```file``` 输入字段绑定到 ```MultipartFile``` 对象。

控制器方法还应该有一个 ```@ResponseBody``` 注释。这将导致控制器方法返回上传文件的内容作为对请求的响应。

最后，控制器方法应该有一个带有值```/upload```的```@RequestMapping```注释。这会将 URL ```/upload``` 映射到控制器方法。

## 保存上传的文件

文件上传后，我们需要将其保存到我们之前配置的目录中。我们可以通过在 ```MultipartFile``` 对象上调用 ```transferTo()``` 方法来做到这一点。

```transferTo()``` 方法将 ```File``` 对象作为参数。我们可以通过将配置的位置与上传文件的原始文件名连接来创建一个 ```File``` 对象。

文件传输完成后，我们可以返回一个带有“201”状态代码的“ResponseEntity”对象，表示文件已成功上传。

## 结论

在这篇文章中，我们研究了如何在 Spring Boot 应用程序中实现文件上传。我们首先查看 @ConfigurationProperties 注释以及如何使用它在 Spring Boot 中配置文件上传。然后我们创建了一个简单的 HTML 表单，允许用户选择要上传的文件。最后，我们实现了一个控制器来处理文件上传并将文件保存到服务器上的目录中。