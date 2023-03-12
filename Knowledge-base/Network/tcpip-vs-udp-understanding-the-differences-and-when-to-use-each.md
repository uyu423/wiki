---
title: TCP/IP 대 UDP: 차이점 이해 및 각 사용 시기
description: 
published: true
date: 2023-03-12T01:32:37.706Z
tags: 
editor: markdown
dateCreated: 2023-03-12T01:32:37.705Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [TCP/IP vs. UDP: Understanding the Differences and When to Use Each***English** document is available*](/en/Knowledge-base/Network/tcpip-vs-udp-understanding-the-differences-and-when-to-use-each)
{.links-list}

TCP/IP 대 UDP: 차이점 이해 및 각 사용 시기

TCP(Transmission Control Protocol) 및 UDP(User Datagram Protocol)는 컴퓨터 네트워크에서 사용되는 두 가지 주요 통신 프로토콜입니다. 인터넷 프로토콜(IP)은 인터넷을 통한 통신에 사용되는 주요 프로토콜이며 TCP와 UDP를 모두 사용합니다. TCP와 UDP는 기본 프로토콜로 동일한 IP를 공유하지만 다른 기능을 제공합니다. 강력하고 신뢰할 수 있는 네트워크 응용 프로그램을 구축하기 위해 이 두 프로토콜 간의 차이점과 각 프로토콜을 사용하는 시기를 이해하는 것이 중요합니다.

## TCP/IP란?

TCP는 응용 프로그램 간에 안정적이고 순서가 지정된 데이터 전달을 제공하는 연결 지향 프로토콜입니다. TCP는 데이터 전송 전에 두 끝점 사이에 연결을 설정하고 모든 패킷이 대상에 올바르게 전달되도록 합니다. 3방향 핸드셰이크 프로세스를 사용하여 연결을 설정하고 데이터 전송 순서를 유지하며 데이터 무결성을 확인합니다. TCP는 파일 전송, 이메일 및 웹 브라우징과 같이 안정적인 데이터 전송이 필요한 애플리케이션에 사용됩니다.

## UDP란?

UDP는 응용 프로그램 간에 빠르고 신뢰할 수 없는 데이터 전달을 제공하는 연결 없는 프로토콜입니다. TCP와 달리 데이터 전송 전에 연결을 설정하지 않으며 데이터 무결성 검사를 제공하지 않습니다. UDP는 비디오 및 오디오 스트리밍, 온라인 게임 및 실시간 통신과 같이 더 빠른 데이터 전송이 필요한 응용 프로그램에 사용됩니다.

## TCP와 UDP의 주요 차이점

TCP와 UDP 사이에는 다음을 포함하여 몇 가지 차이점이 있습니다.

### 연결 지향 vs. 비연결

위에서 언급했듯이 TCP는 데이터 전송 전에 연결을 설정하는 연결 지향 프로토콜인 반면 UDP는 연결이 없고 데이터 전송 전에 연결을 설정하지 않습니다.

### 신뢰성

TCP는 신뢰할 수 있는 데이터 전송을 제공하여 모든 패킷이 올바른 순서로 대상에 전달되도록 합니다. UDP는 빠른 데이터 전송을 제공하지만 모든 패킷이 대상에 전달된다는 보장은 없으며 패킷이 순서 없이 도착할 수 있습니다.

### 감사의 말

TCP는 승인을 사용하여 대상에서 데이터 패킷을 수신했는지 확인합니다. 패킷이 손실되거나 손상되면 수신자는 보낸 사람에게 손실된 패킷을 다시 전송하도록 요청합니다. 반대로 UDP는 승인을 제공하지 않으며 손실된 패킷은 재전송되지 않습니다.

### 흐름 제어

