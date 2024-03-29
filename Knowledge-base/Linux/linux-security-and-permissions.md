---
title: Linux 보안 및 권한
description: 
published: true
date: 2023-02-11T20:32:36.500Z
tags: 
editor: markdown
dateCreated: 2023-02-11T20:32:29.517Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Linux Security and Permissions***English** document is available*](/en/Knowledge-base/Linux/linux-security-and-permissions)
{.links-list}


# 리눅스 보안 및 권한

Linux의 가장 큰 장점 중 하나는 보안입니다. Linux는 기본적으로 매우 안전하지만 더 안전하게 만들 수 있는 방법이 여전히 있습니다. 이 기사에서는 Linux 시스템의 보안을 향상시킬 수 있는 몇 가지 방법을 살펴보겠습니다.

## 파일 권한

보안의 가장 중요한 측면 중 하나는 파일 권한입니다. 파일 권한은 파일을 읽고 쓰고 실행할 수 있는 사람을 결정합니다. 기본적으로 파일 소유자만 파일을 읽고 쓰고 실행할 수 있습니다. 다른 사람은 읽고 실행할 수만 있습니다.

파일의 권한을 보려면 `-l` 옵션과 함께 `ls` 명령을 사용하십시오.

    $ ls -l
    -rw-r--r-- 1 존 존 0 4월 25일 18:42 file1

첫 번째 열은 파일의 권한을 보여줍니다. 다음 열에는 파일 소유자가 표시됩니다. 세 번째 열에는 파일이 속한 그룹이 표시됩니다. 네 번째 열은 파일 크기를 바이트 단위로 보여줍니다. 다섯 번째 열에는 파일이 마지막으로 수정된 날짜와 시간이 표시됩니다. 여섯 번째 열에는 파일 이름이 표시됩니다.

권한은 일련의 문자로 표시됩니다. 첫 번째 문자는 일반 파일의 경우 `-`, 디렉토리의 경우 `d`, 심볼릭 링크의 경우 `l`입니다. 다음 9개의 문자는 3개씩 3개의 그룹으로 나뉩니다. 첫 번째 그룹은 소유자의 권한, 두 번째 그룹은 그룹의 권한, 세 번째 그룹은 다른 사람의 권한입니다.

세 문자로 구성된 각 그룹은 읽기를 위한 `r`, 쓰기를 위한 `w`, 실행을 위한 `x` 또는 권한이 없는 경우 `-`로 구성됩니다. 예를 들어 'rwxr-xr-x' 권한은 소유자가 파일을 읽고 쓰고 실행할 수 있음을 의미합니다. 그룹은 파일을 읽고 실행할 수 있습니다. 다른 사람들은 파일을 읽고 실행할 수 있습니다.

파일의 권한을 변경하려면 `chmod` 명령을 사용하십시오. 예를 들어 소유자에게 읽기, 쓰기 및 실행 권한을 부여하고 그룹 및 다른 사용자에게 읽기 및 실행 권한을 부여하려면 다음 명령을 사용합니다.

    $ chmod 755 파일1

`chmod` 명령을 사용하여 파일의 소유자와 그룹을 변경할 수도 있습니다. 예를 들어 파일 소유자를 `john`으로, 그룹을 `users`로 변경하려면 다음 명령을 사용합니다.

    $ chmod u+rwx,g+rwx,o+rwx 파일1

## 사용자 계정

보안의 또 다른 중요한 측면은 사용자 계정입니다. 기본적으로 Linux 시스템에는 루트 사용자와 몇 명의 다른 기본 사용자가 있습니다. 루트 사용자는 시스템에 대한 전체 액세스 권한을 가지며 무엇이든 할 수 있습니다. 다른 사용자는 제한된 액세스 권한을 가지며 특정 작업만 수행할 수 있습니다.

시스템을 사용하는 사람마다 별도의 사용자 계정을 만드는 것이 좋습니다. 이렇게 하면 한 사람의 계정이 손상되더라도 다른 계정은 여전히 안전합니다.

사용자 계정을 생성하려면 `adduser` 명령을 사용하십시오. 예를 들어 `john`에 대한 사용자 계정을 만들려면 다음 명령을 사용합니다.

    $ adduser 존

사용자에게 루트 권한으로 명령을 실행할 수 있는 sudo 액세스 권한을 부여하려면 `usermod` 명령을 사용하십시오. 예를 들어 `john` sudo 액세스 권한을 부여하려면 다음 명령을 사용합니다.

    $ usermod -aG sudo 존

## 방화벽

Linux 시스템의 보안을 향상시키는 또 다른 방법은 방화벽을 설치하는 것입니다. 방화벽은 네트워크에서 들어오고 나가는 트래픽을 제어하는 프로그램입니다.

Linux 시스템에는 `iptables`라는 내장 방화벽이 있습니다. `iptables`를 설치하려면 `apt-get` 명령을 사용하십시오.

    $ sudo apt-get 설치 iptables

`iptables`를 구성하려면 `/etc/iptables.conf` 파일을 편집하십시오. 예를 들어 포트 80(HTTP용)에서 들어오는 트래픽을 허용하려면 `/etc/iptables.conf` 파일에 다음 줄을 추가합니다.

    -A 입력 -p tcp --dport 80 -j 수락

변경 사항을 저장하려면 `iptables-save` 명령을 사용하십시오.

    $ sudo iptables-저장

## 결론

이 기사에서는 Linux 시스템의 보안을 향상시킬 수 있는 몇 가지 방법을 살펴보았습니다. 기본적으로 Linux는 매우 안전하지만 더 안전하게 만들 수 있는 방법이 여전히 있습니다. 이 기사에서 설명하는 기술을 사용하여 Linux 시스템을 더욱 안전하게 만들 수 있습니다.