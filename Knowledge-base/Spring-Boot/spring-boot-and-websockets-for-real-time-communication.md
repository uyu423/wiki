---
title: 실시간 통신을 위한 Spring Boot 및 WebSocket
description: 
published: true
date: 2023-02-04T10:56:44.407Z
tags: 
editor: markdown
dateCreated: 2023-02-04T10:56:42.581Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Spring Boot and WebSockets for Real-Time Communication***English** document is available*](/en/Knowledge-base/Spring-Boot/spring-boot-and-websockets-for-real-time-communication)
{.links-list}


# 실시간 통신을 위한 스프링 부트와 웹소켓

Websocket은 웹 브라우저와 웹 서버 간의 실시간 통신을 제공하는 수단으로 점차 대중화되고 있습니다. Spring Boot는 Websocket을 사용하는 웹 애플리케이션을 개발하고 배포하는 매우 편리한 방법을 제공합니다.

## WebSocket이 무엇인가요?

WebSocket은 단일 TCP 연결을 통해 전이중 통신 채널을 제공하는 비교적 새로운 기술입니다. 이는 클라이언트와 서버가 동시에 데이터를 보내고 받을 수 있음을 의미합니다.

WebSocket은 특히 채팅 애플리케이션 및 온라인 게임과 같이 짧은 대기 시간이 필요한 애플리케이션에 적합합니다.

## 스프링 부트를 사용하는 이유

Spring Boot는 Java 애플리케이션을 개발하는 데 매우 널리 사용되는 프레임워크입니다. 이를 통해 Spring 기반 애플리케이션을 매우 쉽게 만들고 배포할 수 있습니다.

또한 Spring Boot는 Websocket을 사용하는 웹 애플리케이션을 개발하고 배포하는 매우 편리한 방법을 제공합니다.

## 시작하기

이 섹션에서는 WebSocket을 사용하는 매우 간단한 채팅 애플리케이션을 만듭니다.

우리는 다음과 같은 도구와 기술을 사용할 것입니다.

- 스프링 부트
- 웹소켓
- 자바

### 전제 조건

시작하기 전에 다음 도구가 설치되어 있는지 확인해야 합니다.

- 자바 8
- 메이븐

### 프로젝트 만들기

Spring Initializr를 사용하여 프로젝트를 생성할 것입니다. Spring Initializr는 Spring 기반 프로젝트를 만드는 데 도움이 되는 웹 애플리케이션입니다.

http://start.spring.io로 이동하여 다음 옵션을 선택합니다.

- Java 및 Spring Boot 1.4로 Maven 프로젝트 생성
- 웹
- 웹소켓
- 백리향

"프로젝트 생성"을 클릭하여 프로젝트를 다운로드합니다.

### 프로젝트 설정

프로젝트가 있으면 선호하는 IDE로 가져와야 합니다. IntelliJ IDEA를 사용하고 있습니다.

프로젝트를 가져오면 다음 프로젝트 구조가 표시됩니다.

```
├── pom.xml
└── src
    └── main
        ├── java
        │   └── com
        │       └── example
        │           └── websockets
        │               └── Application.java
        └── resources
            ├── application.properties
            └── templates
                └── index.html
```

### WebSocket 핸들러 구현

WebSocket 핸들러를 구현하는 것으로 시작하겠습니다. 이것은 클라이언트로부터 메시지를 받고 클라이언트에게 메시지를 보내는 구성 요소입니다.

`com.example.websockets` 패키지에 `MessageHandler`라는 새 Java 클래스를 만듭니다.

`MessageHandler` 클래스에 다음 코드를 추가합니다.

```java
@Component
public class MessageHandler {

    private final SimpMessagingTemplate messagingTemplate;

    @Autowired
    public MessageHandler(SimpMessagingTemplate messagingTemplate) {
        this.messagingTemplate = messagingTemplate;
    }

    @MessageMapping("/send/message")
    public void onReceiveMessage(String message) {
        System.out.println("Received message: " + message);
        messagingTemplate.convertAndSend("/topic/messages", message);
    }
}
```

`MessageHandler` 클래스에서 어떤 일이 일어나는지 살펴보겠습니다.

