---
title: 백엔드에서 gRPC 구현
description: 
published: true
date: 2023-02-01T23:43:42.558Z
tags: 
editor: markdown
dateCreated: 2023-02-01T23:43:40.989Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Implementing gRPC in Your Backend***English** document is available*](/en/Knowledge-base/Backend/implementing-grpc-in-your-backend)
{.links-list}


# 백엔드에서 gRPC 구현

## 소개

gRPC는 모든 환경에서 실행할 수 있는 최신 오픈 소스 RPC 프레임워크입니다. 전송에는 HTTP/2를 사용하고 메시지 직렬화에는 프로토콜 버퍼를 사용합니다. gRPC는 C# , Go, Java, Node.js, PHP, Python, Ruby를 비롯한 다양한 언어로 제공됩니다.

이 기사에서는 백엔드에서 gRPC를 사용하는 방법을 보여줍니다. 다음 주제를 다룰 것입니다.

- gRPC 서버 설정
- gRPC 서비스 정의
- gRPC 서비스 구현
- gRPC 서비스 호출

## gRPC 서버 설정

가장 먼저 해야 할 일은 gRPC 서버를 설치하는 것입니다. 다음 명령을 사용하여 이 작업을 수행할 수 있습니다.

```
$ go get -u github.com/grpc/grpc-go/cmd/grpc_server
```

서버가 설치되면 시작해야 합니다. 다음 명령을 사용하여 이 작업을 수행할 수 있습니다.

```
$ grpc_server
```

서버는 기본적으로 포트 8080에서 시작하고 수신 대기합니다.

## gRPC 서비스 정의

다음으로 gRPC 서비스를 정의해야 합니다. gRPC 서비스는 .proto 파일을 사용하여 정의됩니다. 파일에는 다음이 포함되어 있습니다.

- 메시지 정의
- 서비스 정의

### 메시지 정의

메시지 정의는 클라이언트와 서버 간에 교환될 데이터를 정의하는 데 사용됩니다. 다음은 메시지 정의의 예입니다.

```proto
message Request {
  string text = 1;
}

message Response {
  string text = 1;
}
```

### 서비스 정의

서비스 정의는 클라이언트가 호출할 수 있는 RPC 메서드를 정의하는 데 사용됩니다. 다음은 서비스 정의의 예입니다.

```proto
service Service {
  rpc Process(Request) returns (Response);
}
```

## gRPC 서비스 구현

gRPC 서비스를 정의했으면 이를 구현해야 합니다. 다음은 Go에서의 예시 구현입니다.

```go
package main

import (
    "context"
    "log"
    "net"

    "google.golang.org/grpc"
    "google.golang.org/grpc/codes"
    "google.golang.org/grpc/status"

    pb "github.com/grpc/grpc-go/examples/helloworld/helloworld"
)

const (
    port = ":50051"
)

// server is used to implement helloworld.GreeterServer.
type server struct{}

// SayHello implements helloworld.GreeterServer
func (s *server) SayHello(ctx context.Context, in *pb.HelloRequest) (*pb.HelloReply, error) {
    log.Printf("Received: %v", in.GetName())
    return &pb.HelloReply{Message: "Hello " + in.GetName()}, nil
}

func main() {
    lis, err := net.Listen("tcp", port)
    if err != nil {
        log.Fatalf("failed to listen: %v", err)
    }
    s := grpc.NewServer()
    pb.RegisterGreeterServer(s, &server{})
    if err := s.Serve(lis); err != nil {
        log.Fatalf("failed to serve: %v", err)
    }
}
```

## gRPC 서비스 호출

gRPC 서비스를 구현한 후에는 클라이언트에서 호출할 수 있습니다. 다음은 Go의 예제 클라이언트입니다.

```go
package main

import (
    "context"
    "log"
    "time"

    "google.golang.org/grpc"
    pb "github.com/grpc/grpc-go/examples/helloworld/helloworld"
)

const (
    address     = "localhost:50051"
    defaultName = "world"
)

func main() {
    // Set up a connection to the server.
    conn, err := grpc.Dial(address, grpc.WithInsecure())
    if err != nil {
        log.Fatalf("did not connect: %v", err)
    }
    defer conn.Close()
    c := pb.NewGreeterClient(conn)

    // Contact the server and print out its response.
    name := defaultName
    if len(os.Args) > 1 {
        name = os.Args[1]
    }
    ctx, cancel := context.WithTimeout(context.Background(), time.Second)
    defer cancel()
    r, err := c.SayHello(ctx, &pb.HelloRequest{Name: name})
    if err != nil {
        log.Fatalf("could not greet: %v", err)
    }
    log.Printf("Greeting: %s", r.GetMessage())
}
```

## 결론

이 기사에서는 백엔드에서 gRPC를 사용하는 방법을 보여주었습니다. 우리는 다음 주제를 다루었습니다.

- gRPC 서버 설정
- gRPC 서비스 정의
- gRPC 서비스 구현
- gRPC 서비스 호출

gRPC에 대해 자세히 알아보려면 다음 리소스를 권장합니다.

- 공식 gRPC 문서: https://grpc.io/docs/
- Go에서 gRPC를 사용하는 방법에 대한 자습서: https://tutorialedge.net/golang/grpc-go-tutorial/