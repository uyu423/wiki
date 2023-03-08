---
title: 014: Spring Boot 및 WebSocket 작업
description: 
published: true
date: 2023-02-03T09:18:03.826Z
tags: 
editor: markdown
dateCreated: 2023-02-03T09:17:58.701Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [014: Working with Spring Boot and WebSockets***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/014-working-with-spring-boot-and-websockets)
{.links-list}


# 014: Spring Boot와 WebSocket으로 작업하기

WebSocket은 실시간 애플리케이션을 구축하기 위한 강력한 도구입니다. Spring Boot를 사용하면 WebSocket을 쉽게 사용할 수 있습니다. 이 게시물에서는 Spring Boot 및 WebSocket을 사용하는 방법을 배웁니다.

## WebSocket이 무엇인가요?

WebSocket은 클라이언트와 서버 간의 전이중 통신을 허용하는 통신 프로토콜입니다. 이는 클라이언트와 서버가 동시에 데이터를 보내고 받을 수 있음을 의미합니다.

WebSocket은 실시간 애플리케이션을 구축하는 좋은 방법입니다. 빠르고 효율적이며 데이터가 제공되는 즉시 클라이언트에 데이터를 푸시할 수 있습니다.

## 스프링 부트 설정

간단한 Spring Boot 애플리케이션을 설정하여 시작하겠습니다. Spring Initializr를 사용하여 프로젝트를 생성합니다.

Spring Initializr 웹 사이트(https://start.spring.io/)로 이동합니다.

다음 옵션을 선택합니다.

- 프로젝트: 메이븐 프로젝트
- 언어: 자바
- 스프링 부트 버전: 2.1.3
- 그룹: com.example
- 아티팩트: websockets-demo

프로젝트 생성을 클릭합니다.

이제 시작하는 데 필요한 모든 것이 포함된 zip 파일이 있어야 합니다. 파일의 압축을 풀고 원하는 IDE에서 엽니다.

## WebSocket 끝점 만들기

간단한 WebSocket 끝점을 만들어 시작하겠습니다. @ServerEndpoint 주석을 사용하여 엔드포인트를 생성합니다.

com.example.websockets.demo 패키지에 새 Java 클래스를 만들고 이름을 MyWebSocketEndpoint.java로 지정합니다.

MyWebSocketEndpoint.java 파일에 다음 코드를 추가합니다.

```java
@ServerEndpoint("/websocket")
public class MyWebSocketEndpoint {

}
```

@ServerEndpoint 주석은 WebSocket 끝점을 만드는 데 사용됩니다. 주석 값은 엔드포인트에 액세스하는 데 사용되는 경로입니다.

## 메시지 보내기 및 받기

이제 엔드포인트가 있으므로 메시지를 보내고 받는 코드를 추가해 보겠습니다.

MyWebSocketEndpoint.java 파일에 다음 코드를 추가합니다.

```java
@ServerEndpoint("/websocket")
public class MyWebSocketEndpoint {

@OnOpen
public void onOpen(Session session) {
    // do something when the connection is opened
}

@OnMessage
public void onMessage(String message, Session session) {
    // do something when a message is received
}

@OnClose
public void onClose(Session session) {
    // do something when the connection is closed
}

@OnError
public void onError(Throwable error) {
    // do something when there is an error
}
}
```

@OnOpen 주석은 연결이 열릴 때 호출될 메서드를 지정하는 데 사용됩니다. @OnMessage 어노테이션은 메시지가 수신될 때 호출될 메소드를 지정하는 데 사용됩니다. @OnClose 주석은 연결이 닫힐 때 호출될 메서드를 지정하는 데 사용됩니다. @OnError 주석은 오류가 있을 때 호출될 메서드를 지정하는 데 사용됩니다.

## 끝점 구성

이제 엔드포인트가 있으므로 구성해 보겠습니다.

MyWebSocketEndpoint.java 파일에 다음 코드를 추가합니다.

```java
@ServerEndpoint("/websocket")
public class MyWebSocketEndpoint {

@OnOpen
public void onOpen(Session session) {
    // do something when the connection is opened
}

@OnMessage
public void onMessage(String message, Session session) {
    // do something when a message is received
}

@OnClose
public void onClose(Session session) {
    // do something when the connection is closed
}

@OnError
public void onError(Throwable error) {
    // do something when there is an error
}
}
```

@ServerEndpoint 주석은 WebSocket 끝점을 만드는 데 사용됩니다. 주석 값은 엔드포인트에 액세스하는 데 사용되는 경로입니다.

@OnOpen 주석은 연결이 열릴 때 호출될 메서드를 지정하는 데 사용됩니다. @OnMessage 어노테이션은 메시지가 수신될 때 호출될 메소드를 지정하는 데 사용됩니다. @OnClose 주석은 연결이 닫힐 때 호출될 메서드를 지정하는 데 사용됩니다. @OnError 주석은 오류가 있을 때 호출될 메서드를 지정하는 데 사용됩니다.

## 끝점 테스트

이제 엔드포인트가 있으므로 테스트해 보겠습니다.

com.example.websockets.demo 패키지에 새 Java 클래스를 만들고 이름을 MyWebSocketEndpointTest.java로 지정합니다.

MyWebSocketEndpointTest.java 파일에 다음 코드를 추가합니다.

```java
@Test
public void testMyWebSocketEndpoint() throws Exception {
    URI uri = new URI("ws://localhost:8080/websocket");
    WebSocketContainer container = ContainerProvider.getWebSocketContainer();
    Session session = container.connectToServer(MyWebSocketEndpoint.class, uri);
    session.getBasicRemote().sendText("Hello world!");
    session.close();
}
```

testMyWebSocketEndpoint() 메서드에서 WebSocket 끝점에 대한 URI를 만듭니다. 그런 다음 WebSocketContainer를 생성하고 엔드포인트에 연결합니다. 서버에 메시지를 보낸 다음 연결을 닫습니다.

테스트를 실행하면 다음 출력이 표시됩니다.

```
Hello world!
```

## 결론

이 게시물에서는 Spring Boot 및 WebSocket을 사용하는 방법을 배웠습니다. 간단한 WebSocket 끝점을 만들고 테스트했습니다.