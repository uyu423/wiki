---
title: Building Backend Systems with gRPC
description: 
published: true
date: 2023-02-17T18:00:51.188Z
tags: 
editor: markdown
dateCreated: 2023-01-29T20:52:09.319Z
---

- [gRPC로 백엔드 시스템 구축***Korean** version of this document is available*](/ko/Knowledge-base/Backend/building-backend-systems-with-grpc)
{.links-list}


# Building Backend Systems with gRPC 

In this article, we'll take a look at how to use gRPC to build backend systems. gRPC is a language-neutral, platform-neutral RPC framework that enables client and server applications to communicate transparently. It is based on the HTTP/2 protocol and uses Protocol Buffers as its interface description language.

gRPC is a great choice for building backend services. It is efficient and easy to use. In this article, we'll see how to use gRPC to build a simple backend service. We'll start by looking at the basics of gRPC and then we'll implement a simple service.

## What is gRPC? 

gRPC is a language-neutral, platform-neutral RPC framework that enables client and server applications to communicate transparently. It is based on the HTTP/2 protocol and uses Protocol Buffers as its interface description language.

gRPC is a great choice for building backend services. It is efficient and easy to use. In this article, we'll see how to use gRPC to build a simple backend service.

## Why use gRPC? 

gRPC is a great choice for building backend services for a number of reasons:

- It is efficient. gRPC uses HTTP/2, which is a binary protocol that is more efficient than HTTP/1.1.
- It is easy to use. gRPC uses Protocol Buffers as its interface description language. Protocol Buffers are a way to encode data in a format that is both efficient and easy to use.
- It is language-neutral. gRPC is based on the HTTP/2 protocol, which is language-neutral. This means that gRPC can be used with any programming language.

## How does gRPC work? 

gRPC works by defining a service in a .proto file. The .proto file defines the methods that can be called, the parameters that can be passed, and the return types.

The .proto file is then used to generate code in the language of your choice. The generated code contains the methods that can be called, the parameters that can be passed, and the return types.

## How do I use gRPC? 

In order to use gRPC, you need to install the gRPC library for your language of choice. You can find the installation instructions for the gRPC library here:

https://grpc.io/docs/languages/

Once you have installed the gRPC library, you can use the generated code to call the methods defined in the .proto file.

## Example 

Let's take a look at a simple example. We'll start by defining a service in a .proto file.

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

This .proto file defines a service with a single method, SayHello. The SayHello method takes a HelloRequest and returns a HelloResponse.

The HelloRequest contains a single field, name, which is a string. The HelloResponse contains a single field, message, which is also a string.

Now that we have defined our service, we can generate code in the language of our choice. We'll use the protoc tool to generate the code. The protoc tool is available here:

https://github.com/google/protobuf/releases

Once you have downloaded and installed the protoc tool, you can use it to generate the code. The following command will generate the code for the Greeter service in the Go programming language:

```
protoc -I . greeter.proto --go_out=plugins=grpc:.
```

This command will generate a file called greeter.pb.go. This file contains the generated code for the Greeter service.

The generated code contains the methods that can be called, the parameters that can be passed, and the return types. In our example, the generated code contains a SayHello method. This method takes a HelloRequest and returns a HelloResponse.

We can use the generated code to call the SayHello method. The following code shows how to call the SayHello method in the Go programming language:

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

This code creates a connection to the server and then calls the SayHello method. The SayHello method takes a HelloRequest and returns a HelloResponse. The HelloRequest contains a name field. The HelloResponse contains a message field.

The code prints the message field from the HelloResponse. In our example, the message field contains the string "Hello World".

## Conclusion 

In this article, we've seen how to use gRPC to build backend services. gRPC is a great choice for building backend services. It is efficient and easy to use. In this article, we've seen how to use gRPC to build a simple backend service.