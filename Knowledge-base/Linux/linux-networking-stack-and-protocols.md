---
title: Linux 네트워킹 스택 및 프로토콜
description: 
published: true
date: 2023-02-11T22:32:16.979Z
tags: 
editor: markdown
dateCreated: 2023-02-11T22:32:15.419Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Linux Networking Stack and Protocols***English** document is available*](/en/Knowledge-base/Linux/linux-networking-stack-and-protocols)
{.links-list}


Linux 네트워킹은 방대하고 복잡한 주제입니다. 이 기사에서는 네트워킹 스택 및 프로토콜에 중점을 둘 것입니다.

## Linux 네트워킹 스택

Linux 네트워킹 스택은 각각 고유한 역할을 수행하는 여러 구성 요소로 구성됩니다.

### 커널

Linux 네트워킹 스택의 핵심은 커널입니다. 커널은 네트워킹 장치를 포함한 모든 하드웨어 리소스 관리를 담당합니다. 또한 TCP/IP와 같은 핵심 네트워킹 프로토콜을 구현합니다.

### 쉘

커널 위에는 쉘이 있습니다. 쉘은 커널과 상호 작용할 수 있는 사용자 인터페이스입니다. 명령을 실행하고 프로그램을 실행하는 방법을 제공합니다.

### 구성 파일

셸은 구성 파일을 사용하여 커널과 그 위에서 실행되는 프로그램의 동작을 제어합니다. 네트워킹을 위한 가장 중요한 구성 파일은 호스트 이름을 IP 주소에 매핑하는 /etc/hosts 파일과 호스트 이름을 확인하는 데 사용할 DNS 서버를 정의하는 /etc/resolv.conf 파일입니다.

### 유틸리티

네트워킹을 구성하고 문제를 해결하는 데 사용되는 많은 유틸리티가 있습니다. 가장 중요한 것 중 일부는 네트워크 인터페이스를 구성하는 데 사용되는 ifconfig와 연결 테스트에 사용되는 ping입니다.

## TCP/IP 프로토콜 스택

TCP/IP 프로토콜 스택은 인터넷의 핵심 기능을 구현하는 데 사용되는 프로토콜 집합입니다. 네 개의 레이어로 구성됩니다.

- 애플리케이션 계층은 애플리케이션이 서로 통신하는 계층입니다.
- 호스트 간의 종단 간 통신을 담당하는 전송 계층.
- 호스트 간의 트래픽 라우팅을 담당하는 네트워크 계층.
- 동일한 네트워크에 있는 호스트 간의 연결을 제공하는 링크 계층.

TCP/IP 스택은 커널에서 구현되며 셸은 구성 및 문제 해결을 위한 유틸리티를 제공합니다.

## 참조

- https://www.tldp.org/LDP/GNU-Linux-Tools-Summary/html/c1022.htm
- https://www.thegeekstuff.com/2012/03/linux-networking-stack/
- https://www.redhat.com/en/blog/introduction-linux-networking-stack-part-1