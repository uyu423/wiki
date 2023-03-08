---
title: Linux 네트워킹 및 방화벽 구성
description: 
published: true
date: 2023-02-11T23:32:29.218Z
tags: 
editor: markdown
dateCreated: 2023-02-11T23:32:27.473Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Linux Networking and Firewall Configuration***English** document is available*](/en/Knowledge-base/Linux/linux-networking-and-firewall-configuration)
{.links-list}


# Linux 네트워킹 및 방화벽 구성

대다수의 위협이 인터넷에서 오기 때문에 좋은 방화벽 구성은 모든 Linux 서버에 매우 중요합니다. 이 가이드는 널리 사용되는 iptables 도구를 사용하여 방화벽을 구성하는 기본 사항을 소개합니다.

## 목차

- [방화벽이란?](# what-is-a-firewall)
- [iptables](# iptables)
  - [iptables 설치하기](# installing-iptables)
  - [iptables 설정하기](# configuring-iptables)
- [결론](# 결론)
- [자원](# resources)

## 방화벽이란?

컴퓨팅에서 방화벽은 미리 정해진 보안 규칙에 따라 들어오고 나가는 네트워크 트래픽을 모니터링하고 제어하는 네트워크 보안 시스템입니다. 방화벽은 일반적으로 신뢰할 수 있는 내부 네트워크와 신뢰할 수 없는 외부 네트워크(예: 인터넷) 사이에 장벽을 설정합니다.

## iptables

Iptables는 대부분의 Linux 배포판에 포함된 널리 사용되는 방화벽 도구입니다. 일련의 규칙을 사용하여 허용하거나 차단할 트래픽을 결정합니다.

### iptables 설치

Iptables는 대부분의 Linux 배포판에 포함되어 있으며 패키지 관리자와 함께 설치할 수 있습니다. 예를 들어 데비안 기반 시스템에서:

```
$ sudo apt-get install iptables
```

### iptables 구성

Iptables는 일련의 체인을 사용하여 패킷으로 수행할 작업을 결정합니다. 패킷을 삭제, 거부 또는 수락할 수 있습니다. 기본 체인은 `INPUT`, `FORWARD` 및 `OUTPUT`입니다.

#### 규칙

iptables의 규칙은 여러 일치 기준과 대상으로 구성됩니다. 일치 기준은 프로토콜(예: TCP, UDP), 소스 및 대상 IP 주소, 소스 및 대상 포트 번호와 같은 것일 수 있습니다. 대상은 `DROP`, `REJECT` 또는 `ACCEPT`일 수 있습니다.

##### 규칙 추가

규칙은 `iptables` 명령으로 추가할 수 있습니다. 예를 들어 들어오는 모든 트래픽을 삭제하려면 다음을 수행합니다.

```
$ iptables -A INPUT -j DROP
```

이 규칙은 `INPUT` 체인에 추가되고 패킷을 삭제하는 `DROP` 대상을 갖게 됩니다.

##### 규칙 삭제

규칙은 `iptables` 명령으로 삭제할 수 있습니다. 예를 들어 이전 규칙을 삭제하려면 다음과 같이 하십시오.

```
$ iptables -D INPUT 1
```

이렇게 하면 `INPUT` 체인의 첫 번째 규칙이 삭제됩니다.

##### 규칙 저장

규칙은 `iptables-save` 명령으로 저장할 수 있습니다. 예를 들어:

```
$ iptables-save > /etc/iptables.rules
```

그러면 `/etc/iptables.rules` 파일에 규칙이 저장됩니다.

##### 규칙 로드 중

규칙은 `iptables-restore` 명령으로 로드할 수 있습니다. 예를 들어:

```
$ iptables-restore < /etc/iptables.rules
```

그러면 `/etc/iptables.rules` 파일에서 규칙이 로드됩니다.

## 결론

이 안내서는 iptables로 방화벽을 구성하는 기본 사항을 소개했습니다. 자세한 내용은 아래 리소스를 참조하세요.

## 자원

- [Iptables 튜토리얼](https://www.digitalocean.com/community/tutorials/a-deep-dive-into-iptables-and-netfilter-architecture)
- [Ubuntu 및 Debian 클라우드 서버에서 UFW로 방화벽을 설정하는 방법](https://www.digitalocean.com/community/tutorials/how-to-setup-a-firewall-with-ufw-on-an- 우분투 및 데비안 클라우드 서버)
- [CentOS 7에서 CSF 방화벽으로 서버를 보호하는 방법](https://www.digitalocean.com/community/tutorials/how-to-secure-your-server-with-csf-firewall-on-centos-7 )