---
title: 백엔드 개발에서 고성능 통신을 위한 gRPC
description: 
published: true
date: 2023-02-13T10:55:57.823Z
tags: 
editor: markdown
dateCreated: 2023-02-13T10:55:50.915Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [gRPC for High-Performance Communication in Backend Development***English** document is available*](/en/Knowledge-base/Backend/grpc-for-high-performance-communication-in-backend-development)
{.links-list}


# 백엔드 개발에서 고성능 통신을 위한 gRPC

gRPC는 모든 환경에서 실행할 수 있는 최신 오픈 소스 고성능 RPC 프레임워크입니다. 전송을 위해 HTTP/2를 사용하고 인터페이스 설명 언어로 프로토콜 버퍼를 사용합니다.

gRPC는 다음과 같이 설계되었습니다.

- **Simple**: 사용하기 쉽고 확장하기 쉽게 설계되었습니다.
- **빠른**: 낮은 오버헤드, 높은 성능.
- **언어 불가지론**: 다양한 프로그래밍 언어를 지원합니다.
- **플랫폼 불가지론**: 온프레미스, 클라우드 및 하이브리드 환경을 비롯한 다양한 환경에서 실행됩니다.

이 기사에서는 백엔드 개발에서 고성능 통신을 위해 gRPC를 사용하는 방법을 살펴보겠습니다.

## gRPC를 사용하는 이유

gRPC를 사용하는 데는 여러 가지 이유가 있지만 가장 중요한 이유는 다음과 같습니다.

- **성능**: gRPC는 고성능을 위해 설계되었습니다. 다중화되고 양방향 스트리밍을 허용하는 전송에 HTTP/2를 사용합니다.
- **언어 불가지론**: gRPC는 다양한 프로그래밍 언어를 지원하므로 다국어 환경에서 쉽게 사용할 수 있습니다.
- **플랫폼 불가지론**: gRPC는 온프레미스, 클라우드 및 하이브리드 환경을 비롯한 다양한 환경에서 실행할 수 있습니다.

## gRPC는 어떻게 사용하나요?

gRPC를 사용하는 것은 간단합니다. 첫 번째 단계는 선택한 프로그래밍 언어에 대한 gRPC 라이브러리를 설치하는 것입니다. 그런 다음 프로토콜 버퍼 인터페이스 설명 언어를 사용하여 .proto 파일에서 서비스를 정의해야 합니다. 마지막으로 서비스를 구현하기 위한 코드를 작성해야 합니다.

간단한 예를 살펴보겠습니다. 우리는 이름을 받아 인사말을 반환하는 서비스를 만들 것입니다.

먼저 Node.js용 gRPC 라이브러리를 설치해야 합니다.

```
npm install grpc
```

다음으로 .proto 파일에서 서비스를 정의해야 합니다. 우리는 파일을 greet.proto라고 부를 것입니다:

```proto
syntax = "proto3";

package greet;

service Greeter {
  rpc SayHello (HelloRequest) returns (HelloReply) {}
}

message HelloRequest {
  string name = 1;
}

message HelloReply {
  string message = 1;
}
```

이 파일에서는 SayHello라는 단일 메서드를 사용하여 Greeter라는 서비스를 정의했습니다. 이 메서드는 이름이 포함된 HelloRequest를 사용하고 메시지가 포함된 HelloReply를 반환합니다.

마지막으로 서비스를 구현하기 위한 코드를 작성해야 합니다. Greetinger_server.js라는 파일을 생성합니다.

```javascript
var grpc = require('grpc');
var protoLoader = require('@grpc/proto-loader');

var packageDefinition = protoLoader.loadSync(
  __dirname + '/greet.proto',
  {
    keepCase: true,
    longs: String,
    enums: String,
    defaults: true,
    oneofs: true
  });
var greet_proto = grpc.loadPackageDefinition(packageDefinition).greet;

function sayHello(call, callback) {
  callback(null, {message: 'Hello ' + call.request.name});
}

function main() {
  var server = new grpc.Server();
  server.addService(greet_proto.Greeter.service, {sayHello: sayHello});
  server.bind('0.0.0.0:50051', grpc.ServerCredentials.createInsecure());
  server.start();
}

main();
```

이 파일에서 grpc 및 proto-loader 라이브러리를 가져왔습니다. .proto 파일을 로드하고 SayHello 메서드를 정의했습니다. 마지막으로 gRPC 서버를 만들고 포트 50051에서 시작했습니다.

## 결론

이 기사에서는 백엔드 개발에서 고성능 통신을 위해 gRPC를 사용하는 방법을 살펴보았습니다. gRPC 라이브러리를 설치하는 방법, .proto 파일에서 서비스를 정의하는 방법 및 서비스를 구현하기 위한 코드를 작성하는 방법을 살펴보았습니다.