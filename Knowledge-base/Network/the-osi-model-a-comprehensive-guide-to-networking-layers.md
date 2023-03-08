---
title: OSI 모델: 네트워킹 계층에 대한 포괄적인 가이드
description: 
published: true
date: 2023-03-02T09:32:29.381Z
tags: 
editor: markdown
dateCreated: 2023-03-02T09:32:21.883Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [The OSI Model: A Comprehensive Guide to Networking Layers***English** document is available*](/en/Knowledge-base/Network/the-osi-model-a-comprehensive-guide-to-networking-layers)
{.links-list}
OSI 모델: 네트워킹 계층에 대한 포괄적인 가이드

OSI(Open Systems Interconnection) 모델은 네트워크의 서로 다른 시스템 간에 데이터가 전송되는 방식을 정의하는 개념적 프레임워크입니다. ISO(International Organization for Standardization)에서 컴퓨터가 서로 통신할 수 있는 표준화된 방법을 제공하기 위해 개발했습니다. OSI 모델은 각각 고유한 기능과 프로세스가 있는 7개의 개별 계층으로 나뉩니다. 이 기사에서는 OSI 모델과 해당 네트워킹 계층에 대한 포괄적인 가이드를 제공하고 IT 개발을 위한 실용적인 정보와 실제 솔루션을 제공합니다.

## OSI 모델 계층

OSI 모델은 각각 고유한 기능과 프로세스가 있는 7개의 계층으로 나뉩니다. 이러한 레이어는 다음과 같습니다.

1. **물리 계층:** 물리 계층은 OSI 모델의 첫 번째 계층입니다. 구리선이나 광섬유 케이블과 같은 물리적 매체를 통해 원시 데이터를 전송하는 역할을 합니다. 이 계층의 주요 기능은 디지털 데이터를 네트워크를 통해 전송할 수 있는 물리적 신호로 변환하는 것입니다.

2. **데이터 링크 계층:** 데이터 링크 계층은 OSI 모델의 두 번째 계층입니다. 동일한 네트워크 세그먼트에 있는 두 장치 간에 오류 없는 통신을 제공하는 역할을 합니다. 이 계층은 프레이밍, 오류 감지 및 흐름 제어를 담당합니다.

3. **네트워크 계층:** 네트워크 계층은 OSI 모델의 세 번째 계층입니다. 논리적 주소 지정 및 라우팅 서비스 제공을 담당합니다. 이 계층은 데이터가 소스에서 대상으로 이동하는 최상의 경로를 결정하는 역할을 합니다.

4. **전송 계층:** 전송 계층은 OSI 모델의 네 번째 계층입니다. 종단 간 안정적인 데이터 전송을 제공합니다. 이 계층은 오류 복구 및 흐름 제어를 담당합니다.

5. **세션 계층:** 세션 계층은 OSI 모델의 다섯 번째 계층입니다. 서로 다른 장치의 응용 프로그램 간의 세션 설정, 관리 및 종료를 담당합니다. 이 계층은 동기화 및 검사점 지정을 담당합니다.

6. **프레젠테이션 계층:** 프레젠테이션 계층은 OSI 모델의 여섯 번째 계층입니다. 데이터가 네트워크를 통해 전송될 수 있도록 형식화, 암호화 및 압축을 담당합니다. 이 계층은 데이터 변환 및 암호화를 담당합니다.

7. **응용 계층:** 응용 계층은 OSI 모델의 7번째 계층입니다. 애플리케이션에 네트워크 서비스를 제공하는 역할을 담당합니다. 이 계층은 사용자 인증 및 데이터 암호화를 담당합니다.

## OSI 모델 기능

OSI 모델은 컴퓨터가 서로 통신할 수 있는 표준화된 방법을 제공하도록 설계되었습니다. OSI 모델의 각 계층은 통신이 발생하는 데 필요한 특정 기능을 수행합니다. 이러한 기능에는 다음이 포함됩니다.

- **데이터 캡슐화:** OSI 모델의 각 계층은 스택 아래로 이동할 때 데이터 패킷에 자체 머리글과 바닥글을 추가합니다. 이 프로세스를 데이터 캡슐화라고 합니다.

- **프로토콜 변환:** OSI 모델의 각 계층은 특정 프로토콜을 사용하여 상위 및 하위 계층과 통신합니다. 이를 통해 서로 다른 프로토콜을 사용하는 장치가 서로 통신할 수 있습니다.

- **오류 감지 및 복구:** OSI 모델의 각 계층은 오류 감지 및 복구를 담당합니다. 이렇게 하면 데이터가 정확하고 안정적으로 전송됩니다.

