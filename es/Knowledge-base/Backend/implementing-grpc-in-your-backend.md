---
title: Implementando gRPC en su backend
description: 
published: true
date: 2023-02-01T23:43:42.620Z
tags: 
editor: markdown
dateCreated: 2023-02-01T23:43:40.990Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Implementing gRPC in Your Backend***English** document is available*](/en/Knowledge-base/Backend/implementing-grpc-in-your-backend)
{.links-list}


# Implementando gRPC en su backend

## Introducción

gRPC es un marco RPC moderno de código abierto que puede ejecutarse en cualquier entorno. Utiliza HTTP/2 para el transporte y Protocol Buffers para la serialización de mensajes. gRPC está disponible en muchos lenguajes, incluidos C# , Go, Java, Node.js, PHP, Python y Ruby.

En este artículo, le mostraremos cómo usar gRPC en su backend. Cubriremos los siguientes temas:

- Configuración de un servidor gRPC
- Definición de un servicio gRPC
- Implementación de un servicio gRPC
- Llamar a un servicio gRPC

## Configuración de un servidor gRPC

Lo primero que debe hacer es instalar el servidor gRPC. Puedes hacer esto usando el siguiente comando:

```
$ go get -u github.com/grpc/grpc-go/cmd/grpc_server
```

Una vez que el servidor está instalado, debe iniciarlo. Puedes hacer esto usando el siguiente comando:

```
$ grpc_server
```

El servidor se iniciará y escuchará en el puerto 8080 de forma predeterminada.

## Definición de un servicio gRPC

A continuación, debe definir un servicio gRPC. Un servicio de gRPC se define mediante un archivo .proto. El archivo contiene lo siguiente:

- Una definición de mensaje
- Una definición de servicio

### Definición de mensaje

Se utiliza una definición de mensaje para definir los datos que se intercambiarán entre el cliente y el servidor. La siguiente es una definición de mensaje de ejemplo:

```proto
message Request {
  string text = 1;
}

message Response {
  string text = 1;
}
```

### Definición de servicio

Se utiliza una definición de servicio para definir los métodos RPC que puede llamar el cliente. La siguiente es una definición de servicio de ejemplo:

```proto
service Service {
  rpc Process(Request) returns (Response);
}
```

## Implementando un servicio gRPC

Una vez que haya definido su servicio gRPC, debe implementarlo. El siguiente es un ejemplo de implementación en Go:

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

## Llamar a un servicio gRPC

Una vez que haya implementado su servicio gRPC, puede llamarlo desde su cliente. El siguiente es un cliente de ejemplo en Go:

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

## Conclusión

En este artículo, mostramos cómo usar gRPC en su backend. Hemos cubierto los siguientes temas:

- Configuración de un servidor gRPC
- Definición de un servicio gRPC
- Implementación de un servicio gRPC
- Llamar a un servicio gRPC

Si desea obtener más información sobre gRPC, le recomendamos los siguientes recursos:

- La documentación oficial de gRPC: https://grpc.io/docs/
- Un tutorial sobre cómo usar gRPC en Go: https://tutorialedge.net/golang/grpc-go-tutorial/