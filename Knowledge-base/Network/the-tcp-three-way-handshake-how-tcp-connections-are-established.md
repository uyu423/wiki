---
title: TCP 3방향 핸드셰이크: TCP 연결 설정 방법
description: 
published: true
date: 2023-03-06T11:32:34.514Z
tags: 
editor: markdown
dateCreated: 2023-03-06T11:32:33.134Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [The TCP Three-Way Handshake: How TCP Connections Are Established***English** document is available*](/en/Knowledge-base/Network/the-tcp-three-way-handshake-how-tcp-connections-are-established)
{.links-list}

# TCP 3방향 핸드셰이크: TCP 연결 설정 방법

TCP(Transmission Control Protocol)는 인터넷 프로토콜(IP) 인프라에서 가장 널리 사용되는 프로토콜입니다. TCP는 서로 다른 호스트에서 실행되는 응용 프로그램 간에 종단 간 통신을 제공하는 안정적인 연결 지향 프로토콜입니다. TCP 연결은 3방향 핸드셰이크라는 프로세스를 사용하여 설정됩니다.

## TCP 연결이란?
TCP 연결은 네트워크를 통해 두 호스트 간에 설정된 논리적 연결입니다. 이 연결은 두 호스트 간에 안정적이고 정렬된 바이트 스트림 통신 채널을 제공합니다.

TCP 연결은 연결을 설정하기 위해 두 호스트 간에 3개의 패킷을 교환하는 프로세스인 3방향 핸드셰이크를 사용하여 설정됩니다.

## TCP 3방향 핸드셰이크 이해
3방향 핸드셰이크는 TCP 연결을 설정하기 위해 두 호스트 간에 3개의 패킷을 교환하는 프로세스입니다.

1. 핸드셰이크의 첫 번째 단계에서 클라이언트는 SYN(동기화) 패킷을 서버로 보냅니다. SYN 패킷에는 무작위 시퀀스 번호와 SYN으로 설정된 TCP 플래그가 포함되어 있습니다.

2. 핸드셰이크의 두 번째 단계에서 서버는 SYN-ACK(synchronize-acknowledge) 패킷으로 응답합니다. SYN-ACK 패킷에는 클라이언트로부터 받은 시퀀스 번호보다 하나 큰 승인 번호, 임의의 시퀀스 번호, SYN 및 ACK로 설정된 TCP 플래그가 포함됩니다.

3. 핸드셰이크의 세 번째 단계에서 클라이언트는 ACK(승인) 패킷으로 응답합니다. ACK 패킷에는 서버로부터 받은 시퀀스 번호보다 하나 큰 승인 번호와 ACK로 설정된 TCP 플래그가 포함되어 있습니다.

3방향 핸드셰이크가 완료되면 클라이언트와 서버 간에 TCP 연결이 설정되고 두 호스트 간에 데이터를 전송할 수 있습니다.

## TCP 3방향 핸드셰이크 코드 예제
다음은 Python을 사용하는 TCP 3방향 핸드셰이크의 예입니다.

```python
import socket

# create a socket object
client_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# set the server address and port
server_address = ('localhost', 8888)

# connect to the server
client_socket.connect(server_address)

# send the SYN packet
client_socket.send(b'\x00\x01\x00\x00\x00\x01\x00\x00\x00\x00\x00\x00\x00\x00\x00\x00')

# receive the SYN-ACK packet
syn_ack_packet = client_socket.recv(1024)

# send the ACK packet
client_socket.send(b'\x00\x01\x00\x00\x00\x01\x00\x00\x00\x00\x00\x00\x00\x00\x00\x01')

# the connection is now established
```

## 결론
TCP 3방향 핸드셰이크는 TCP 연결을 설정하기 위해 두 호스트 간에 3개의 패킷을 교환하는 프로세스입니다. TCP는 IP 인프라에서 가장 널리 사용되는 프로토콜이므로 3방향 핸드셰이크의 작동 방식을 이해하는 것은 IT 개발에 필수적입니다.

## 외부 리소스
- [TCP 3방향 핸드셰이크](https://www.geeksforgeeks.org/tcp-3-way-handshake-process/)
- [TCP/IP 프로토콜 아키텍처 모델](https://www.networkworld.com/article/3250475/tcp-ip-protocol-architecture-model.html)
- [전송 제어 프로토콜](https://en.wikipedia.org/wiki/Transmission_Control_Protocol)