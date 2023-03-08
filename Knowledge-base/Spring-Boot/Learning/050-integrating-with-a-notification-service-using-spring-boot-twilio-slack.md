---
title: 050: Spring Boot(Twilio, Slack)를 사용하여 알림 서비스와 통합
description: 
published: true
date: 2023-02-04T16:32:26.915Z
tags: 
editor: markdown
dateCreated: 2023-02-04T16:32:25.327Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [050: Integrating with a notification service using Spring Boot (Twilio, Slack)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/050-integrating-with-a-notification-service-using-spring-boot-twilio-slack)
{.links-list}


# 050: Spring Boot(Twilio, Slack)를 이용한 알림 서비스 연동

이번 포스팅에서는 Spring Boot를 이용하여 알림 서비스와 연동하는 방법에 대해 알아보겠습니다. 예제에서는 Twilio와 Slack을 사용하지만 다른 알림 서비스에도 동일한 원칙을 적용할 수 있습니다.

## 환경 설정

시작하기 전에 환경을 설정해야 합니다. 이 게시물에서는 Java 개발 환경을 사용한다고 가정합니다.

먼저 Spring Boot CLI를 설치해야 합니다. https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started-installing-spring-boot.html에서 지침을 찾을 수 있습니다.

Spring Boot CLI를 설치했으면 새 프로젝트를 생성해야 합니다. 다음 명령을 실행하여 그렇게 할 수 있습니다.

```
$ spring init -d=web,jpa,thymeleaf my-project
```

그러면 웹, JPA 및 Thymeleaf 종속성을 포함하는 새로운 Spring Boot 프로젝트가 생성됩니다.

다음으로 프로젝트에 다음 종속성을 추가해야 합니다.

```
$ cd my-project
$ ./mvnw install

...

<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-thymeleaf</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>com.twilio.sdk</groupId>
        <artifactId>twilio-java-sdk</artifactId>
        <version>7.0.0</version>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-test</artifactId>
        <scope>test</scope>
    </dependency>
</dependencies>
```

## Twilio 구성

이제 프로젝트가 설정되었으므로 Twilio 구성을 시작할 수 있습니다. 가장 먼저 해야 할 일은 Twilio 계정에 가입하는 것입니다. 여기에서 할 수 있습니다: https://www.twilio.com/try-twilio

계정이 있으면 새 프로젝트를 만들어야 합니다. 대시보드에서 "새 프로젝트 만들기" 버튼을 클릭하면 됩니다.

프로젝트 이름을 지정하고 "프로젝트 만들기"를 클릭합니다.

프로젝트가 생성되면 새 API 키를 생성해야 합니다. 대시보드 왼쪽에 있는 "API 키" 링크를 클릭하면 됩니다.

"새 API 키 만들기" 버튼을 클릭하고 키 이름을 지정합니다.

키가 생성되면 클립보드에 복사해야 합니다. 잠시 후에 사용하겠습니다.

## 슬랙 구성

이제 Twilio 계정이 설정되었으므로 Slack 구성을 시작할 수 있습니다. 가장 먼저 해야 할 일은 Slack 계정에 가입하는 것입니다. https://slack.com/에서 그렇게 할 수 있습니다.

계정이 있으면 새 채널을 만들어야 합니다. 대시보드 왼쪽에 있는 "채널" 링크를 클릭하면 됩니다.

채널 이름을 지정하고 "채널 만들기"를 클릭합니다.

채널이 생성되면 팀원을 초대해야 합니다. 채널 오른쪽에 있는 "사람 초대" 링크를 클릭하면 됩니다.

초대할 사람들의 이메일 주소를 입력하고 "초대장 보내기"를 클릭하십시오.

## 알림 보내기

이제 환경이 설정되었으므로 알림 전송을 시작할 수 있습니다.

Twilio를 사용하여 알림을 보내려면 다음 코드를 사용해야 합니다.

```java
// Replace these with your own values
String accountSid = "YOUR_TWILIO_ACCOUNT_SID";
String authToken = "YOUR_TWILIO_AUTH_TOKEN";

// Initialize the Twilio client
Twilio.init(accountSid, authToken);

// Create the notification
Notification notification = Notification.creator(
        new PhoneNumber("+11234567890"), // to
        new PhoneNumber("+10987654321"), // from
        "Hello world!" // body
).create();
```

Slack을 사용하여 알림을 보내려면 다음 코드를 사용해야 합니다.

```java
// Replace these with your own values
String channelId = "YOUR_SLACK_CHANNEL_ID";
String apiKey = "YOUR_SLACK_API_KEY";

// Initialize the Slack client
Slack slack = Slack.getInstance(apiKey);

// Create the notification
Notification notification = slack.notify(
        channelId, // channel
        "Hello world!" // message
);
```

## 결론

이번 포스팅에서는 Spring Boot를 이용하여 알림 서비스와 연동하는 방법에 대해 알아보았습니다. 예제에는 Twilio와 Slack을 사용했지만 동일한 원칙을 다른 알림 서비스에도 적용할 수 있습니다.