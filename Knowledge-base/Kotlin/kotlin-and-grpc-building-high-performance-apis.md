---
title: Kotlin 및 gRPC: 고성능 API 구축
description: 
published: true
date: 2023-02-18T10:06:32.053Z
tags: 
editor: markdown
dateCreated: 2023-02-18T10:06:30.643Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and gRPC: Building High-Performance APIs***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-grpc-building-high-performance-apis)
{.links-list}


# Kotlin 및 gRPC: 고성능 API 구축

[Kotlin](https://kotlinlang.org/)은 JVM에서 실행되고 고성능 애플리케이션을 만드는 데 사용할 수 있는 정적 유형 프로그래밍 언어입니다. [gRPC](https://grpc.io/)는 모든 환경에서 실행할 수 있는 고성능 오픈 소스 RPC 프레임워크입니다. 이 기사에서는 Kotlin 및 gRPC를 사용하여 고성능 API를 빌드하는 방법을 살펴보겠습니다.

## 왜 코틀린인가?

Kotlin은 사용하기 쉽고 안전하며 간결하도록 설계된 최신 언어입니다. Kotlin은 Java와 완벽하게 상호 운용되므로 JVM에서 실행되는 애플리케이션을 빌드하는 데 사용할 수 있습니다. Kotlin은 [JavaScript](https://kotlinlang.org/docs/tutorials/javascript/getting-started-gradle/getting-started-with-gradle.html) 및 [Native](https ://kotlinlang.org/docs/reference/native-overview.html).

Kotlin의 주요 이점 중 하나는 Java보다 훨씬 덜 장황하다는 것입니다. 이렇게 하면 Kotlin 코드를 더 쉽게 읽고 이해할 수 있습니다. Kotlin에는 Java보다 안전한 기능도 있습니다. 예를 들어 Kotlin에는 null 포인터 예외를 방지하는 null 안전성이 있습니다.

Kotlin은 고성능 애플리케이션을 구축하는 데 탁월한 선택입니다. Kotlin 코드는 Java 코드만큼 빠르게 실행될 수 있으며 작고 효율적인 실행 파일을 만드는 데 사용할 수 있습니다.

## 왜 gRPC인가?

gRPC는 모든 환경에서 실행할 수 있는 고성능 오픈 소스 RPC 프레임워크입니다. gRPC는 [프로토콜 버퍼](https://developers.google.com/protocol-buffers)(또는 protobufs)를 사용하여 메시지 유형과 서비스 인터페이스를 정의합니다. gRPC 서비스는 모든 언어로 작성할 수 있지만 protobuf는 제한된 수의 언어에서만 지원됩니다.

gRPC는 짧은 대기 시간과 높은 처리량을 위해 설계된 [HTTP/2](https://en.wikipedia.org/wiki/HTTP/2) 프로토콜을 기반으로 합니다. gRPC 서비스는 단일 연결을 통해 다중화될 수 있으며 gRPC 메시지는 압축될 수 있습니다.

gRPC는 고성능 API를 구축하기 위한 탁월한 선택입니다. gRPC 서비스는 모든 언어로 작성할 수 있으며 gRPC 메시지는 단일 연결을 통해 다중화될 수 있습니다. gRPC는 또한 [스트리밍](https://grpc.io/docs/guides/concepts.html# streaming) 및 [양방향 스트리밍](https://grpc.io/docs/guides/concepts. html#양방향 스트리밍).

## Kotlin과 gRPC: 완벽한 조화

Kotlin과 gRPC는 고성능 API를 구축하기 위한 완벽한 조합입니다. Kotlin은 사용하기 쉽고 안전하며 간결하도록 설계된 최신 언어입니다. gRPC는 모든 환경에서 실행할 수 있는 고성능 오픈 소스 RPC 프레임워크입니다. 이 섹션에서는 Kotlin 및 gRPC를 사용하여 고성능 API를 빌드하는 방법을 살펴보겠습니다.

### gRPC 서비스 정의

gRPC 서비스는 [.proto 파일](https://developers.google.com/protocol-buffers/docs/proto3)을 사용하여 정의됩니다. .proto 파일은 메시지 유형 및 서비스 인터페이스를 정의합니다.

예를 들어 다음 .proto 파일은 `UserRequest` 메시지를 받아서 `UserResponse` 메시지를 반환하는 단일 메서드 `GetUser`가 있는 간단한 gRPC 서비스를 정의합니다.

```protobuf
syntax = "proto3";

package com.example.user;

service UserService {
  rpc GetUser (UserRequest) returns (UserResponse);
}

message UserRequest {
  int32 id = 1;
}

message UserResponse {
  int32 id = 1;
  string name = 2;
  string email = 3;
}
```

.proto 파일은 Kotlin 코드를 생성하도록 컴파일됩니다. 생성된 코드에는 메시지 유형과 서비스 인터페이스가 포함됩니다.

### gRPC 서비스 구현

gRPC 서비스는 [서버](https://grpc.io/docs/languages/kotlin/basics/server/) 및 [클라이언트](https://grpc.io/docs/languages/kotlin/)를 사용하여 구현됩니다. 기본/클라이언트/). 서버는 서비스 인터페이스를 구현하고 클라이언트는 서비스 인터페이스를 사용합니다.

예를 들어, 다음 코드는 `UserService`의 `GetUser` 메서드를 구현합니다.

```kotlin
class UserService : UserServiceGrpc.UserServiceImplBase() {
  override fun getUser(request: UserRequest, responseObserver: StreamObserver<UserResponse>) {
    // TODO: implement getUser
  }
}
```

`getUser` 메서드는 `UserRequest` 메시지와 `UserResponse` 메시지의 `StreamObserver`를 사용합니다. `getUser` 메서드는 `UserRequest` 메시지를 사용하여 데이터베이스 또는 다른 API에서 데이터를 가져올 수 있습니다. `getUser` 메소드는 `StreamObserver`를 사용하여 `UserResponse` 메시지를 다시 클라이언트로 스트리밍할 수 있습니다.

### gRPC 서비스 호출

[클라이언트](https://grpc.io/docs/languages/kotlin/basics/client/)를 사용하여 gRPC 서비스를 호출합니다. 클라이언트는 서버에 대한 `Channel`을 생성하고 클라이언트는 `Channel`을 사용하여 서비스 메서드를 호출합니다.

예를 들어 다음 코드는 `UserService`의 `GetUser` 메서드를 호출합니다.

```kotlin
val channel = ManagedChannelBuilder.forAddress("localhost", 8080)
    .usePlaintext()
    .build()
val userService = UserServiceGrpc.newStub(channel)
val request = UserRequest.newBuilder()
    .setId(1)
    .build()
val responseObserver = object : StreamObserver<UserResponse> {
  override fun onNext(value: UserResponse) {
    // TODO: handle UserResponse
  }

  override fun onError(t: Throwable) {
    // TODO: handle error
  }

  override fun onCompleted() {
    // TODO: handle completion
  }
}
userService.getUser(request, responseObserver)
```

이 코드는 `localhost:8080`에서 서버에 대한 `Channel`을 생성합니다. 그런 다음 코드는 `Channel`을 사용하여 `UserService`를 생성합니다. 이 코드는 `id`가 `1`인 `UserRequest`를 생성합니다. 그런 다음 코드는 `UserResponse` 메시지의 `StreamObserver`를 생성합니다. 이 코드는 `request` 및 `responseObserver`를 사용하여 `UserService`의 `GetUser` 메서드를 호출합니다. `GetUser` 메서드는 `id`가 `1`인 사용자의 데이터를 가져오고 `UserResponse` 메시지를 다시 `responseObserver`로 스트리밍합니다.

## 결론

Kotlin과 gRPC는 고성능 API를 구축하는 데 탁월한 선택입니다. Kotlin은 사용하기 쉽고 안전하며 간결하도록 설계된 최신 언어입니다. gRPC는 모든 환경에서 실행할 수 있는 고성능 오픈 소스 RPC 프레임워크입니다. 이 기사에서는 Kotlin과 gRPC를 사용하여 고성능 API를 빌드하는 방법을 살펴보았습니다.