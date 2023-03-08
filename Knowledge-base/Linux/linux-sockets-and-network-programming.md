---
title: Linux 소켓 및 네트워크 프로그래밍
description: 
published: true
date: 2023-02-12T00:32:25.603Z
tags: 
editor: markdown
dateCreated: 2023-02-12T00:32:18.598Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Linux Sockets and Network Programming***English** document is available*](/en/Knowledge-base/Linux/linux-sockets-and-network-programming)
{.links-list}


# 리눅스 소켓과 네트워크 프로그래밍

이 기사에서 우리는 리눅스 소켓과 네트워크 프로그래밍에 대해 논의할 것입니다. 그것들이 무엇인지, 어떻게 작동하는지, 몇 가지 일반적인 사용 사례를 다룰 것입니다. 또한 사용 방법을 설명하기 위해 C로 된 몇 가지 코드 예제를 제공합니다.

## 소켓이란?

컴퓨터 네트워킹에서 소켓은 양방향 또는 단방향 데이터 통신 채널의 끝점입니다. 소켓을 사용하여 두 컴퓨터 간에 연결을 설정한 다음 데이터를 교환하는 데 사용할 수 있습니다.

소켓은 스트림 지향 또는 데이터그램 지향일 수 있습니다. 스트림 지향 소켓은 두 컴퓨터 간에 안정적이고 순서가 있으며 오류가 확인된 연결을 제공합니다. 반면에 데이터그램 지향 소켓은 연결이 없으며 데이터가 전송된 순서대로 전달된다는 것을 보장하지 않습니다.

## 어떻게 작동하나요?

소켓은 한 컴퓨터에서 포트 번호에 바인딩된 소켓 객체를 생성하여 작동합니다. 그런 다음 이 소켓 객체를 사용하여 역시 포트 번호에 바인딩된 다른 컴퓨터의 소켓에 연결할 수 있습니다. 연결이 설정되면 두 컴퓨터 간에 데이터를 교환할 수 있습니다.

## 일반적인 사용 사례

응용 프로그램에서 소켓을 사용하려는 이유는 많습니다. 몇 가지 일반적인 사용 사례는 다음과 같습니다.

- 채팅 애플리케이션 만들기
- 멀티플레이어 게임 만들기
- 한 컴퓨터에서 다른 컴퓨터로 데이터 보내기
- 웹 서버 생성

## 코드 예시

다음은 소켓을 사용하는 방법을 설명하기 위해 C로 작성된 몇 가지 코드 예제입니다.

### 소켓 생성

소켓을 생성하려면 `socket()` 함수를 사용해야 합니다. 이 함수는 세 가지 인수를 사용합니다.

- 소켓의 주소 패밀리(예: IPv4의 경우 `AF_INET` 또는 IPv6의 경우 `AF_INET6`)
- 소켓의 유형(예: 스트림 지향 소켓의 경우 `SOCK_STREAM` 또는 데이터그램 지향 소켓의 경우 `SOCK_DGRAM`)
- 소켓의 프로토콜(예: TCP의 경우 `IPPROTO_TCP` 또는 UDP의 경우 `IPPROTO_UDP`)

```c
int sockfd = socket(AF_INET, SOCK_STREAM, IPPROTO_TCP);
```

### 소켓에 연결하기

소켓에 연결하려면 `connect()` 함수를 사용해야 합니다. 이 함수는 세 가지 인수를 사용합니다.

- 소켓 파일 설명자
- 연결할 소켓의 주소(`struct sockaddr *`로 캐스트)
- 주소의 크기

```c
struct sockaddr_in addr;
addr.sin_family = AF_INET;
addr.sin_port = htons(80);
addr.sin_addr.s_addr = inet_addr("127.0.0.1");

connect(sockfd, (struct sockaddr *)&addr, sizeof(addr));
```

### 데이터 보내기

데이터를 보내려면 `send()` 함수를 사용해야 합니다. 이 함수는 세 가지 인수를 사용합니다.

- 소켓 파일 설명자
- 보낼 데이터(`void *`로 변환)
- 데이터의 크기

```c
char buf[1024];

send(sockfd, buf, sizeof(buf), 0);
```

### 데이터 수신

데이터를 받으려면 `recv()` 함수를 사용해야 합니다. 이 함수는 다음 네 가지 인수를 사용합니다.

- 소켓 파일 설명자
- 데이터를 저장할 버퍼(`void *`로 변환)
- 버퍼의 크기
- 플래그(예: 모든 데이터가 도착하기를 기다리는 `MSG_WAITALL`)

```c
char buf[1024];

recv(sockfd, buf, sizeof(buf), MSG_WAITALL);
```

## 소켓 닫기

소켓을 닫으려면 `close()` 함수를 사용해야 합니다. 이 함수는 단일 인수를 사용합니다.

- 소켓 파일 설명자

```c
close(sockfd);
```

## 외부 리소스

- [ Beej의 네트워크 프로그래밍 가이드](https://beej.us/guide/bgnet/)
- [예제에 의한 Linux 소켓 프로그래밍](https://www.amazon.com/Linux-Socket-Programming-Example-Addison-Wesley/dp/0321524713)
- [리눅스 소켓 프로그래밍 책](https://www.amazon.com/Linux-Socket-Programming-Mark-Twain/dp/188477749X)