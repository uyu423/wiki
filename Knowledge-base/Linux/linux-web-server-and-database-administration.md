---
title: Linux 웹 서버 및 데이터베이스 관리
description: 
published: true
date: 2023-02-12T11:33:40.973Z
tags: 
editor: markdown
dateCreated: 2023-02-12T11:33:39.237Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Linux Web Server and Database Administration***English** document is available*](/en/Knowledge-base/Linux/linux-web-server-and-database-administration)
{.links-list}


# Linux 웹 서버 및 데이터베이스 관리

이 기사에서는 Linux 웹 서버 및 데이터베이스 관리의 기본 사항을 다룹니다. 가장 일반적인 작업에 대한 개요부터 시작한 다음 각 작업에 대해 자세히 살펴보겠습니다.

## 개요

Linux 웹 서버를 관리할 때 가장 일반적인 작업은 다음과 같습니다.

- 웹 서버 소프트웨어 구성
- 도메인 이름 및 DNS 설정
- 사용자 계정 관리
- 서버 보안
- 백업 및 재해 복구
- 서버 모니터링

아래에서 이러한 각 주제를 자세히 다룰 것입니다.

## 웹 서버 소프트웨어 구성

새 웹 서버를 설정할 때 첫 번째 작업은 웹 서버 소프트웨어를 설치하고 구성하는 것입니다. Linux용으로 가장 널리 사용되는 웹 서버 소프트웨어는 Apache HTTP Server입니다. 다른 인기 있는 웹 서버로는 nginx 및 lighttpd가 있습니다.

웹 서버 소프트웨어는 클라이언트(브라우저)의 요청을 처리하고 적절한 응답(일반적으로 웹 페이지)을 반환하는 역할을 합니다. 또한 CGI 지원, 가상 호스팅 및 암호 보호와 같은 다른 기능도 제공합니다.

웹 서버 소프트웨어의 구성은 일반적으로 ```httpd.conf```라는 텍스트 파일을 통해 이루어집니다. 이 파일은 일반적으로 Debian 및 Ubuntu 시스템의 ```/etc/apache2/``` 디렉토리에 있고 Red Hat 및 CentOS 시스템의 ```/etc/httpd/conf/``` 디렉토리에 있습니다.

```httpd.conf``` 파일에는 서버를 구성하는 데 사용할 수 있는 다양한 지시문이 포함되어 있습니다. 가장 일반적인 지시문은 다음과 같습니다.

- ```ServerRoot```: 이 지시어는 서버의 구성 파일이 있는 디렉토리를 지정합니다.
- ```Listen```: 이 지시어는 서버가 청취해야 하는 포트 번호를 지정합니다. HTTP의 기본 포트는 80입니다.
- ```DocumentRoot```: 이 지시어는 서버의 웹 파일이 있는 디렉토리를 지정합니다. 이것은 보통 ```/var/www/html/``` 디렉토리입니다.
- ```<Directory>```: 이 지시어는 특정 디렉토리에 대한 구성을 지정하는 데 사용됩니다.
- ```<VirtualHost>```: 이 지시어는 가상 호스트를 구성하는 데 사용됩니다. 가상 호스트를 사용하면 동일한 서버에서 여러 웹사이트를 호스팅할 수 있습니다.

Apache HTTP Server에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- Apache HTTP 서버 설명서: https://httpd.apache.org/docs/
- Apache HTTP 서버 자습서: https://httpd.apache.org/docs/2.4/en/tutorial.html

## 도메인 이름 및 DNS 설정

다음 작업은 도메인 이름과 DNS를 설정하는 것입니다. 도메인 이름은 인터넷에서 웹사이트를 식별하는 데 사용됩니다. 일반적으로 ```www.example.com``` 형식입니다.

DNS는 도메인 이름을 IP 주소에 매핑하는 데 사용되는 시스템입니다. 브라우저에 도메인 이름을 입력하면 DNS가 웹사이트를 호스팅하는 서버의 IP 주소를 조회하는 데 사용됩니다.

도메인 이름과 DNS 설정에는 도메인 이름 등록과 DNS 구성의 두 부분이 있습니다.

도메인 이름을 등록하려면 도메인 이름 등록 기관을 찾아야 합니다. 이것은 도메인 이름을 판매하는 회사입니다. 등록 기관을 찾으면 사용 가능한 도메인 이름을 검색하고 구입할 수 있습니다.

