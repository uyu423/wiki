---
title: Linux를 사용한 시스템 관리
description: 
published: true
date: 2023-02-11T11:32:22.328Z
tags: 
editor: markdown
dateCreated: 2023-02-11T11:32:20.716Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [System Administration with Linux***English** document is available*](/en/Knowledge-base/Linux/system-administration-with-linux)
{.links-list}


# 리눅스를 이용한 시스템 관리

시스템 관리는 컴퓨터 시스템을 관리하는 프로세스입니다. 일반적으로 시스템 관리에는 소프트웨어 설치, 하드웨어 구성 및 사용자 계정 관리와 같은 작업이 포함됩니다.

루트 사용자와 같이 적절한 권한이 있는 사용자가 시스템 관리를 수행할 수 있습니다. 그러나 실제로는 전담 관리자 팀이 시스템 관리를 수행하는 경우가 많습니다.

## 소프트웨어 설치

시스템 관리자의 가장 일반적인 작업 중 하나는 소프트웨어를 설치하는 것입니다. 이것은 apt와 같은 패키지 관리자를 사용하여 수행할 수 있습니다.

Apt는 소프트웨어를 설치, 업데이트 및 제거하는 데 사용할 수 있는 명령줄 도구입니다. Debian 및 Ubuntu의 기본 패키지 관리자입니다.

apt를 사용하여 패키지를 설치하려면 관리자는 다음 명령을 사용할 수 있습니다.

```
sudo apt install {package_name}
```

## 하드웨어 구성

시스템 관리자의 또 다른 일반적인 작업은 하드웨어를 구성하는 것입니다. 이는 하드웨어 관리 도구인 hw-config를 사용하여 수행할 수 있습니다.

Hw-config는 하드웨어 장치를 구성하는 데 사용할 수 있는 명령줄 도구입니다. 사운드 카드, 네트워크 카드 및 프린터 대기열과 같은 장치를 구성하는 데 사용할 수 있습니다.

hw-config를 사용하여 장치를 구성하기 위해 관리자는 다음 명령을 사용할 수 있습니다.

```
sudo hw-config {device_name}
```

## 사용자 계정 관리

시스템 관리자의 또 다른 일반적인 작업은 사용자 계정을 관리하는 것입니다. 이는 사용자 관리 도구인 usermod를 사용하여 수행할 수 있습니다.

Usermod는 사용자 계정을 추가, 수정 및 삭제하는 데 사용할 수 있는 명령줄 도구입니다. 사용자 계정의 암호를 변경하는 데에도 사용할 수 있습니다.

usermod를 사용하여 사용자를 추가하려면 관리자는 다음 명령을 사용할 수 있습니다.

```
sudo usermod -a -G {group_name} {username}
```

usermod를 사용하여 사용자의 암호를 변경하려면 관리자는 다음 명령을 사용할 수 있습니다.

```
sudo usermod -p {new_password} {username}
```

## 외부 리소스

시스템 관리에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- [시스템 관리 가이드](https://www.tldp.org/LDP/sag/html/)
- [데비안 관리 가이드](https://debian-handbook.info/browse/stable/)
- [우분투 서버 가이드](https://help.ubuntu.com/lts/serverguide/index.html)