먼저 `@Component`로 클래스에 주석을 답니다. 이것은 이것이 다른 구성 요소에 주입될 수 있는 구성 요소임을 Spring에 알립니다.

다음으로 `SimpMessagingTemplate` 필드를 만들고 `@Autowired`로 주석을 답니다. 이것은 이 필드에 `SimpMessagingTemplate`의 인스턴스를 삽입하도록 Spring에 지시합니다.

`SimpMessagingTemplate`은 WebSocket을 통해 클라이언트에 메시지를 보내기 위해 Spring에서 제공하는 구성 요소입니다.

다음으로 `SimpMessagingTemplate`을 매개변수로 사용하는 생성자를 생성합니다. 이 생성자는 Spring이 `messagingTemplate` 필드에 `SimpMessagingTemplate`의 인스턴스를 주입할 때 호출됩니다.

마지막으로 `onReceiveMessage`라는 `@MessageMapping` 주석 메서드가 있습니다. 이 메서드는 메시지가 `/send/message` 끝점으로 전송될 때 호출됩니다.

`@MessageMapping` 주석은 `/send/message` 엔드포인트에서 메시지를 수신할 때 이 메서드를 호출해야 한다고 Spring에 알립니다.

`onReceiveMessage` 메소드는 `String` 매개변수를 사용합니다. 클라이언트에서 보낸 메시지입니다.

`onReceiveMessage` 메서드 내에서 콘솔에 메시지를 인쇄한 다음 `messagingTemplate`을 사용하여 메시지를 `/topic/messages` 엔드포인트로 보냅니다.

`/topic/messages` 엔드포인트는 모든 클라이언트가 구독하는 주제입니다. 메시지가 이 엔드포인트로 전송되면 주제를 구독하는 모든 클라이언트가 메시지를 수신합니다.

### WebSocket 구성 구현

다음으로 WebSocket 구성을 구현해야 합니다. 이것은 WebSocket 연결을 구성할 구성 요소입니다.

`com.example.websockets` 패키지에 `WebSocketConfig`라는 새 Java 클래스를 만듭니다.

`WebSocketConfig` 클래스에 다음 코드를 추가합니다.

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {

    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {
        registry.enableSimpleBroker("/topic");
        registry.setApplicationDestinationPrefixes("/app");
    }

    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        registry.addEndpoint("/websocket").withSockJS();
    }
}
```

`WebSocketConfig` 클래스에서 어떤 일이 일어나는지 살펴보겠습니다.

먼저 `@Configuration` 및 `@EnableWebSocketMessageBroker`로 클래스에 주석을 답니다. `@Configuration` 주석은 이것이 구성 클래스임을 Spring에 알려줍니다. `@EnableWebSocketMessageBroker` 주석은 WebSocket 메시지 브로커를 활성화합니다.

다음으로 `WebSocketMessageBrokerConfigurer` 인터페이스를 구현합니다. 이 인터페이스는 WebSocket 메시지 브로커를 구성하는 방법을 제공합니다.

`configureMessageBroker` 메서드를 재정의합니다. 이 방법은 메시지 브로커를 구성하는 데 사용됩니다.

`configureMessageBroker` 메서드에서 단순 브로커를 활성화하고 애플리케이션 대상 접두사를 설정합니다.

단순 브로커는 게시/구독 메시징을 지원하는 메시지 브로커입니다. 사용이 매우 간단하며 이 예에서 사용할 것입니다.

애플리케이션 대상 접두사는 클라이언트에서 전송되는 모든 메시지의 대상 접두사로 사용됩니다.

마지막으로 `registerStompEndpoints` 메서드를 재정의합니다. 이 방법은 STOMP 끝점을 등록하는 데 사용됩니다. STOMP는 간단한 텍스트 지향 메시징 프로토콜입니다.

`registerStompEndpoints` 메서드에서 `/websocket` URL에 매핑되는 엔드포인트를 추가합니다. 또한 SockJS를 사용하도록 끝점을 구성합니다.

SockJS는 WebSocket을 통해 STOMP를 사용하는 편리한 방법을 제공하는 클라이언트 측 JavaScript 라이브러리입니다.

### 웹 컨트롤러 구현

다음으로 웹 컨트롤러를 구현해야 합니다. 이것은 웹 요청을 처리할 구성 요소입니다.

`com.example.websockets` 패키지에 `WebController`라는 새 Java 클래스를 만듭니다.

`WebController` 클래스에 다음 코드를 추가합니다.

```java
@Controller
public class WebController {

