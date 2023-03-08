---
title: Linux Sockets y Programación de Redes
description: 
published: true
date: 2023-02-12T00:32:25.603Z
tags: 
editor: markdown
dateCreated: 2023-02-12T00:32:18.603Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Linux Sockets and Network Programming***English** document is available*](/en/Knowledge-base/Linux/linux-sockets-and-network-programming)
{.links-list}


# Linux Sockets y Programación de Redes

En este artículo, discutiremos los sockets de Linux y la programación de redes. Cubriremos qué son, cómo funcionan y algunos casos de uso comunes. También proporcionaremos algunos ejemplos de código en C para ilustrar cómo usarlos.

## ¿Qué son los enchufes?

En las redes informáticas, un socket es un punto final de un canal de comunicación de datos bidireccional o unidireccional. Los sockets se pueden usar para establecer una conexión entre dos computadoras, que luego se pueden usar para intercambiar datos.

Los sockets pueden estar orientados a secuencias u orientados a datagramas. Los sockets orientados a flujo proporcionan una conexión confiable, ordenada y con verificación de errores entre dos computadoras. Los sockets orientados a datagramas, por otro lado, no tienen conexión y no garantizan que los datos se entreguen en el mismo orden en que se enviaron.

## ¿Cómo trabajan?

Los sockets funcionan mediante la creación de un objeto de socket en una computadora, que está vinculado a un número de puerto. Este objeto de socket se puede usar para conectarse a un socket en otra computadora, que también está vinculada a un número de puerto. Una vez que se establece una conexión, se pueden intercambiar datos entre las dos computadoras.

## Casos de uso comunes

Hay muchas razones por las que podría querer usar sockets en sus aplicaciones. Algunos casos de uso comunes incluyen:

- Creación de una aplicación de chat.
- Creación de un juego multijugador
- Envío de datos de un ordenador a otro
- Creación de un servidor web

## Ejemplos de código

Aquí hay algunos ejemplos de código en C para ilustrar cómo usar sockets.

### Creando un zócalo

Para crear un socket, debe usar la función `socket()`. Esta función toma tres argumentos:

- La familia de direcciones del socket (por ejemplo, `AF_INET` para IPv4 o `AF_INET6` para IPv6)
- El tipo de socket (por ejemplo, `SOCK_STREAM` para un socket orientado a secuencias o `SOCK_DGRAM` para un socket orientado a datagramas)
- El protocolo del socket (por ejemplo, `IPPROTO_TCP` para TCP o `IPPROTO_UDP` para UDP)

```c
int sockfd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
```

### Conexión a un enchufe

Para conectarse a un socket, necesita usar la función `connect()`. Esta función toma tres argumentos:

- El descriptor de archivo de socket
- La dirección del socket al que conectarse (transmitido a `struct sockaddr *`)
- El tamaño de la dirección.

```c
struct sockaddr_in addr;
addr.sin_family = AF_INET;
addr.sin_port = htons(80);
addr.sin_addr.s_addr = inet_addr("127.0.0.1");

connect(sockfd, (struct sockaddr *)&addr, sizeof(addr));
```

### Enviando datos

Para enviar datos, debe utilizar la función `send()`. Esta función toma tres argumentos:

- El descriptor de archivo de socket
- Los datos a enviar (cast to a `void *`)
- El tamaño de los datos.

```c
char buf[1024];

send(sockfd, buf, sizeof(buf), 0);
```

### Recibiendo información

Para recibir datos, necesita usar la función `recv()`. Esta función toma cuatro argumentos:

- El descriptor de archivo de socket
- El búfer para almacenar los datos (convertido en un `vacío *`)
- El tamaño del búfer
- Las banderas (por ejemplo, `MSG_WAITALL` para esperar a que lleguen todos los datos)

```c
char buf[1024];

recv(sockfd, buf, sizeof(buf), MSG_WAITALL);
```

## Cerrar un socket

Para cerrar un socket, debe usar la función `close()`. Esta función toma un único argumento:

- El descriptor de archivo de socket

```c
close(sockfd);
```

## Recursos externos

- [Guía de programación de red de Beej](https://beej.us/guide/bgnet/)
- [Programación de sockets de Linux por ejemplo](https://www.amazon.com/Linux-Socket-Programming-Example-Addison-Wesley/dp/0321524713)
- [El libro de programación de sockets de Linux](https://www.amazon.com/Linux-Socket-Programming-Mark-Twain/dp/188477749X)