## 실제 애플리케이션의 OSI 모델

OSI 모델을 이해하는 것은 컴퓨터 네트워크 구축 및 문제 해결을 위한 프레임워크를 제공하므로 IT 개발에 중요합니다. OSI 모델은 네트워크 프로토콜 및 애플리케이션을 설계하고 문제를 해결하는 데 사용됩니다. OSI 모델의 일부 실제 응용 프로그램은 다음과 같습니다.

- **TCP/IP 프로토콜 제품군:** TCP/IP 프로토콜 제품군은 인터넷을 통해 데이터를 전송하는 데 사용되는 프로토콜 집합입니다. OSI 모델을 기반으로 하며 4개의 계층으로 구성됩니다.

- **이더넷 프로토콜:** 이더넷은 근거리 통신망(LAN)에서 장치를 연결하는 데 사용되는 널리 사용되는 네트워킹 프로토콜입니다. OSI 모델의 데이터 링크 계층을 기반으로 합니다.

- **무선 네트워킹:** 무선 네트워킹은 OSI 모델을 사용하여 장치 간에 무선 연결을 제공합니다. OSI 모델의 물리 계층은 공중파를 통해 데이터를 전송하는 데 사용됩니다.

## 코드 예제

다음은 OSI 모델의 사용을 설명하는 몇 가지 코드 스니펫입니다.

### TCP/IP 프로토콜 제품군

TCP/IP 프로토콜 제품군은 OSI 모델을 기반으로 합니다. 다음은 Python에서 TCP/IP 프로토콜 제품군이 사용되는 방법의 예입니다.

```python
import socket

# create a socket object
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# connect to the server
s.connect(('127.0.0.1', 8080))

# send some data
s.send('Hello World')

# receive some data
data = s.recv(1024)

# close the socket
s.close()
```

### 이더넷 프로토콜

이더넷은 근거리 통신망(LAN)에서 장치를 연결하는 데 사용되는 널리 사용되는 네트워킹 프로토콜입니다. 다음은 C에서 이더넷이 사용되는 방법의 예입니다.

```c
#include <stdio.h>
#include <string.h>
#include <sys/socket.h>
#include <arpa/inet.h>
#include <net/ethernet.h>

int main(int argc, char *argv[])
{
    int socket_desc;
    struct sockaddr_in server;
    char *message, server_reply[2000];
    struct ether_header eh;
    
    // create a socket
    socket_desc = socket(AF_INET, SOCK_STREAM, 0);
    
    // set the server address
    server.sin_addr.s_addr = inet_addr("127.0.0.1");
    server.sin_family = AF_INET;
    server.sin_port = htons( 8080 );
    
    // connect to the server
    connect(socket_desc, (struct sockaddr *)&server, sizeof(server));
    
    // send some data
    strcpy(message, "Hello World");
    eh.ether_shost[0] = 0x00;
    eh.ether_shost[1] = 0x11;
    eh.ether_shost[2] = 0x22;
    eh.ether_shost[3] = 0x33;
    eh.ether_shost[4] = 0x44;
    eh.ether_shost[5] = 0x55;
    eh.ether_dhost[0] = 0x00;
    eh.ether_dhost[1] = 0x11;
    eh.ether_dhost[2] = 0x22;
    eh.ether_dhost[3] = 0x33;
    eh.ether_dhost[4] = 0x44;
    eh.ether_dhost[5] = 0x66;
    eh.ether_type = htons(ETH_P_IP);
    send(socket_desc, &eh, sizeof(eh), 0);
    send(socket_desc, message, strlen(message), 0);
    
    // receive some data
    recv(socket_desc, server_reply, 2000, 0);
    
    // close the socket
    close(socket_desc);
    
    return 0;
}
```

## 결론

OSI 모델은 컴퓨터가 네트워크를 통해 서로 통신하는 방법을 이해하기 위한 중요한 프레임워크입니다. OSI 모델은 프로세스를 7개의 개별 계층으로 나누어 개발자가 네트워크 프로토콜 및 응용 프로그램을 설계하고 문제를 해결할 수 있는 표준화된 방법을 제공합니다. OSI 모델을 이해하는 것은 IT 개발에 필수적이며 TCP/IP 및 이더넷과 같은 네트워킹 프로토콜에 실제 응용 프로그램이 있습니다.

## 외부 리소스

- [OSI 모델 - Wikipedia](https://en.wikipedia.org/wiki/OSI_model)
- [TCP/IP 프로토콜 제품군 - Wikipedia](https://en.wikipedia.org/wiki/Internet_protocol_suite)
- [이더넷 - Wikipedia](https://en.wikipedia.org/wiki/Ethernet)