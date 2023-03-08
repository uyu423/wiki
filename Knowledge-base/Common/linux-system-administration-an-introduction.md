---
title: Linux 시스템 관리: 소개
description: 
published: true
date: 2023-02-25T17:32:32.240Z
tags: 
editor: markdown
dateCreated: 2023-02-25T17:32:30.857Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Linux System Administration: An Introduction***English** document is available*](/en/Knowledge-base/Common/linux-system-administration-an-introduction)
{.links-list}


# Linux 시스템 관리: 소개

Linux는 무료 및 오픈 소스 소프트웨어 개발 및 배포 모델로 조립된 Unix와 유사하고 대부분 POSIX 호환 컴퓨터 운영 체제입니다. 모든 Linux 시스템의 정의 구성 요소는 Linux 커널로, 1991년 10월 5일에 Linus Torvalds가 처음 출시한 운영 체제 커널입니다. 많은 Linux 배포판은 이름에 "Linux"라는 단어를 사용하지만 Free Software Foundation은 전체 운영 체제를 언급할 때 GNU 소프트웨어, 특히 GNU Compiler Collection(GCC)의 중요성을 강조하기 위해 GNU/Linux라는 이름을 사용합니다. , 그들이 무료 운영 체제로 간주하는 것을 만들 때.

## 역사

Linux 커널의 개발은 독점 유닉스 계열 운영 체제인 Minix에 대한 무료 오픈 소스 대안을 만들기 위해 1991년에 시작되었습니다. Linux 커널의 주요 작성자인 Linus Torvalds는 1991년 10월 5일에 Linux 커널 개발을 시작했습니다. 1993년 8월 17일에 그는 Linux 커널의 첫 번째 버전인 버전 0.01을 출시했습니다.

그 이후로 Linux는 많은 운영 체제, 특히 Debian, Ubuntu, Mint, Fedora, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Gentoo Linux, Arch Linux 및 Android의 커널로 채택되었습니다. 라우터, 셋톱 박스, 디지털 비디오 레코더 및 비디오 게임 콘솔과 같은 많은 소비자 장치에도 사용됩니다.

## 특징

Linux는 모놀리식 커널입니다. 즉, 운영 체제의 모든 구성 요소가 단일 실행 파일인 커널에 통합됩니다. 이 디자인의 장점은 사용자 요청과 커널 응답 사이의 대기 시간을 줄여 시스템 성능과 안정성을 향상시킨다는 것입니다.

Linux는 또한 개인용 컴퓨터에서 슈퍼컴퓨터에 이르기까지 광범위한 하드웨어 플랫폼을 지원합니다. 이는 커널이 모든 하드웨어 플랫폼에서 실행되도록 구성할 수 있고 많은 수의 오픈 소스 드라이버를 사용할 수 있기 때문에 가능합니다.

## 배포판

각각 다른 초점을 가진 수백 개의 Linux 배포판이 있습니다. Debian 및 Ubuntu와 같은 일부 배포판은 범용으로 설계된 반면 Fedora 및 Red Hat Enterprise Linux와 같은 다른 배포판은 서버 관리 또는 소프트웨어 개발과 같은 특정 사용 사례를 위해 설계되었습니다.

## 데스크탑 환경

데스크탑 환경은 그래픽 사용자 인터페이스(GUI)와 운영 체제 작업을 위한 일련의 응용 프로그램을 제공하는 소프트웨어 모음입니다. Linux에서 가장 널리 사용되는 데스크톱 환경은 GNOME, KDE 및 Xfce입니다.

## 소프트웨어

Linux 시스템에는 웹 브라우저, 오피스 제품군 및 소프트웨어 개발용 도구 세트를 포함하여 기본적으로 다양한 소프트웨어가 설치되어 있습니다. 또한 온라인 리포지토리에서 설치할 수 있는 수천 개의 응용 프로그램이 있습니다.

## 명령줄

Linux는 텍스트 기반 운영 체제이므로 사용자는 텍스트 명령을 사용하여 시스템과 상호 작용합니다. 명령줄은 Linux 시스템을 관리하기 위한 강력한 도구이며 그래픽 사용자 인터페이스를 사용하여 수행할 수 없는 작업을 수행하기 위해 종종 명령줄을 사용해야 합니다.

## 파일과 디렉토리

Linux는 계층적 파일 시스템을 사용합니다. 즉, 파일은 디렉토리로 구성되고 디렉토리는 다른 디렉토리를 포함할 수 있습니다. 파일 시스템은 맨 위에 루트 디렉토리(/)가 있는 트리로 구성됩니다.

## 사용자 및 그룹

사용자는 Linux 시스템을 사용하는 개인입니다. 각 사용자는 고유한 사용자 ID(UID)를 가지며 하나 이상의 그룹의 구성원입니다. 그룹은 사용자를 구성하고 파일 및 디렉터리와 같은 리소스에 대한 액세스를 제어하는 데 사용됩니다.

## 프로세스

프로세스는 실행 중인 프로그램 인스턴스입니다. 모든 프로세스에는 고유한 프로세스 ID(PID)가 있으며 특정 사용자 및 그룹과 연결됩니다. 프로세스는 운영 체제에 의해 생성되고 종료됩니다.

## 서비스

서비스는 시스템이 부팅될 때 자동으로 시작되어 백그라운드에서 실행되는 프로세스입니다. 서비스는 네트워크 파일 공유 또는 이메일과 같이 사용자 인터페이스와 직접 관련되지 않은 기능을 제공합니다.

## 보안

Linux 시스템은 보안을 유지하도록 설계되었으며 보안 관리를 위한 다양한 도구를 포함합니다. 예를 들어 sudo 명령을 사용하여 사용자에게 루트 권한에 대한 임시 액세스 권한을 부여하고 iptables 명령을 사용하여 방화벽을 구성할 수 있습니다.

## 자원

- https://www.tldp.org/LDP/intro-linux/html/
- https://en.wikipedia.org/wiki/Linux_distribution
- https://www.gnu.org/gnu/linux-and-gnu.en.html
- https://www.linux.com/what-is-linux/
- https://www.redhat.com/en/topics/linux/what-is-linux