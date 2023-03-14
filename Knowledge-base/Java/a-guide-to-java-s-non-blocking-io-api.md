---
title: Java의 비차단 I/O API 가이드
description: 
published: true
date: 2023-03-14T07:33:57.804Z
tags: 
editor: markdown
dateCreated: 2023-03-14T07:33:57.804Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [A Guide to Java's Non-Blocking I/O API***English** document is available*](/en/Knowledge-base/Java/a-guide-to-java-s-non-blocking-io-api)
{.links-list}



## 소개

Java에서 입/출력(I/O) 작업은 응용 프로그램과 외부 세계 간의 상호 작용 관리를 담당하므로 모든 응용 프로그램에 중요합니다. Java는 다른 작업의 실행을 차단하지 않고 I/O 작업을 수행할 수 있는 비차단 I/O API를 제공합니다. 이 API는 많은 수의 동시 사용자를 처리할 수 있는 확장 가능한 고성능 애플리케이션을 구축하기 위한 강력한 도구입니다.

## 논블로킹 I/O란?

Java의 Non-Blocking I/O API를 논의하기 전에 Non-Blocking I/O가 무엇을 의미하는지 먼저 이해해 봅시다. 기존 차단 I/O 모델에서 응용 프로그램은 I/O 작업이 완료될 때까지 차단됩니다. 이는 응용 프로그램이 다음 작업을 진행하기 전에 I/O 작업이 완료될 때까지 기다린다는 의미입니다. 이는 많은 수의 동시 사용자를 처리해야 하는 애플리케이션에서 문제가 될 수 있습니다. 그래서 이러한 문제를 극복하기 위해 non-blocking I/O가 도입되었다.

Non-Blocking I/O에서 응용 프로그램은 I/O 작업이 수행되는 동안 다른 작업을 계속 실행할 수 있습니다. 이는 단일 스레드를 사용하여 여러 I/O 작업을 처리함으로써 달성됩니다. I/O 작업이 시작되면 스레드에 알리고 스레드는 I/O 작업이 완료될 때까지 기다리지 않고 다른 작업을 계속 실행합니다. I/O 작업이 완료되면 스레드에 알림이 전송되고 데이터를 처리할 수 있습니다.

## 자바의 논블로킹 I/O API

Java의 Non-Blocking I/O API는 Java 1.4에서 도입되었습니다. I/O 작업을 처리하기 위한 이벤트 기반 접근 방식을 제공하는 리액터 패턴을 기반으로 합니다. API는 파일 또는 네트워크 소켓과 같은 I/O 장치에 대한 연결을 나타내는 채널 개념을 중심으로 구축됩니다. API는 채널 작업을 위한 두 가지 주요 클래스인 `SelectableChannel` 및 `SelectionKey`를 제공합니다.

### 선택 가능한 채널

`SelectableChannel` 클래스는 I/O 작업을 위해 선택할 수 있는 채널을 나타내는 추상 클래스입니다. Selector 개체에 채널을 등록하고 I/O 작업에 대한 채널의 준비 상태를 테스트하는 방법을 제공합니다. `SelectableChannel` 클래스에는 `SocketChannel` 및 `ServerSocketChannel`의 두 가지 구체적인 하위 클래스가 있습니다.

#### 소켓채널

`SocketChannel` 클래스는 네트워크 소켓에서 I/O 작업을 수행하기 위한 채널을 나타냅니다. 데이터 읽기와 쓰기 모두에 사용할 수 있습니다. `SocketChannel` 클래스를 사용하려면 먼저 `SocketChannel` 클래스의 `open()` 메서드를 사용하여 인스턴스를 생성해야 합니다.

```java
SocketChannel socketChannel = SocketChannel.open();
```

`SocketChannel` 인스턴스를 생성했으면 `connect()` 메서드를 사용하여 원격 서버에 연결할 수 있습니다.

```java
socketChannel.connect(new InetSocketAddress("localhost", 8080));
```

원격 서버에 데이터를 쓰려면 `write()` 메서드를 사용할 수 있습니다.

```java
ByteBuffer buffer = ByteBuffer.wrap("Hello World".getBytes());
socketChannel.write(buffer);
```

원격 서버에서 데이터를 읽으려면 `read()` 메서드를 사용할 수 있습니다.

```java
ByteBuffer buffer = ByteBuffer.allocate(1024);
socketChannel.read(buffer);
```

#### 서버 소켓 채널

`ServerSocketChannel` 클래스는 클라이언트로부터 들어오는 연결을 수락하기 위한 채널을 나타냅니다. 클라이언트에서 들어오는 연결을 수신 대기하는 서버를 만드는 데 사용할 수 있습니다. `ServerSocketChannel` 클래스를 사용하려면 먼저 `ServerSocketChannel` 클래스의 `open()` 메서드를 사용하여 인스턴스를 생성해야 합니다.

```java
ServerSocketChannel serverSocketChannel = ServerSocketChannel.open();
```

`ServerSocketChannel` 인스턴스를 생성했으면 `bind()` 메서드를 사용하여 포트에 바인딩할 수 있습니다.

```java
serverSocketChannel.bind(new InetSocketAddress(8080));
```

클라이언트로부터 들어오는 연결을 수락하려면 `accept()` 메서드를 사용할 수 있습니다.

```java
SocketChannel socketChannel = serverSocketChannel.accept();
```

### 선택키

`SelectionKey` 클래스는 Selector 개체로 채널 등록을 나타내는 데 사용됩니다. 여기에는 I/O 작업에 대한 채널의 준비 상태와 채널의 현재 상태에 대한 정보가 포함됩니다. 'SelectionKey' 클래스는 채널의 준비 상태를 테스트하고 키와 연결된 채널을 검색하기 위한 메서드를 제공합니다.

### 선택자

`Selector` 클래스는 I/O 작업 준비가 된 채널을 선택하는 데 사용됩니다. 단일 스레드로 여러 채널의 준비 상태를 모니터링하는 방법을 제공합니다. `Selector` 클래스는 비차단 I/O 모델을 사용하여 I/O 작업이 수행되는 동안 다른 작업의 실행을 차단하지 않도록 합니다.

`Selector` 클래스를 사용하려면 먼저 `open()` 메서드를 사용하여 인스턴스를 만들어야 합니다.

```java
Selector selector = Selector.open();
```

`Selector` 인스턴스를 생성했으면 `SelectableChannel` 클래스의 `register()` 메서드를 사용하여 채널을 등록할 수 있습니다.

```java
SocketChannel socketChannel = SocketChannel.open();
socketChannel.configureBlocking(false);
SelectionKey key = socketChannel.register(selector, SelectionKey.OP_READ);
```

`register()` 메서드는 `Selector` 개체와 관심 집합의 두 가지 인수를 사용합니다. 관심 집합은 애플리케이션이 채널에 대해 관심을 갖는 I/O 작업 유형을 지정합니다.

`Selector` 개체에 채널을 등록하면 `select()` 메서드를 사용하여 I/O 작업 준비가 된 채널을 기다릴 수 있습니다.

```java
int readyChannels = selector.select();
```

`select()` 메서드는 적어도 하나의 채널이 I/O 작업을 위해 준비되거나 시간 초과가 발생할 때까지 차단됩니다. 메서드가 반환되면 `selectedKeys()` 메서드를 사용하여 I/O 작업이 준비된 키 세트를 검색할 수 있습니다.

```java
Set<SelectionKey> selectedKeys = selector.selectedKeys();
```

그런 다음 키 집합을 반복하여 채널에서 I/O 작업을 수행할 수 있습니다.

```java
Iterator<SelectionKey> keyIterator = selectedKeys.iterator();
while (keyIterator.hasNext()) {
    SelectionKey key = keyIterator.next();
    if (key.isReadable()) {
        // Perform read operation
    } else if (key.isWritable()) {
        // Perform write operation
    }
    keyIterator.remove();
}
```

## 결론

Java의 Non-Blocking I/O API는 많은 수의 동시 사용자를 처리할 수 있는 확장 가능한 고성능 애플리케이션을 구축하기 위한 강력한 도구입니다. I/O 작업을 처리하기 위한 이벤트 기반 접근 방식을 제공하므로 I/O 작업이 수행되는 동안 애플리케이션이 다른 작업을 계속 실행할 수 있습니다. Java의 Non-Blocking I/O API를 사용하여 개발자는 기존의 차단 I/O 애플리케이션보다 더 효율적이고 응답성이 뛰어난 애플리케이션을 구축할 수 있습니다.

## 외부 리소스

- [Java Non-Blocking IO](https://www.baeldung.com/java-nio-non-blocking-io)
- [Java NIO 튜토리얼](https://www.javatpoint.com/java-nio-tutorial)
- [자바 NIO 선택기](https://www.tutorialspoint.com/java_nio/java_nio_selector.htm)
- [자바 NIO 채널](https://www.javatpoint.com/java-nio-channels)