---
title: Linux 커널 모듈 및 로드 가능한 커널 개체
description: 
published: true
date: 2023-02-11T16:32:20.415Z
tags: 
editor: markdown
dateCreated: 2023-02-11T16:32:18.723Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Linux Kernel Modules and Loadable Kernel Objects***English** document is available*](/en/Knowledge-base/Linux/linux-kernel-modules-and-loadable-kernel-objects)
{.links-list}


# 리눅스 커널 모듈과 적재 가능한 커널 객체

## 개요

Linux 커널 모듈은 커널을 다시 컴파일하지 않고 런타임에 커널에 로드할 수 있는 개체 코드 조각입니다.

로드 가능한 커널 모듈은 커널을 다시 컴파일하거나 시스템을 재부팅할 필요 없이 커널의 기능을 확장하는 메커니즘을 제공합니다.

 커널 모듈은 장치 드라이버, 파일 시스템 및 기타 기능을 커널에 추가하는 데 사용할 수 있습니다.

## 커널 모듈의 종류

커널 모듈에는 두 가지 유형이 있습니다.

1. **로드 가능한 커널 모듈**: 필요에 따라 커널에서 로드 및 언로드할 수 있는 모듈입니다.
2. **정적으로 컴파일된 커널 모듈**: 커널 자체로 컴파일되는 모듈입니다.

## 적재 가능한 커널 모듈의 장점

로드 가능한 커널 모듈은 정적으로 컴파일된 커널 모듈에 비해 여러 가지 장점이 있습니다.

1. 시스템을 재부팅할 필요 없이 필요에 따라 커널에서 로드 및 언로드할 수 있습니다.
2. 커널을 다시 컴파일할 필요 없이 커널에서 기능을 추가하거나 제거하는 데 사용할 수 있습니다.
3. 커널을 재컴파일하거나 시스템을 재부팅할 필요 없이 커널의 기능을 확장할 수 있는 메커니즘을 제공합니다.

## 적재 가능한 커널 모듈의 단점

로드 가능한 커널 모듈에는 정적으로 컴파일된 커널 모듈에 비해 여러 가지 단점이 있습니다.

1. 적절하게 설계 및 구현되지 않은 경우 보안 취약성을 도입할 수 있습니다.
2. 디버그 및 문제 해결이 어려울 수 있습니다.
3. 유지 관리 및 업데이트가 어려울 수 있습니다.

## 커널 모듈 로딩 및 언로딩

커널 모듈은 `insmod` 명령을 사용하여 커널에 로드하고 `rmmod` 명령을 사용하여 커널에서 언로드할 수 있습니다.

`insmod` 명령은 커널 모듈의 이름을 인수로 받아 커널에 로드합니다. `rmmod` 명령은 커널 모듈의 이름을 인수로 받아 커널에서 제거합니다.

## 커널 모듈 생성

커널 모듈은 커널을 다시 컴파일하지 않고 런타임에 커널에 로드할 수 있는 개체 코드 조각입니다. 커널 모듈은 일반적으로 C 프로그래밍 언어로 작성됩니다.

커널 모듈은 `-DMODULE` 컴파일러 플래그로 컴파일해야 합니다. 이 플래그는 코드가 커널 모듈로 컴파일되고 있음을 컴파일러에 알립니다.

커널 모듈은 `-fPIC` 컴파일러 플래그로 컴파일해야 합니다. 이 플래그는 위치 독립적인 코드를 생성하도록 컴파일러에 지시합니다. 위치 독립적 코드는 모든 주소에서 메모리에 로드되고 실행될 수 있습니다.

`-DMODULE` 및 `-fPIC` 컴파일러 플래그는 `CFLAGS` 환경 변수를 사용하여 컴파일러에 전달할 수 있습니다.

```
$ export CFLAGS=-DMODULE -fPIC
```

`CFLAGS` 환경 변수가 설정되면 `make` 명령을 사용하여 커널 모듈을 컴파일할 수 있습니다.

```
$ make
```

## 커널 모듈 로드

커널 모듈은 `insmod` 명령을 사용하여 커널에 로드할 수 있습니다. `insmod` 명령은 커널 모듈의 이름을 인수로 받아 커널에 로드합니다.

```
$ insmod hello.ko
```

## 커널 모듈 언로드

커널 모듈은 `rmmod` 명령을 사용하여 커널에서 언로드할 수 있습니다. `rmmod` 명령은 커널 모듈의 이름을 인수로 받아 커널에서 제거합니다.

```
$ rmmod hello
```

## 참조

https://www.kernel.org/doc/Documentation/kmod/modules.txt
https://www.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.kernel/loadable_kernel_modules.htm
https://www.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.kernel/creating_kernel_modules.htm
https://www.ibm.com/support/knowledgecenter/ssw_aix_71/com.ibm.aix.kernel/loading_unloading_kernel_modules.htm