도메인 이름을 등록했으면 DNS를 구성해야 합니다. 이것은 ```dig``` 및 ```nslookup``` 명령을 사용하여 수행할 수 있습니다. 자세한 내용은 다음 리소스를 참조하십시오.

- Linux에서 Dig 명령을 사용하는 방법: https://www.howtogeek.com/427654/htg-explains-what-is-dig-and-how-to-use-it/
- Linux에서 NSlookup 명령을 사용하는 방법: https://www.howtogeek.com/427950/htg-explains-what-is-nslookup-and-how-to-use-it/

## 사용자 계정 관리

다음 작업은 사용자 계정을 관리하는 것입니다. Linux 서버에는 시스템 계정과 사용자 계정의 두 가지 유형의 사용자 계정이 있습니다.

시스템 계정은 시스템에서 특정 서비스를 실행하는 데 사용됩니다. 일반적으로 숫자 UID를 가지며 인간 사용자가 사용하기 위한 것이 아닙니다.

사용자 계정은 인간 사용자가 시스템에 로그인하는 데 사용됩니다. 일반적으로 사용자 이름과 암호가 있습니다.

사용자 계정을 관리하려면 ```useradd```, ```usermod``` 및 ```userdel``` 명령을 사용할 수 있습니다. 자세한 내용은 다음 리소스를 참조하십시오.

- Linux VPS에서 사용자 추가 및 삭제 방법: https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-a-linux-vps
- Linux에서 사용자 비밀번호 변경 방법: https://www.digitalocean.com/community/tutorials/how-to-change-a-user-s-password-in-linux

## 서버 보안

다음 작업은 서버 보안입니다. Linux 서버를 보호하는 방법에는 여러 가지가 있지만 가장 일반적인 방법을 다룰 것입니다.

서버를 보호하는 첫 번째 방법은 방화벽을 설치하는 것입니다. 방화벽은 통과하는 트래픽을 필터링하는 소프트웨어 또는 하드웨어 장치입니다. 원치 않는 트래픽을 차단하고 특정 트래픽만 허용하는 데 사용할 수 있습니다.

Linux용 가장 일반적인 방화벽 소프트웨어는 iptables입니다. 널리 사용되는 다른 방화벽에는 firewalld 및 ufw가 있습니다.

서버를 보호하는 두 번째 방법은 통신을 암호화하는 것입니다. 이를 수행하는 가장 일반적인 방법은 SSL/TLS를 사용하는 것입니다. SSL/TLS는 서버와 클라이언트 간의 통신을 암호화하는 데 사용되는 프로토콜입니다.

통신을 암호화하려면 인증서를 생성해야 합니다. 인증서는 서버 및 암호화 키에 대한 정보가 포함된 파일입니다. 그런 다음 인증서는 서버와 클라이언트에서 통신을 암호화하고 해독하는 데 사용됩니다.

인증서를 생성하려면 ```openssl``` 명령을 사용할 수 있습니다. 자세한 내용은 다음 리소스를 참조하십시오.

- Apache에서 SSL/TLS 인증서를 설치하는 방법: https://www.digitalocean.com/community/tutorials/how-to-install-an-ssl-certificate-from-a-commercial-certificate-authority
- CentOS 7에서 Apache용 자체 서명 SSL 인증서를 생성하는 방법: https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache- in-centos-7

서버를 보호하는 세 번째 방법은 보안 스캐너를 사용하는 것입니다. 보안 스캐너는 시스템의 보안 취약성을 스캔하는 데 사용되는 도구입니다. Linux용으로 가장 널리 사용되는 보안 스캐너는 Nessus입니다.

Linux 서버 보안에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- 방화벽 규칙으로 서버를 보호하는 방법: https://www.digitalocean.com/community/tutorials/how-to-secure-a-server-with-firewall-rules-ufw
- Ubuntu 및 Debian 클라우드 서버에서 UFW로 방화벽을 설정하는 방법: https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-an -ubuntu-and-debian-cloud-server
- Ubuntu VPS에서 SSH를 강화하는 방법: https://www.digitalocean.com/community/tutorials/how-to-harden-ssh-on-an-ubuntu-vps

