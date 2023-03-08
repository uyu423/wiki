---
title: 033: 在 Spring Boot 应用程序中实现电子邮件发送
description: 
published: true
date: 2023-02-04T01:32:45.764Z
tags: 
editor: markdown
dateCreated: 2023-02-04T01:32:44.106Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [033: Implementing email sending in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/033-implementing-email-sending-in-a-spring-boot-application)
{.links-list}


电子邮件是许多应用程序的基本组成部分。它用于从通知用户系统事件到发送密码重置和确认电子邮件的所有内容。

在本文中，我们将探讨如何向 Spring Boot 应用程序添加电子邮件功能。我们将涵盖以下主题：

* 在 Spring Boot 中配置邮件发送
* 发送简单的电子邮件
* 发送 HTML 电子邮件
* 发送附件

## 在 Spring Boot 中配置邮件发送

Spring Boot 可以轻松地在您的应用程序中配置电子邮件发送。您只需添加正确的依赖项并在 application.properties 文件中配置一些属性。

您需要做的第一件事是将 spring-boot-starter-mail 依赖项添加到您的项目中。这个 starter 将引入您开始在 Spring Boot 中发送电子邮件所需的所有依赖项。

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```

建立依赖关系后，您可以在 application.properties 文件中配置以下属性：

* spring.mail.host= # SMTP 服务器主机。例如，smtp.gmail.com。
* spring.mail.port= # SMTP 服务器端口。例如，587。
* spring.mail.username= # 用于连接到 SMTP 服务器的帐户的用户名。
* spring.mail.password= # 用于连接到 SMTP 服务器的帐户密码。
* spring.mail.protocol= # 连接到 SMTP 服务器时使用的协议。例如，smtp。
* spring.mail.properties.mail.smtp.auth=true # 连接SMTP服务器时是否使用认证。
* spring.mail.properties.mail.smtp.starttls.enable=true # 连接SMTP服务器时是否使用STARTTLS。

## 发送简单的邮件

现在您已经在 Spring Boot 应用程序中配置了电子邮件，让我们看一下如何发送简单的电子邮件。

您首先需要的是 JavaMailSender 接口的一个实例。此接口提供发送电子邮件的方法。您可以使用 @Autowired 注释将此接口注入到您的 Spring Boot 应用程序中。

```java
@Autowired
private JavaMailSender javaMailSender;
```

拥有 JavaMailSender 接口的实例后，您可以使用以下代码发送简单的电子邮件：

```java
javaMailSender.send(new MimeMessagePreparator() {
    public void prepare(MimeMessage mimeMessage) throws Exception {
        MimeMessageHelper messageHelper = new MimeMessageHelper(mimeMessage, true);
        messageHelper.setFrom("sender@example.com");
        messageHelper.setTo("receiver@example.com");
        messageHelper.setSubject("Email subject");
        messageHelper.setText("Email body");
    }
});
```

在上面的代码中，我们使用 JavaMailSender 接口的 send() 方法发送电子邮件。我们还使用 MimeMessagePreparator 来准备电子邮件消息。

MimeMessagePreparator 是一个接口，允许您在发送之前准备 MimeMessage 实例。如果您需要在电子邮件上设置标题或附件等操作，这将非常有用。

在上面的代码中，我们使用 MimeMessageHelper 类来帮助我们准备电子邮件。 MimeMessageHelper 类提供了设置常用电子邮件标头和正文内容的便捷方法。

一旦准备好电子邮件消息，它就会被传递到 JavaMailSender 接口的 send() 方法并发送电子邮件。

## 发送 HTML 邮件

除了发送简单的文本电子邮件，您还可以使用 Spring Boot 发送 HTML 电子邮件。为此，您只需将电子邮件的文本消息设置为 HTML 字符串即可。

```java
javaMailSender.send(new MimeMessagePreparator() {
    public void prepare(MimeMessage mimeMessage) throws Exception {
        MimeMessageHelper messageHelper = new MimeMessageHelper(mimeMessage, true);
        messageHelper.setFrom("sender@example.com");
        messageHelper.setTo("receiver@example.com");
        messageHelper.setSubject("Email subject");
        messageHelper.setText("<p>Email body</p>", true);
    }
});
```

在上面的代码中，我们将电子邮件的文本消息设置为 HTML 字符串。我们还将 setText() 方法的第二个参数设置为 true。这告诉 MimeMessageHelper 文本消息是 HTML 并且应该这样呈现。

## 发送附件

您还可以使用 Spring Boot 发送电子邮件中的附件。为此，您只需使用 MimeMessageHelper 类的 addAttachment() 方法。

```java
javaMailSender.send(new MimeMessagePreparator() {
    public void prepare(MimeMessage mimeMessage) throws Exception {
        MimeMessageHelper messageHelper = new MimeMessageHelper(mimeMessage, true);
        messageHelper.setFrom("sender@example.com");
        messageHelper.setTo("receiver@example.com");
        messageHelper.setSubject("Email subject");
        messageHelper.setText("Email body");
        messageHelper.addAttachment("attachment.txt", new File("attachment.txt"));
    }
});
```

在上面的代码中，我们使用 addAttachment() 方法将附件添加到电子邮件中。第一个参数是附件的名称，第二个参数是要附加的文件。

您可以多次调用 addAttachment() 方法以将多个附件添加到电子邮件中。

## 结论

在本文中，我们了解了如何向 Spring Boot 应用程序添加电子邮件功能。我们涵盖了以下主题：

* 在 Spring Boot 中配置邮件发送
* 发送简单的电子邮件
* 发送 HTML 电子邮件
* 发送附件

借助您在本文中获得的知识，您应该能够向任何 Spring Boot 应用程序添加电子邮件功能。