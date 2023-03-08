---
title: 038: Spring Boot와 WebSocket을 사용하여 채팅 애플리케이션 만들기
description: 
published: true
date: 2023-02-04T06:32:23.442Z
tags: 
editor: markdown
dateCreated: 2023-02-04T06:32:21.663Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [038: Building a chat application using Spring Boot and WebSockets***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/038-building-a-chat-application-using-spring-boot-and-websockets)
{.links-list}


# 038: Spring Boot와 WebSocket을 사용하여 채팅 애플리케이션 빌드하기

WebSocket은 채팅 애플리케이션과 같은 실시간 애플리케이션을 구축하기 위한 강력한 도구입니다. 이 게시물에서는 Spring Boot 및 WebSocket을 사용하여 채팅 애플리케이션을 빌드하는 방법을 보여줍니다.

## 프로젝트 설정

시작하려면 새 Spring Boot 프로젝트를 생성해야 합니다. [Spring Initializr](https://start.spring.io/)를 사용하여 이를 수행할 수 있습니다. Web 및 WebSocket 종속성을 선택해야 합니다.

프로젝트를 설정했으면 `pom.xml`에 다음 종속성을 추가해야 합니다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-websocket</artifactId>
</dependency>
```

## WebSocket 구성

다음으로 `application.properties` 파일에서 WebSocket을 구성해야 합니다.

```properties
server.port=8080

spring.websocket.server.port=8081
spring.websocket.server.path=/ws
```

## WebSocket 끝점 만들기

이제 프로젝트가 설정되었으므로 WebSocket 엔드포인트 빌드를 시작할 수 있습니다. `ChatEndpoint`라는 새 클래스를 만들고 `@ServerEndpoint`로 주석을 답니다. 이 주석은 이 클래스가 WebSocket 끝점임을 Spring에 알립니다.

```java
@ServerEndpoint("/ws")
public class ChatEndpoint {

}
```

## 메시지 보내기 및 받기

다음 단계는 메시지를 보내고 받는 방법을 추가하는 것입니다. `@OnMessage` 주석은 메서드를 메시지 처리기로 표시하는 데 사용됩니다. 이 메서드는 WebSocket 끝점에서 메시지를 받을 때마다 호출됩니다.

```java
@OnMessage
public void handleMessage(String message, Session session) {
    // do something with the message
}
```

메시지를 보내려면 `Session.getBasicRemote().sendText(message)` 메서드를 사용할 수 있습니다.

```java
@OnMessage
public void handleMessage(String message, Session session) {
    session.getBasicRemote().sendText("Echo: " + message);
}
```

## 채팅 애플리케이션 테스트

[WebSocket.org Echo Test](https://www.websocket.org/echo.html)를 사용하여 채팅 애플리케이션을 테스트할 수 있습니다. WebSocket 끝점(ws://localhost:8081/ws)을 입력하고 메시지 보내기를 시작합니다. 보낸 메시지가 다시 울려퍼지는 것을 볼 수 있습니다.

## 결론

이 게시물에서는 Spring Boot 및 WebSocket을 사용하여 채팅 애플리케이션을 빌드하는 방법을 보여 주었습니다. WebSocket은 실시간 애플리케이션을 구축하기 위한 강력한 도구입니다.