---
title: 092: Spring Boot와 WebSocket으로 채팅 애플리케이션 만들기
description: 
published: true
date: 2023-02-05T22:32:31.875Z
tags: 
editor: markdown
dateCreated: 2023-02-05T22:32:30.221Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [092: Building a Chat Application with Spring Boot and WebSockets***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/092-building-a-chat-application-with-spring-boot-and-websockets)
{.links-list}


# 092: Spring Boot와 WebSocket으로 채팅 애플리케이션 만들기

이 게시물에서는 Spring Boot 및 WebSocket을 사용하여 채팅 애플리케이션을 빌드하는 방법을 살펴보겠습니다.

WebSocket은 웹 브라우저와 서버 간의 양방향 전이중 영구 연결입니다. 그들은 둘 사이의 실시간 통신을 허용합니다.

Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 응용 프로그램을 쉽게 만들 수 있는 Java 기반 프레임워크입니다.

## 프로젝트 설정

Spring Initializr를 사용하여 프로젝트를 설정할 것입니다. https://start.spring.io/로 이동하여 다음을 선택합니다.

* 웹
* 웹소켓
* 백리향

프로젝트 이름을 "chat-application"으로 지정하고 "프로젝트 생성"을 클릭합니다.

## 종속성

Spring Boot는 프로젝트에 필요한 종속성을 자동으로 구성합니다.

## 웹소켓

WebSocket은 컨트롤러에 의해 처리됩니다. 우리 프로젝트에서 `ChatController.java`라는 컨트롤러를 만들 것입니다.

```java
@Controller
public class ChatController {

    @MessageMapping("/chat")
    @SendTo("/topic/messages")
    public String sendMessage(String message) {
        return message;
    }
}
```

`@MessageMapping` 주석은 특정 URL을 컨트롤러 메서드에 매핑합니다. `@SendTo` 주석은 WebSocket 서버 엔드포인트의 URL을 지정합니다. 그런 다음 메시지는 해당 끝점에 연결된 모든 클라이언트에 브로드캐스트됩니다.

HTML 파일에서 입력 필드와 제출 버튼이 있는 양식을 추가합니다. 양식은 `/chat` 엔드포인트에 POST됩니다.

```html
<form action="/chat" th:action="@{/chat}" th:object="${message}" method="post">
    <input type="text" th:field="*{text}"/>
    <input type="submit" value="Send"/>
</form>
```

입력 필드는 `message` 개체의 `text` 속성에 바인딩됩니다. 폼이 제출되면 `message` 객체가 `ChatController`의 `sendMessage` 메서드로 전달되고 `text` 속성이 브로드캐스트할 메시지로 사용됩니다.

## 방송 메시지

'SimpMessagingTemplate'을 사용하여 메시지를 특정 대상으로 브로드캐스트할 수 있습니다.

```java
@Autowired
private SimpMessagingTemplate template;

@MessageMapping("/chat")
@SendTo("/topic/messages")
public String sendMessage(String message) {
    this.template.convertAndSend("/topic/messages", message);
    return message;
}
```

`convertAndSend` 메서드는 메시지를 JSON으로 변환하고 지정된 대상으로 보냅니다.

## 메시지 수신

특정 URL을 메서드에 매핑하기 위해 `@SubscribeMapping` 주석을 사용할 수 있습니다. 이 메서드는 클라이언트가 URL을 구독할 때 호출됩니다.

```java
@Controller
public class ChatController {

    @Autowired
    private SimpMessagingTemplate template;

    @MessageMapping("/chat")
    @SendTo("/topic/messages")
    public String sendMessage(String message) {
        this.template.convertAndSend("/topic/messages", message);
        return message;
    }

    @SubscribeMapping("/topic/messages")
    public List<String> subscribe() {
        List<String> messages = new ArrayList<>();
        messages.add("Hello");
        messages.add("Welcome");
        return messages;
    }
}
```

`subscribe` 메서드는 클라이언트가 `/topic/messages` 대상을 구독할 때 클라이언트에 보낼 메시지 목록을 반환합니다.

## 애플리케이션 테스트

애플리케이션을 실행하고 http://localhost:8080/으로 이동하여 애플리케이션을 테스트할 수 있습니다. 양식과 메시지 목록이 표시되어야 합니다.

브라우저의 개발자 도구를 열고 네트워크 탭으로 이동할 수도 있습니다. WebSocket 연결이 설정되는 것을 볼 수 있습니다.

## 결론

이번 포스트에서는 Spring Boot와 WebSocket으로 채팅 애플리케이션을 빌드하는 방법을 살펴보았습니다.