    @GetMapping("/")
    public String index() {
        return "index";
    }
}
```

`WebController` 클래스에서 어떤 일이 일어나는지 살펴보겠습니다.

먼저 `@Controller`로 클래스에 주석을 답니다. 이는 이것이 웹 컨트롤러임을 Spring에 알려줍니다.

다음으로 `index`라는 `@GetMapping` 주석 메서드가 있습니다. 이 메서드는 `/` URL에 GET 요청이 있을 때 호출됩니다.

`index` 메서드 내에서 `index` 템플릿을 반환합니다. `index` 템플릿은 `resources/templates` 디렉터리에 있습니다.

### 색인 템플릿 구현

다음으로 `인덱스` 템플릿을 구현해야 합니다.

`resources/templates/index.html` 파일을 열고 다음 코드를 추가합니다.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>WebSocket Chat</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/sockjs-client/1.1.2/sockjs.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/stomp.js/2.3.3/stomp.min.js"></script>
</head>
<body>

<h1>WebSocket Chat</h1>

<form id="message-form">
    <label for="message-input">Message:</label>
    <input type="text" id="message-input" placeholder="Enter a message">
    <button type="submit">Send</button>
</form>

<ul id="messages">
    <!-- Messages will be inserted here -->
</ul>

<script>
    var stompClient = null;

    function connect() {
        var socket = new SockJS('/websocket');
        stompClient = Stomp.over(socket);

        stompClient.connect({}, function (frame) {
            console.log('Connected: ' + frame);
            stompClient.subscribe('/topic/messages', function (message) {
                showMessage(JSON.parse(message.body).message);
            });
        });
    }

    function disconnect() {
        if (stompClient !== null) {
            stompClient.disconnect();
        }
        console.log("Disconnected");
    }

    function sendMessage() {
        var message = document.getElementById('message-input').value;
        stompClient.send("/app/send/message", {}, JSON.stringify({'message': message}));
    }

    function showMessage(message) {
        var messages = document.getElementById('messages');
        var li = document.createElement('li');
        li.appendChild(document.createTextNode(message));
        messages.appendChild(li);
    }

    connect();
</script>

</body>
</html>
```

`인덱스` 템플릿에서 어떤 일이 벌어지고 있는지 살펴보겠습니다.

먼저 `sockjs` 및 `stomp` JavaScript 라이브러리를 포함합니다. 이러한 라이브러리는 클라이언트에서 WebSocket 서버에 연결하는 데 사용됩니다.

다음으로 `message-form`의 `id`가 있는 `<form>` 요소가 있습니다. 이 `<form>` 요소는 서버에 메시지를 제출하는 데 사용됩니다.

`<form>` 요소 안에는 `<label>` 요소와 `<input>` 요소가 있습니다. `<input>` 요소는 서버로 보낼 메시지를 입력하는 데 사용됩니다.

마지막으로 `messages`의 `id`가 있는 `<ul>` 요소가 있습니다. 이 `<ul>` 요소는 서버에서 받은 메시지를 표시하는 데 사용됩니다.

`<ul>` 요소 아래에는 JavaScript `<script>` 요소가 있습니다. 이 `<script>` 요소에는 WebSocket 서버에 연결하고 메시지를 보내고 받는 코드가 포함되어 있습니다.

먼저 `stompClient` 변수를 생성합니다. 이 변수는 STOMP 클라이언트를 저장하는 데 사용됩니다.

다음으로 `connect` 함수가 있습니다. 이 함수는 WebSocket 서버에 연결하는 데 사용됩니다.

`connect` 함수 내에서 새로운 `SockJS` 인스턴스를 생성하고 `/websocket` URL을 생성자에 전달합니다. 이 URL은 `WebSocketConfig` 클래스에서 구성한 끝점입니다.

그런 다음 새 `stompClient` 인스턴스를 만들고 `SockJS` 인스턴스를 생성자에 전달합니다.