TCP는 흐름 제어를 사용하여 발신자와 수신자 간에 전송되는 데이터의 양을 조절합니다. 수신자가 발신자가 보낸 데이터의 양을 처리할 수 있도록 하여 수신자의 과부하로 인한 패킷 손실을 방지합니다. 대조적으로 UDP에는 흐름 제어가 없으며 발신자는 어떤 속도로든 데이터를 보낼 수 있으므로 잠재적으로 수신자를 압도할 수 있습니다.

### 오류 확인

TCP는 체크섬을 사용하여 데이터 패킷이 오류 없이 전달되도록 합니다. 오류가 감지되면 TCP는 송신자에게 패킷 재전송을 요청합니다. UDP는 또한 오류 검사를 제공하지만 손실된 패킷의 재전송을 요청하지 않습니다.

## TCP를 사용하는 경우

TCP는 웹 브라우징, 이메일 및 파일 전송과 같이 안정적인 데이터 전송 및 주문이 필요한 애플리케이션에 이상적입니다. TCP는 데이터 전송 전에 연결을 설정하고 데이터 무결성 검사를 제공하여 모든 데이터가 오류 없이 대상에 전달되도록 합니다. TCP는 또한 데이터 흐름 제어가 필요한 애플리케이션에 적합하여 과부하된 수신기로 인한 패킷 손실을 방지합니다.

다음은 Python에서 TCP 소켓 프로그래밍의 예입니다.

```python
import socket

# create a TCP socket
tcp_socket = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# connect to a remote server
tcp_socket.connect(('www.example.com', 80))

# send data
tcp_socket.send(b'GET / HTTP/1.1\r\nHost: www.example.com\r\n\r\n')

# receive data
data = tcp_socket.recv(1024)

# close the socket
tcp_socket.close()
```

이 코드는 TCP 소켓을 만들고 HTTP 프로토콜을 사용하여 원격 서버에 연결합니다. 서버에 HTTP 요청을 보내고 응답을 받습니다.

## UDP를 사용하는 경우

UDP는 비디오 및 오디오 스트리밍, 온라인 게임, 실시간 통신과 같이 빠른 데이터 전송이 필요하고 안정적인 데이터 전달이 필요하지 않은 애플리케이션에 이상적입니다. UDP는 데이터 전송 전에 연결을 설정하지 않고 데이터 무결성 검사를 제공하지 않으므로 데이터 전송 속도가 빨라집니다. UDP는 승인이나 재전송을 기다릴 필요가 없기 때문에 최소한의 대기 시간이 필요한 애플리케이션에도 적합합니다.

다음은 Python에서 UDP 소켓 프로그래밍의 예입니다.

```python
import socket

# create a UDP socket
udp_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# send data
udp_socket.sendto(b'Hello, world!', ('www.example.com', 1234))

# receive data
data, address = udp_socket.recvfrom(1024)

# close the socket
udp_socket.close()
```

이 코드는 UDP 소켓을 만들고 원격 서버에 메시지를 보냅니다. 서버에서 응답을 받고 소켓을 닫습니다.

## 결론

TCP와 UDP는 컴퓨터 네트워크에서 사용되는 두 가지 기본 통신 프로토콜입니다. TCP는 신뢰할 수 있고 순서가 지정된 데이터 전송을 제공하는 반면 UDP는 빠르고 신뢰할 수 없는 데이터 전송을 제공합니다. 강력하고 신뢰할 수 있는 네트워크 응용 프로그램을 구축하기 위해 이 두 프로토콜 간의 차이점과 각 프로토콜을 사용하는 시기를 이해하는 것이 중요합니다.

## 외부 리소스

- [TCP와 UDP: 차이점은 무엇인가요?](https://www.cloudflare.com/learning/ddos/glossary/tcp-vs-udp/)
- [TCP/IP 대 UDP: 차이점 이해](https://www.lifewire.com/tcp-ip-and-udp-explained-373381)
- [TCP/IP 및 UDP 설명](https://www.inetdaemon.com/tutorials/internet/ip/protocols/tcp_vs_udp.shtml)