---
title: 在后端实施 gRPC
description: 
published: true
date: 2023-02-01T23:43:42.634Z
tags: 
editor: markdown
dateCreated: 2023-02-01T23:43:40.990Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Implementing gRPC in Your Backend***English** document is available*](/en/Knowledge-base/Backend/implementing-grpc-in-your-backend)
{.links-list}


# 在你的后端实现 gRPC

## 介绍

gRPC 是一个可以在任何环境中运行的现代开源 RPC 框架。它使用 HTTP/2 进行传输，使用 Protocol Buffers 进行消息序列化。 gRPC 支持多种语言，包括 C# 、Go、Java、Node.js、PHP、Python 和 Ruby。

在本文中，我们将展示如何在后端使用 gRPC。我们将涵盖以下主题：

- 设置 gRPC 服务器
- 定义一个 gRPC 服务
- 实现 gRPC 服务
- 调用 gRPC 服务

## 设置 gRPC 服务器

您需要做的第一件事是安装 gRPC 服务器。您可以使用以下命令执行此操作：

```
$ go get -u github.com/grpc/grpc-go/cmd/grpc_server
```

安装服务器后，您需要启动它。您可以使用以下命令执行此操作：

```
$ grpc_server
```

服务器将默认启动并侦听端口 8080。

## 定义 gRPC 服务

接下来，您需要定义一个 gRPC 服务。 gRPC 服务是使用 .proto 文件定义的。该文件包含以下内容：

- 消息定义
- 服务定义

### 消息定义

消息定义用于定义将在客户端和服务器之间交换的数据。以下是示例消息定义：

```proto
message Request {
  string text = 1;
}

message Response {
  string text = 1;
}
```

### 服务定义

服务定义用于定义客户端可以调用的 RPC 方法。以下是示例服务定义：

```proto
service Service {
  rpc Process(Request) returns (Response);
}
```

## 实现 gRPC 服务

定义 gRPC 服务后，您需要实施它。以下是 Go 中的示例实现：

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

## 调用 gRPC 服务

一旦你实现了你的 gRPC 服务，你就可以从你的客户端调用它。以下是 Go 中的示例客户端：

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

## 结论

在本文中，我们展示了如何在后端使用 gRPC。我们涵盖了以下主题：

- 设置 gRPC 服务器
- 定义一个 gRPC 服务
- 实现 gRPC 服务
- 调用 gRPC 服务

如果您想了解有关 gRPC 的更多信息，我们推荐以下资源：

- 官方 gRPC 文档：https://grpc.io/docs/
- 关于如何在 Go 中使用 gRPC 的教程：https://tutorialedge.net/golang/grpc-go-tutorial/