다음으로 `stompClient` 인스턴스에서 `connect` 메서드를 호출합니다. 이 메서드는 두 개의 인수를 사용합니다. 첫 번째 인수는 빈 객체이고 두 번째 인수는 콜백 함수입니다.

콜백 함수는 연결이 설정되면 호출됩니다.

콜백 함수 내에서 `/topic/messages` 주제를 구독합니다. 이것은 `MessageHandler` 클래스가 메시지를 게시하는 주제입니다.

이 주제에 대한 메시지가 수신되면 메시지를 인수로 사용하여 콜백 함수가 호출됩니다.

콜백 함수에서 `showMessage` 함수를 호출하고 메시지를 함수에 전달합니다.

`showMessage` 함수는 메시지를 인수로 사용하고 메시지를 `messages` `<ul>`에 추가합니다.

마지막으로 `disconnect` 기능이 있습니다. 이 기능은 WebSocket 서버에서 연결을 끊는 데 사용됩니다.

`disconnect` 함수 내에서 `stompClient` 변수가 `null`이 아닌지 확인합니다. `null`이 아니면 `stompClient` 인스턴스에서 `disconnect` 메서드를 호출합니다.

`sendMessage` 함수도 있습니다. 이 기능은 서버에 메시지를 보내는 데 사용됩니다.

`sendMessage` 함수 내에서 `message-input` `<input>` 요소에서 메시지를 가져와 `message`라는 변수에 저장합니다.

그런 다음 `stompClient` 인스턴스에서 `send` 메서드를 호출하고 대상, 헤더 및 본문을 메서드에 전달합니다.

대상은 메시지를 보내려는 끝점입니다. 이 경우 `/app/send/message` 엔드포인트로 메시지를 보내려고 합니다. 이것은 `MessageHandler` 클래스에서 구성한 끝점입니다.

헤더와 본문은 선택 사항입니다. 이 예제에서는 헤더를 설정할 필요가 없으므로 빈 개체만 전달합니다.

본문은 서버로 보내려는 메시지입니다. 우리는 `JSON.stringify` 함수를 사용하여 메시지를 JSON 문자열로 변환합니다.

마지막으로 `showMessage` 함수가 있습니다. 이 기능은 `messages` `<ul>`에 메시지를 표시하는 데 사용됩니다.

`showMessage` 함수 내에서 `messages` `<ul>`를 가져와 `messages`라는 변수에 저장합니다.

그런 다음 새 `<li>` 요소를 만들고 `li`라는 변수에 저장합니다.

그런 다음 메시지를 텍스트로 사용하여 새 `TextNode`를 만들고 `<li>` 요소에 추가합니다.

마지막으로 `<li>` 요소를 `messages` `<ul>`에 추가합니다.

`index` 템플릿의 끝에서 `connect` 함수를 호출합니다. 그러면 클라이언트가 WebSocket 서버에 연결됩니다.

### 애플리케이션 테스트

이제 애플리케이션을 구현했으므로 테스트해 보겠습니다.

'Application' 클래스를 실행하여 애플리케이션을 시작합니다.

애플리케이션이 시작되면 웹 브라우저를 열고 http://localhost:8080으로 이동합니다.

다음 페이지가 표시됩니다.

![WebSocket 채팅 페이지](https://i.imgur.com/uGjTtqP.png)

'메시지' 필드에 메시지를 입력하고 '보내기' 버튼을 클릭합니다.

메시지가 `Messages` 목록에 표시되어야 합니다.

![메시지가 포함된 WebSocket 채팅 페이지](https://i.imgur.com/DVnWql6.png)

## 결론

이 기사에서는 Spring Boot와 WebSocket을 사용하여 실시간 채팅 애플리케이션을 만드는 방법을 살펴보았습니다.

또한 'SimpMessagingTemplate'을 사용하여 WebSocket을 통해 클라이언트에 메시지를 보내는 방법도 살펴보았습니다.

## 참조

- [Spring Boot 참조 문서](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/)
- [웹소켓](https://en.wikipedia.org/wiki/WebSocket)
- [스프링부트와 웹소켓](https://spring.io/guides/gs/messaging-stomp-websocket/)
- [WebSocket을 사용하여 채팅 애플리케이션 구축