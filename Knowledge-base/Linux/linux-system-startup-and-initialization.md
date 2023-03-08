---
title: Linux 시스템 시작 및 초기화
description: 
published: true
date: 2023-02-11T04:55:12.919Z
tags: 
editor: markdown
dateCreated: 2023-02-11T04:55:11.367Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Linux System Startup and Initialization***English** document is available*](/en/Knowledge-base/Linux/linux-system-startup-and-initialization)
{.links-list}


# Linux 시스템 시작 및 초기화

Linux 시스템이 부팅될 때마다 시스템을 초기화하기 위해 여러 프로세스가 시작됩니다. 이 프로세스를 시스템 시작 또는 초기화라고 하며 일반적으로 다음 순서로 발생합니다.

1. ** 바이오스 **
2. ** 마스터 부트 레코드(MBR)**
3. ** 부트로더 **
4. ** 커널 **
5. ** 초기화 프로세스 **
6. ** 사용자 공간 **

## 바이오스

BIOS(Basic Input/Output System)는 컴퓨터를 켤 때 가장 먼저 실행되는 것입니다. 부트 로더가 포함된 하드 드라이브의 부트 섹터를 읽어 컴퓨터를 부팅하는 역할을 합니다.

## 마스터 부트 레코드(MBR)

MBR은 부트로더 로딩을 담당하는 작은 코드 조각입니다. 일반적으로 하드 드라이브의 첫 번째 섹터에 있습니다.

## 부트로더

부트 로더는 운영 체제 커널을 로드하는 프로그램입니다. Linux 시스템에서 사용되는 가장 일반적인 부트로더는 GRUB(Grand Unified Bootloader)입니다.

## 커널

커널은 운영 체제의 핵심이며 메모리, 장치 및 프로세스와 같은 시스템 리소스 관리를 담당합니다.

## 초기화 프로세스

init 프로세스는 커널이 시작하는 첫 번째 프로세스입니다. 시스템의 다른 모든 프로세스 시작을 담당합니다.

## 사용자 공간

init 프로세스가 다른 모든 필수 프로세스를 시작한 후 시스템은 사용자 공간에 있다고 합니다. 일반 사용자가 로그인하여 프로그램을 실행할 수 있는 곳입니다.