---
title: TCP 최대 세그먼트 크기: TCP 성능을 최적화하는 방법
description: 
published: true
date: 2023-03-07T12:33:05.653Z
tags: 
editor: markdown
dateCreated: 2023-03-07T12:33:05.653Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [The TCP Maximum Segment Size: How to Optimize TCP Performance***English** document is available*](/en/Knowledge-base/Network/the-tcp-maximum-segment-size-how-to-optimize-tcp-performance)
{.links-list}

TCP 최대 세그먼트 크기: TCP 성능을 최적화하는 방법

TCP(전송 제어 프로토콜)는 인터넷 프로토콜(IP) 제품군의 핵심 프로토콜 중 하나입니다. 호스트에서 실행되는 애플리케이션 간에 안정적이고 순서가 있으며 오류가 확인된 데이터 전달을 제공합니다. 그러나 TCP 성능은 최대 세그먼트 크기(MSS)를 비롯한 다양한 요인의 영향을 받을 수 있습니다. 이 기사에서는 TCP MSS와 이를 최적화하여 TCP 성능을 향상시키는 방법에 대해 설명합니다.

## TCP 최대 세그먼트 크기는 무엇입니까?

TCP MSS는 호스트가 단일 TCP 세그먼트에서 기꺼이 받아들이는 최대 데이터 양입니다. TCP 세그먼트는 TCP 연결을 통해 호스트 간에 교환되는 데이터 단위입니다. 헤더와 페이로드로 구성됩니다. 헤더에는 시퀀스 번호 및 플래그와 같은 제어 정보가 포함되며 페이로드에는 전송되는 실제 데이터가 포함됩니다.

TCP MSS는 두 호스트 간에 TCP 연결을 설정하는 프로세스인 TCP 3방향 핸드셰이크 중에 협상됩니다. 클라이언트는 클라이언트가 수락하려는 MSS 값을 포함하는 SYN(동기화) 세그먼트를 서버로 보냅니다. 서버는 서버가 수락하려는 MSS 값을 포함하는 SYN-ACK(synchronize-acknowledge) 세그먼트로 응답합니다. 클라이언트는 ACK(확인) 세그먼트로 서버의 응답을 확인합니다.

기본 TCP MSS 값은 일반적으로 대부분의 네트워크에서 단일 IP 패킷으로 전송할 수 있는 최대 데이터 크기인 1460바이트로 설정됩니다. 그러나 최대 패킷 크기를 제한하는 라우터나 방화벽과 같은 장치가 네트워크 경로에 포함된 경우 실제 TCP MSS는 더 작을 수 있습니다.

## TCP 최대 세그먼트 크기가 중요한 이유는 무엇입니까?

TCP MSS는 여러 방식으로 TCP 성능에 영향을 줄 수 있습니다. 첫째, 더 작은 MSS는 주어진 양의 데이터를 전송하는 데 필요한 TCP 세그먼트의 수를 증가시킬 수 있으며, 이는 TCP 프로토콜의 오버헤드를 증가시킬 수 있습니다. 둘째, 작은 MSS는 네트워크의 최대 전송 단위(MTU)에 맞도록 큰 TCP 세그먼트를 더 작은 IP 조각으로 나누는 프로세스인 TCP 조각화 가능성을 높일 수 있습니다. 조각화는 특히 오류율이 높은 네트워크에서 네트워크 대기 시간을 늘리고 TCP 성능을 저하시킬 수 있습니다.

반면에 더 큰 MSS는 TCP 프로토콜의 오버헤드를 줄이고 TCP 조각화 가능성을 최소화하여 TCP 성능을 향상시킬 수 있습니다. 그러나 더 큰 MSS는 특히 오류율이 높은 네트워크에서 패킷 손실 가능성을 높일 수도 있습니다. 이는 더 큰 TCP 세그먼트가 손상되거나 손실된 패킷을 포함할 가능성이 더 높기 때문입니다.

## TCP 최대 세그먼트 크기를 최적화하는 방법은 무엇입니까?

최적의 TCP MSS 값은 네트워크 경로, 애플리케이션 요구 사항 및 호스트 리소스를 비롯한 여러 요인에 따라 달라집니다. 일반적으로 TCP MSS는 TCP 조각화나 과도한 패킷 손실이 발생하지 않는 가장 큰 값으로 설정해야 합니다.

