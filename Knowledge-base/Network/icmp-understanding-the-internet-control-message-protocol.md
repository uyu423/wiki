---
title: ICMP: 인터넷 제어 메시지 프로토콜 이해
description: 
published: true
date: 2023-03-03T16:32:26.979Z
tags: 
editor: markdown
dateCreated: 2023-03-03T16:32:25.622Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [ICMP: Understanding the Internet Control Message Protocol***English** document is available*](/en/Knowledge-base/Network/icmp-understanding-the-internet-control-message-protocol)
{.links-list}
### ICMP란?

ICMP(Internet Control Message Protocol)는 OSI 모델의 네트워크 계층에서 필수적인 프로토콜입니다. 오류 메시지 보고 및 네트워크 장치 간의 제어 메시지 교환을 담당합니다. ICMP는 네트워크 관리자와 엔지니어가 네트워크 문제를 해결하고 진단 정보를 제공하는 데 사용됩니다.

ICMP는 라우터, 서버 및 방화벽을 비롯한 광범위한 네트워크 장치에서 사용됩니다. 인터넷의 적절한 기능에 필수적이며 IP, TCP 및 UDP와 같은 다른 프로토콜과 함께 사용됩니다.

### ICMP는 어떻게 작동하나요?

ICMP 메시지는 일반 데이터 패킷과 마찬가지로 IP 패킷으로 전송됩니다. 장치에 오류가 발생하거나 제어 메시지를 보내야 하는 경우 ICMP 메시지를 IP 패킷에 캡슐화하여 대상 장치로 보냅니다. 그런 다음 대상 장치는 ICMP 메시지를 처리하고 적절한 조치를 취합니다.

### ICMP 메시지 유형

ICMP 메시지는 오류 메시지와 정보 메시지의 두 범주로 나눌 수 있습니다.

#### 오류 메시지

오류가 발생하면 네트워크 장치에서 오류 메시지가 생성됩니다. 가장 일반적인 오류 메시지 중 일부는 다음과 같습니다.

- 대상에 도달할 수 없음: 장치가 대상 네트워크 또는 호스트에 도달할 수 없을 때 생성됩니다.
- 시간 초과: 장치가 지정된 시간 제한 내에 패킷을 전달하지 못한 경우 발생합니다.
- 리디렉션: 라우터가 다른 게이트웨이로 트래픽을 보내도록 장치에 알릴 때 생성됩니다.

#### 정보 메시지

정보 메시지는 진단 정보를 제공하기 위해 네트워크 장치에서 생성됩니다. 가장 일반적인 정보 메시지는 다음과 같습니다.

- 에코 요청 및 응답(Ping): 다른 장치와의 연결을 테스트하기 위해 장치에서 생성됩니다.
- 타임스탬프 요청 및 응답: 네트워크의 장치 간에 시계를 동기화하기 위해 생성됩니다.
- 주소 마스크 요청 및 응답: 네트워크의 서브넷 마스크를 얻기 위해 생성됩니다.

### ICMP 및 보안

ICMP는 합법적인 목적과 악의적인 목적 모두에 사용될 수 있습니다. 예를 들어 ping은 네트워크 문제 해결에 일반적으로 사용되는 도구이지만 네트워크에서 활성 호스트를 식별하기 위한 정찰 도구로도 사용할 수 있습니다.

ICMP를 사용하여 다음과 같은 다양한 유형의 공격을 실행할 수도 있습니다.

- Ping Floods : 핑 요청의 폭주로 대상 네트워크를 압도하는 DDoS 공격 유형입니다.
- ICMP 리디렉션 공격: 트래픽 라우팅을 조작하여 악성 호스트로 리디렉션하는 공격입니다.
- 스머프 공격 : 브로드캐스트 주소로 핑 요청을 대량으로 보내 서비스 거부를 일으키는 DDoS 공격의 일종.

ICMP와 관련된 위험을 완화하기 위해 네트워크 관리자와 엔지니어는 다음과 같은 다양한 조치를 취할 수 있습니다.

- ICMP 에코 요청 비활성화: 핑 플러드가 네트워크를 압도하는 것을 방지할 수 있습니다.
- 방화벽 구성 : 의심스러운 ICMP 트래픽을 차단하도록 방화벽을 구성할 수 있습니다.
- 네트워크 트래픽 모니터링 : 관리자는 네트워크 트래픽을 모니터링하여 의심스러운 ICMP 트래픽을 감지하고 대응할 수 있습니다.

### ICMP 명령 예

다음은 ping 명령을 사용하여 Linux 시스템에서 실행할 수 있는 ICMP 명령의 몇 가지 예입니다.

```shell
# Ping a host to test connectivity
ping google.com

# Ping a host and display the round-trip time
ping -c 3 google.com

# Ping a host and display the IP address
ping -c 3 google.com | grep "64 bytes" | cut -d " " -f 4 | tr -d ":"
```

### 결론

ICMP는 OSI 모델의 네트워크 계층에서 필수적인 프로토콜입니다. 오류 메시지 보고 및 네트워크 장치 간의 제어 메시지 교환을 담당합니다. ICMP 메시지는 오류 메시지와 정보 메시지의 두 범주로 나눌 수 있습니다. ICMP는 합법적인 목적과 악의적인 목적 모두에 사용될 수 있으며 네트워크 관리자와 엔지니어는 ICMP와 관련된 위험을 완화하기 위해 적절한 조치를 취해야 합니다.

### 외부 리소스

- [RFC 792 - 인터넷 제어 메시지 프로토콜](https://datatracker.ietf.org/doc/html/rfc792)
- [ICMP 공격 이해](https://www.sans.org/reading-room/whitepapers/threats/understanding-icmp-attacks-70)
- [Ping 및 ICMP: 무엇이며 무엇을 합니까?](https://www.cloudflare.com/learning/network-layer/ping-and-icmp-overview/)