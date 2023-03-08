---
title: gRPC로 백엔드 시스템 구축
description: 
published: true
date: 2023-02-17T18:00:52.570Z
tags: 
editor: markdown
dateCreated: 2023-01-29T20:52:09.320Z
---

- [Building Backend Systems with gRPC***English** version of this document is available*](/en/Knowledge-base/Backend/building-backend-systems-with-grpc)
{.links-list}


# gRPC로 백엔드 시스템 구축

이 기사에서는 gRPC를 사용하여 백엔드 시스템을 구축하는 방법을 살펴보겠습니다. gRPC는 클라이언트와 서버 애플리케이션이 투명하게 통신할 수 있게 해주는 언어 중립적이고 플랫폼 중립적인 RPC 프레임워크입니다. HTTP/2 프로토콜을 기반으로 하며 프로토콜 버퍼를 인터페이스 설명 언어로 사용합니다.

gRPC는 백엔드 서비스 구축에 탁월한 선택입니다. 효율적이고 사용하기 쉽습니다. 이 기사에서는 gRPC를 사용하여 간단한 백엔드 서비스를 빌드하는 방법을 살펴봅니다. 먼저 gRPC의 기본 사항을 살펴본 다음 간단한 서비스를 구현합니다.

## gRPC란?

gRPC는 클라이언트와 서버 애플리케이션이 투명하게 통신할 수 있게 해주는 언어 중립적이고 플랫폼 중립적인 RPC 프레임워크입니다. HTTP/2 프로토콜을 기반으로 하며 프로토콜 버퍼를 인터페이스 설명 언어로 사용합니다.

gRPC는 백엔드 서비스 구축에 탁월한 선택입니다. 효율적이고 사용하기 쉽습니다. 이 기사에서는 gRPC를 사용하여 간단한 백엔드 서비스를 빌드하는 방법을 살펴봅니다.

## gRPC를 사용하는 이유는 무엇입니까?

gRPC는 여러 가지 이유로 백엔드 서비스를 구축하는 데 탁월한 선택입니다.

- 효율적입니다. gRPC는 HTTP/1.1보다 효율적인 이진 프로토콜인 HTTP/2를 사용합니다.
- 사용하기 쉽습니다. gRPC는 프로토콜 버퍼를 인터페이스 설명 언어로 사용합니다. 프로토콜 버퍼는 효율적이고 사용하기 쉬운 형식으로 데이터를 인코딩하는 방법입니다.
- 언어 중립적입니다. gRPC는 언어 중립적인 HTTP/2 프로토콜을 기반으로 합니다. 즉, gRPC는 모든 프로그래밍 언어와 함께 사용할 수 있습니다.

## gRPC는 어떻게 작동하나요?

gRPC는 .proto 파일에서 서비스를 정의하여 작동합니다. .proto 파일은 호출할 수 있는 메서드, 전달할 수 있는 매개 변수 및 반환 유형을 정의합니다.

그런 다음 .proto 파일을 사용하여 선택한 언어로 코드를 생성합니다. 생성된 코드에는 호출할 수 있는 메서드, 전달할 수 있는 매개 변수 및 반환 유형이 포함됩니다.

## gRPC는 어떻게 사용하나요?

gRPC를 사용하려면 선택한 언어에 대한 gRPC 라이브러리를 설치해야 합니다. 여기에서 gRPC 라이브러리에 대한 설치 지침을 찾을 수 있습니다.

https://grpc.io/docs/languages/

gRPC 라이브러리를 설치하면 생성된 코드를 사용하여 .proto 파일에 정의된 메서드를 호출할 수 있습니다.

## 예

간단한 예를 살펴보겠습니다. .proto 파일에서 서비스를 정의하는 것으로 시작하겠습니다.

```
syntax = "proto3";

service Greeter {
  rpc SayHello (HelloRequest) returns (HelloResponse);
}

message HelloRequest {
  string name = 1;
}

message HelloResponse {
  string message = 1;
}
```

이 .proto 파일은 SayHello라는 단일 메서드로 서비스를 정의합니다. SayHello 메서드는 HelloRequest를 받아 HelloResponse를 반환합니다.

HelloRequest에는 문자열인 이름이라는 단일 필드가 포함되어 있습니다. HelloResponse에는 문자열이기도 한 메시지라는 단일 필드가 포함되어 있습니다.

이제 서비스를 정의했으므로 선택한 언어로 코드를 생성할 수 있습니다. protoc 도구를 사용하여 코드를 생성합니다. protoc 도구는 여기에서 사용할 수 있습니다.

https://github.com/google/protobuf/releases

protoc 도구를 다운로드하여 설치하면 이를 사용하여 코드를 생성할 수 있습니다. 다음 명령은 Go 프로그래밍 언어로 Greeter 서비스용 코드를 생성합니다.

```
protoc -I . greeter.proto --go_out=plugins=grpc:.
```

이 명령은 Greetinger.pb.go라는 파일을 생성합니다. 이 파일에는 Greeter 서비스에 대해 생성된 코드가 포함되어 있습니다.

생성된 코드에는 호출할 수 있는 메서드, 전달할 수 있는 매개 변수 및 반환 유형이 포함됩니다. 이 예에서 생성된 코드에는 SayHello 메서드가 포함되어 있습니다. 이 메서드는 HelloRequest를 받아 HelloResponse를 반환합니다.

생성된 코드를 사용하여 SayHello 메서드를 호출할 수 있습니다. 다음 코드는 Go 프로그래밍 언어에서 SayHello 메서드를 호출하는 방법을 보여줍니다.

```go
func main() {
  conn, err := grpc.Dial("localhost:50051", grpc.WithInsecure())
  if err != nil {
    log.Fatalf("did not connect: %v", err)
  }
  defer conn.Close()
  c := pb.NewGreeterClient(conn)
  r, err := c.SayHello(context.Background(), &pb.HelloRequest{Name: "World"})
  if err != nil {
    log.Fatalf("could not greet: %v", err)
  }
  log.Printf("Greeting: %s", r.Message)
}
```

이 코드는 서버에 대한 연결을 만든 다음 SayHello 메서드를 호출합니다. SayHello 메서드는 HelloRequest를 받아 HelloResponse를 반환합니다. HelloRequest에는 이름 필드가 포함되어 있습니다. HelloResponse에는 메시지 필드가 포함되어 있습니다.

이 코드는 HelloResponse의 메시지 필드를 인쇄합니다. 이 예에서 메시지 필드에는 "Hello World"라는 문자열이 포함되어 있습니다.

## 결론

이 문서에서는 gRPC를 사용하여 백엔드 서비스를 빌드하는 방법을 살펴보았습니다. gRPC는 백엔드 서비스 구축에 탁월한 선택입니다. 효율적이고 사용하기 쉽습니다. 이 기사에서는 gRPC를 사용하여 간단한 백엔드 서비스를 빌드하는 방법을 살펴보았습니다.