### 1. 경로 MTU 결정

경로 MTU는 주어진 네트워크 경로에서 단편화 없이 전송할 수 있는 IP 패킷의 최대 크기입니다. 최대 패킷 크기를 제한하는 라우터나 방화벽과 같은 모든 장치뿐만 아니라 경로를 따라 있는 각 네트워크 링크의 MTU에 따라 달라집니다. 경로 MTU를 결정하려면 "dont-fragment" 플래그와 함께 "traceroute" 또는 "ping" 명령을 사용하여 다른 패킷 크기로 네트워크 경로를 조사할 수 있습니다.

```{language} {code}
$ traceroute -n -M do -p 80 example.com
```

```{language} {code}
$ ping -c 1 -D -s 1500 example.com
```

경로 MTU를 결정하면 IP 헤더 크기(일반적으로 20바이트)와 TCP 헤더 크기(일반적으로 20바이트)를 빼서 최대 TCP 페이로드 크기를 얻을 수 있습니다.

### 2. TCP MSS 설정

TCP MSS를 설정하려면 네트워크 경로를 따라 위치한 라우터 또는 방화벽과 같은 네트워크 장치에서 "ip tcp adjust-mss" 명령을 사용할 수 있습니다. 이 명령은 경로 MTU를 기반으로 장치를 통과하는 TCP SYN 세그먼트의 MSS 값을 조정합니다.

```{language} {code}
R1(config)# interface GigabitEthernet0/0
R1(config-if)# ip tcp adjust-mss 1400
```

또는 Linux 또는 macOS 호스트에서 "iptables" 또는 "ipfw" 방화벽 규칙을 사용하거나 Windows 호스트에서 "netsh" 명령을 사용하여 호스트 자체에서 TCP MSS를 설정할 수 있습니다.

```{language} {code}
$ sudo iptables -A FORWARD -p tcp --tcp-flags SYN,RST SYN -j TCPMSS --set-mss 1400
```

```{language} {code}
$ sudo ipfw add pipe 1 tcp from any to any setup via en0 tcpflags syn mss 1400
```

```{language} {code}
C:\> netsh interface ipv4 set subinterface "Local Area Connection" mtu=1400 store=persistent
```

### 3. TCP 성능 테스트

TCP MSS를 설정한 후에는 TCP 성능을 테스트하여 애플리케이션 요구 사항을 충족하는지 확인해야 합니다. "iperf" 또는 "ttcp"와 같은 도구를 사용하여 호스트 간의 TCP 처리량 및 대기 시간을 측정할 수 있습니다.

```{language} {code}
$ iperf -s
```

```{language} {code}
$ iperf -c 192.168.1.1 -M 1400
```

```{language} {code}
$ ttcp -r
```

```{language} {code}
$ ttcp -t 192.168.1.1 -m 1400
```

TCP 성능이 애플리케이션 요구 사항을 충족하지 않는 경우 TCP MSS 값을 조정하고 최적의 TCP 성능을 얻을 때까지 테스트를 반복할 수 있습니다.

## 결론

TCP MSS는 TCP 성능에 영향을 미칠 수 있는 중요한 매개변수입니다. TCP MSS를 최적의 값으로 설정하면 TCP 통신의 효율성과 안정성을 향상시킬 수 있습니다. 그러나 최적의 TCP MSS는 다양한 요인에 따라 다르며 최상의 결과를 얻으려면 테스트 및 조정이 필요할 수 있습니다. 이 기사의 지침을 따르면 TCP MSS를 최적화하고 애플리케이션의 성능을 향상시킬 수 있습니다.

## 외부 리소스

- [RFC 879 - TCP 최대 세그먼트 크기 및 관련 항목](https://tools.ietf.org/html/rfc879)
- [RFC 1191 - 경로 MTU 검색](https://tools.ietf.org/html/rfc1191)
- [TCP 최대 세그먼트 크기(MSS) 관리](https://www.cisco.com/c/en/us/support/docs/ip/generic-routing-encapsulation-gre/25885-pmtud-ipfrag.html)
- [TCP 성능 튜닝 팁](https://docs.oracle.com/cd/E19455-01/806-1075/6j9vh8m4u/index.html)