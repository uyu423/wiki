---
title: 033: Implementing email sending in a Spring Boot application
description: 
published: true
date: 2023-02-04T01:32:49.347Z
tags: 
editor: markdown
dateCreated: 2023-02-04T01:32:44.108Z
---

- [033: Implementación del envío de correo electrónico en una aplicación Spring Boot***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/033-implementing-email-sending-in-a-spring-boot-application)
{.links-list}
- [033: 在 Spring Boot 应用程序中实现电子邮件发送***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/033-implementing-email-sending-in-a-spring-boot-application)
{.links-list}
- [033: Spring Boot 애플리케이션에서 이메일 전송 구현***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/033-implementing-email-sending-in-a-spring-boot-application)
{.links-list}


Emailing is a fundamental part of many applications. It's used for everything from notifying users of system events to sending password resets and confirmation emails. 

In this post, we'll explore how to add emailing capabilities to a Spring Boot application. We'll cover the following topics:

* Configuring email sending in Spring Boot
* Sending simple emails
* Sending HTML emails
* Sending attachments

## Configuring email sending in Spring Boot

Spring Boot makes it easy to configure email sending in your application. All you need is to add the right dependency and configure a few properties in your application.properties file.

The first thing you need to do is add the spring-boot-starter-mail dependency to your project. This starter will pull in all the dependencies you need to get started with emailing in Spring Boot.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```

Once you have the dependency in place, you can configure the following properties in your application.properties file:

* spring.mail.host= # SMTP server host. For example, smtp.gmail.com.
* spring.mail.port= # SMTP server port. For example, 587.
* spring.mail.username= # Username of the account to use to connect to the SMTP server.
* spring.mail.password= # Password of the account to use to connect to the SMTP server.
* spring.mail.protocol= # Protocol to use when connecting to the SMTP server. For example, smtp.
* spring.mail.properties.mail.smtp.auth=true # Whether to use authentication when connecting to the SMTP server.
* spring.mail.properties.mail.smtp.starttls.enable=true # Whether to use STARTTLS when connecting to the SMTP server.

## Sending simple emails

Now that you have emailing configured in your Spring Boot application, let's take a look at how to send a simple email.

The first thing you need is an instance of the JavaMailSender interface. This interface provides methods for sending emails. You can inject this interface into your Spring Boot application using the @Autowired annotation.

```java
@Autowired
private JavaMailSender javaMailSender;
```

Once you have an instance of the JavaMailSender interface, you can use the following code to send a simple email:

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

In the code above, we're using the send() method of the JavaMailSender interface to send an email. We're also using a MimeMessagePreparator to prepare the email message. 

The MimeMessagePreparator is an interface that allows you to prepare a MimeMessage instance before it's sent. This is useful if you need to do things like set headers or attachments on the email. 

In the code above, we're using the MimeMessageHelper class to help us prepare the email message. The MimeMessageHelper class provides convenience methods for setting common email headers and body content. 

Once the email message is prepared, it's passed to the send() method of the JavaMailSender interface and the email is sent.

## Sending HTML emails

In addition to sending simple text emails, you can also send HTML emails using Spring Boot. To do this, you just need to set the text message of the email to be an HTML string.

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

In the code above, we're setting the text message of the email to be an HTML string. We're also setting the second parameter of the setText() method to true. This tells the MimeMessageHelper that the text message is HTML and should be rendered as such. 

## Sending attachments

You can also send attachments with your email messages using Spring Boot. To do this, you just need to use the addAttachment() method of the MimeMessageHelper class.

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

In the code above, we're using the addAttachment() method to add an attachment to the email message. The first parameter is the name of the attachment and the second parameter is the file to be attached. 

You can call the addAttachment() method multiple times to add multiple attachments to an email message.

## Conclusion

In this post, we've seen how to add emailing capabilities to a Spring Boot application. We've covered the following topics:

* Configuring email sending in Spring Boot
* Sending simple emails
* Sending HTML emails
* Sending attachments

With the knowledge you've gained in this post, you should be able to add emailing capabilities to any Spring Boot application.