## 백업 및 재해 복구

다음 작업은 백업 및 재해 복구 계획을 설정하는 것입니다. 이를 수행하는 방법에는 여러 가지가 있지만 가장 일반적인 방법을 다룰 것입니다.

백업을 설정하는 첫 번째 방법은 ```rsync```라는 도구를 사용하는 것입니다. ```rsync```는 한 위치에서 다른 위치로 파일을 복사하는 데 사용할 수 있는 도구입니다. 파일 및 디렉터리의 백업을 만드는 데 사용할 수 있습니다.

백업을 설정하는 두 번째 방법은 ```tar```라는 도구를 사용하는 것입니다. ```tar```는 파일 및 디렉토리의 아카이브를 만드는 데 사용할 수 있는 도구입니다. 아카이브는 파일을 압축하고 백업하는 데 사용할 수 있습니다.

백업을 설정하는 세 번째 방법은 ```dd```라는 도구를 사용하는 것입니다. ```dd```는 디스크 이미지를 만드는 데 사용할 수 있는 도구입니다. 디스크 이미지는 전체 파티션 또는 디스크를 백업하는 데 사용할 수 있습니다.

Linux 서버 백업에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- ```rsync```를 사용하여 서버 파일을 백업하는 방법: https://www.digitalocean.com/community/tutorials/how-to-backup-your-server-files-using-rsync
- ```tar```를 사용하여 서버를 백업하는 방법: https://www.digitalocean.com/community/tutorials/how-to-backup-your-server-using-tar
- ```dd```를 사용하여 서버를 백업하는 방법: https://www.digitalocean.com/community/tutorials/how-to-backup-your-server-using-dd

백업 및 재해 복구 계획 설정의 두 번째 부분은 재해 복구 계획을 만드는 것입니다. 이 계획은 서버 오류와 같은 주요 재해로부터 복구하는 방법을 간략하게 설명해야 합니다.

재해 복구 계획을 만드는 첫 번째 단계는 시스템의 중요한 구성 요소를 식별하는 것입니다. 여기에는 웹 서버 소프트웨어, 데이터베이스 소프트웨어 및 데이터가 포함됩니다.

두 번째 단계는 사용할 백업 방법을 식별하는 것입니다. 여기에는 백업을 만드는 데 사용할 도구, 백업 빈도 및 백업 위치가 포함됩니다.

세 번째 단계는 사용할 복구 방법을 식별하는 것입니다. 여기에는 백업을 복원하는 데 사용할 도구, 구성 요소가 복구되는 순서 및 백업 위치가 포함됩니다.

재해 복구 계획 생성에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- 웹사이트 재해 복구 계획을 만드는 방법: https://www.digitalocean.com/community/tutorials/how-to-create-a-website-disaster-recovery-plan
- 서버 마이그레이션 준비 방법: https://www.digitalocean.com/community/tutorials/how-to-prepare-for-a-server-migration

## 서버 모니터링

마지막 작업은 서버를 모니터링하는 것입니다. 여기에는 CPU, 메모리 및 디스크 사용량과 같은 서버 리소스 모니터링과 웹 서버 및 데이터베이스 서버와 같은 서버 서비스 모니터링이 포함됩니다.

서버를 모니터링하는 데 사용할 수 있는 많은 도구가 있습니다. 가장 많이 사용되는 도구는 다음과 같습니다.

- 맨 위
-htop
- 아이오톱
- vmstat
- netstat

Linux 서버 모니터링에 대한 자세한 내용은 다음 리소스를 참조하십시오.

- Ubuntu 16.04에서 ```netdata```로 시스템 메트릭을 모니터링하는 방법: https://www.digitalocean.com/community/tutorials/how-to-monitor-system-metrics-with-netdata-on-ubuntu- 16-04
- Ubuntu 16.04에서 ```glances```로 서버 리소스를 모니터링하는 방법: https://www.digitalocean.com/community/tutorials/how-to-monitor-your-server-resources-with-glances-on -우분투-16-04

## 외부 리소스

- https://www.digitalocean.com/community/tutorials/an-overview-of-linux-web-server-administration
- https://www.digitalocean.com/community/tutorials/an-overview-of-linux-server-administration
- https://www.digitalocean.com/community/tutorials/an-overview-of-linux-database-administration