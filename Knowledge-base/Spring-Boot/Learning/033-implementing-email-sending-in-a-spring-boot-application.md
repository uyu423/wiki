---
title: 033: Spring Boot 애플리케이션에서 이메일 전송 구현
description: 
published: true
date: 2023-02-04T01:32:45.764Z
tags: 
editor: markdown
dateCreated: 2023-02-04T01:32:44.106Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [033: Implementing email sending in a Spring Boot application***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/033-implementing-email-sending-in-a-spring-boot-application)
{.links-list}


이메일 전송은 많은 응용 프로그램의 기본적인 부분입니다. 사용자에게 시스템 이벤트를 알리는 것부터 암호 재설정 및 확인 이메일을 보내는 것까지 모든 것에 사용됩니다.

이 게시물에서는 Spring Boot 애플리케이션에 이메일 기능을 추가하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

* Spring Boot에서 이메일 전송 구성
* 간단한 이메일 보내기
* HTML 이메일 보내기
* 첨부파일 보내기

## Spring Boot에서 이메일 전송 구성

Spring Boot를 사용하면 애플리케이션에서 이메일 전송을 쉽게 구성할 수 있습니다. 필요한 것은 올바른 종속성을 추가하고 application.properties 파일에서 몇 가지 속성을 구성하는 것입니다.

가장 먼저 해야 할 일은 프로젝트에 spring-boot-starter-mail 의존성을 추가하는 것입니다. 이 스타터는 Spring Boot에서 이메일 전송을 시작하는 데 필요한 모든 종속성을 가져옵니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```

종속성이 있으면 application.properties 파일에서 다음 속성을 구성할 수 있습니다.

* spring.mail.host= # SMTP 서버 호스트. 예: smtp.gmail.com.
* spring.mail.port= # SMTP 서버 포트. 예: 587.
* spring.mail.username= # SMTP 서버에 연결하는 데 사용할 계정의 사용자 이름.
* spring.mail.password= # SMTP 서버에 연결하는 데 사용할 계정의 암호.
* spring.mail.protocol= # SMTP 서버에 연결할 때 사용할 프로토콜. 예를 들어, smtp.
* spring.mail.properties.mail.smtp.auth=true # SMTP 서버에 연결할 때 인증 사용 여부.
* spring.mail.properties.mail.smtp.starttls.enable=true # SMTP 서버에 연결할 때 STARTTLS를 사용할지 여부.

## 간단한 이메일 보내기

이제 Spring Boot 애플리케이션에서 이메일 전송을 구성했으므로 간단한 이메일을 보내는 방법을 살펴보겠습니다.

가장 먼저 필요한 것은 JavaMailSender 인터페이스의 인스턴스입니다. 이 인터페이스는 이메일을 보내는 방법을 제공합니다. @Autowired 주석을 사용하여 이 인터페이스를 Spring Boot 애플리케이션에 삽입할 수 있습니다.

```java
@Autowired
private JavaMailSender javaMailSender;
```

JavaMailSender 인터페이스의 인스턴스가 있으면 다음 코드를 사용하여 간단한 이메일을 보낼 수 있습니다.

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

위의 코드에서는 JavaMailSender 인터페이스의 send() 메서드를 사용하여 이메일을 보냅니다. 또한 이메일 메시지를 준비하기 위해 MimeMessagePreparator를 사용하고 있습니다.

MimeMessagePreparator는 전송되기 전에 MimeMessage 인스턴스를 준비할 수 있는 인터페이스입니다. 이는 이메일에 헤더나 첨부 파일을 설정하는 것과 같은 작업을 수행해야 하는 경우에 유용합니다.

위의 코드에서 MimeMessageHelper 클래스를 사용하여 이메일 메시지를 준비하고 있습니다. MimeMessageHelper 클래스는 일반적인 이메일 헤더 및 본문 콘텐츠를 설정하기 위한 편리한 메서드를 제공합니다.

이메일 메시지가 준비되면 JavaMailSender 인터페이스의 send() 메서드로 전달되고 이메일이 전송됩니다.

## HTML 이메일 보내기

간단한 텍스트 이메일을 보내는 것 외에도 Spring Boot를 사용하여 HTML 이메일을 보낼 수도 있습니다. 이렇게 하려면 이메일의 텍스트 메시지를 HTML 문자열로 설정하기만 하면 됩니다.

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

위의 코드에서 이메일의 텍스트 메시지를 HTML 문자열로 설정하고 있습니다. 또한 setText() 메서드의 두 번째 매개변수를 true로 설정합니다. 이는 MimeMessageHelper에게 텍스트 메시지가 HTML이며 HTML로 렌더링되어야 함을 알려줍니다.

## 첨부 파일 보내기

Spring Boot를 사용하여 이메일 메시지와 함께 첨부 파일을 보낼 수도 있습니다. 이렇게 하려면 MimeMessageHelper 클래스의 addAttachment() 메서드를 사용하기만 하면 됩니다.

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

위의 코드에서는 addAttachment() 메서드를 사용하여 전자 메일 메시지에 첨부 파일을 추가합니다. 첫 번째 매개변수는 첨부 파일의 이름이고 두 번째 매개변수는 첨부할 파일입니다.

addAttachment() 메서드를 여러 번 호출하여 전자 메일 메시지에 여러 첨부 파일을 추가할 수 있습니다.

## 결론

이 게시물에서는 Spring Boot 애플리케이션에 이메일 기능을 추가하는 방법을 살펴보았습니다. 우리는 다음 주제를 다루었습니다.

* Spring Boot에서 이메일 전송 구성
* 간단한 이메일 보내기
* HTML 이메일 보내기
* 첨부파일 보내기

이 게시물에서 얻은 지식으로 모든 Spring Boot 애플리케이션에 이메일 기능을 추가할 수 있어야 합니다.