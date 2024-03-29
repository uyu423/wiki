---
title: KVM 및 libvirt를 사용한 Linux 가상화
description: 
published: true
date: 2023-02-12T04:32:38.061Z
tags: 
editor: markdown
dateCreated: 2023-02-12T04:32:36.471Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Linux Virtualization with KVM and libvirt***English** document is available*](/en/Knowledge-base/Linux/linux-virtualization-with-kvm-and-libvirt)
{.links-list}


# KVM 및 libvirt를 사용한 Linux 가상화

## 소개

가상화는 운영 체제, 서버, 저장 장치 또는 네트워크 리소스와 같은 항목의 가상 버전을 생성하는 프로세스입니다. 여러 서버를 하나의 물리적 서버로 통합하고 테스트 및 개발 환경을 만드는 등 다양한 용도로 사용할 수 있는 강력한 기술입니다.

Linux는 오랫동안 다양한 가상화 기술을 사용할 수 있는 가상화 분야의 리더였습니다. 이 기사에서는 가장 인기 있는 두 가지인 KVM과 libvirt에 초점을 맞출 것입니다.

## KVM이란 무엇입니까?

KVM(Kernel-based Virtual Machine)은 버전 2.6.20부터 메인라인 Linux 커널에 포함된 Linux용 전체 가상화 솔루션입니다. KVM을 사용하려면 CPU에 Intel VT-x 또는 AMD-V와 같은 하드웨어 가상화 확장이 있어야 합니다.

KVM은 Linux 커널 위에서 실행되고 하드웨어 가상화 확장을 사용하여 가상화 기능을 제공하는 하이퍼바이저입니다. KVM은 메인라인 Linux 커널에 포함되어 있으며 많은 Linux 배포판에서 기본 가상화 솔루션으로 사용됩니다.

## libvirt가 무엇인가요?

libvirt는 KVM, Xen 등과 같은 가상화 플랫폼을 관리하기 위한 통합 API를 제공하는 툴킷입니다. virt-manager와 같은 많은 가상화 관리 도구에서 사용되며 명령줄 도구로도 사용할 수 있습니다.

libvirt는 스토리지 및 네트워킹과 같은 가상 머신 및 기타 가상화 리소스를 관리하기 위한 강력하고 사용하기 쉬운 API를 제공합니다. 명령줄 도구 및 다른 프로그램에서 사용할 수 있는 라이브러리로 사용할 수 있습니다.

## KVM 및 libvirt 시작하기

KVM 및 libvirt를 사용하려면 하드웨어 가상화 확장 기능이 있는 Linux 시스템과 최신 버전의 Linux 커널이 필요합니다. KVM은 메인라인 Linux 커널에 포함되어 있으므로 최신 버전의 배포판 커널을 사용하는 경우 문제가 발생하지 않습니다.

하드웨어 가상화 확장 및 최신 커널이 있는 Linux 시스템이 있으면 배포판의 패키지 관리자를 사용하여 KVM 및 libvirt를 설치할 수 있습니다. 예를 들어 Debian 및 Ubuntu 시스템에서는 다음 명령을 사용하여 설치할 수 있습니다.

```
sudo apt-get install kvm libvirt-bin
```

KVM 및 libvirt가 설치되면 virt-manager 도구를 사용하여 가상 머신을 관리할 수 있습니다. virt-manager는 가상 머신을 쉽게 만들고 관리할 수 있게 해주는 그래픽 도구입니다.

## 가상 머신 생성

 virt-manager는 가상 머신을 관리하기 위한 그래픽 도구입니다. 시작하려면 다음 명령을 입력하십시오.

```
virt-manager
```

그림 1에 표시된 virt-manager 창이 표시됩니다.


그림 1. virt-manager 창

새 가상 머신을 생성하려면 파일 메뉴를 클릭하고 새 가상 머신을 선택합니다. 그림 2에 표시된 새 VM 마법사 창이 표시됩니다.


그림 2. 새 VM 마법사 창

마법사의 첫 번째 페이지에서 로컬 설치 미디어 옵션을 선택하고 앞으로를 클릭합니다. 다음 페이지에서 ISO 이미지 옵션을 선택하고 전달을 클릭합니다. 다음 페이지에서 찾아보기 버튼을 선택하고 ISO 이미지의 위치를 찾습니다. 그런 다음 앞으로 버튼을 선택합니다.

다음 페이지에 사용 가능한 운영 체제 목록이 표시됩니다. 설치할 운영 체제를 선택하고 앞으로를 클릭하십시오. 다음 페이지에서 가상 머신의 이름을 입력하고 전달을 클릭합니다.

다음 페이지에 사용 가능한 저장 장치 목록이 표시됩니다. 사용하려는 저장 장치를 선택하고 전달을 클릭합니다. 다음 페이지에 사용 가능한 네트워크 장치 목록이 표시됩니다. 사용하려는 네트워크 장치를 선택하고 전달을 클릭합니다.

다음 페이지에는 사용 가능한 CPU 모델 목록이 표시됩니다. 사용하려는 CPU 모델을 선택하고 앞으로를 클릭합니다. 다음 페이지에 사용 가능한 메모리 크기 목록이 표시됩니다. 사용할 메모리 크기를 선택하고 앞으로를 클릭합니다.

다음 페이지에 사용 가능한 비디오 장치 목록이 표시됩니다. 사용하려는 비디오 장치를 선택하고 전달을 클릭합니다. 마지막 페이지에서 선택 사항을 검토하고 마침을 클릭합니다.

virt-manager 도구는 이제 가상 머신을 생성하고 선택한 ISO 이미지에서 부팅합니다. 가상 머신은 일시 중지 상태이므로 시작하려면 재개 버튼을 클릭해야 합니다.

## 가상 머신에 연결

가상 머신이 실행되면 virt-manager 도구를 사용하여 연결할 수 있습니다. 이렇게 하려면 virt-manager 창에서 가상 머신을 선택하고 연결 버튼을 클릭합니다. 그림 3에 표시된 VM에 연결 창이 표시됩니다.


그림 3. VM에 연결 창

마법사의 첫 번째 페이지에서 VNC 옵션을 선택하고 앞으로를 클릭합니다. 다음 페이지에 사용 가능한 VNC 뷰어 목록이 표시됩니다. 사용할 뷰어를 선택하고 앞으로를 클릭합니다. 마지막 페이지에서 선택 사항을 검토하고 마침을 클릭합니다.

virt-manager 도구는 이제 VNC 뷰어를 시작하고 가상 머신에 연결합니다. 가상 머신의 로그인 화면이 표시됩니다.

## virsh로 가상 머신 관리

virt-manager 도구 외에도 virsh 도구를 사용하여 가상 머신을 관리할 수도 있습니다. virsh는 가상 머신을 관리하기 위한 강력한 명령 집합을 제공하는 명령줄 도구입니다.

사용 가능한 모든 virsh 명령을 나열하려면 다음 명령을 입력하십시오.

```
virsh
```

특정 virsh 명령에 대한 도움말을 보려면 다음 명령을 입력하십시오.

```
virsh help {command}
```

사용 가능한 모든 가상 머신을 나열하려면 다음 명령을 입력하십시오.

```
virsh list
```

특정 가상 머신에 대한 정보를 얻으려면 다음 명령을 입력하십시오.

```
virsh dominfo {domain}
```

가상 머신을 시작하려면 다음 명령을 입력하십시오.

```
virsh start {domain}
```

가상 머신을 종료하려면 다음 명령을 입력하십시오.

```
virsh shutdown {domain}
```

가상 머신을 제거하려면 다음 명령을 입력하십시오.

```
virsh destroy {domain}
```

가상 머신을 일시 중단하려면 다음 명령을 입력하십시오.

```
virsh suspend {domain}
```

가상 머신을 재개하려면 다음 명령을 입력하십시오.

```
virsh resume {domain}
```

가상 머신에 연결하려면 다음 명령을 입력하십시오.

```
virsh console {domain}
```

## virt-manager로 스토리지 관리

가상 머신 관리 외에도 virt-manager 도구를 사용하여 스토리지를 관리할 수도 있습니다. 스토리지 관리자를 실행하려면 다음 명령을 입력하십시오.

```
virt-manager --storage
```

그림 4에 표시된 virt-manager Storage 창이 표시됩니다.


그림 4. virt-manager 스토리지 창

새 스토리지 풀을 생성하려면 파일 메뉴를 클릭하고 새 스토리지 풀을 선택합니다. 그림 5와 같이 New Storage Pool 창이 나타납니다.


그림 5. 새 스토리지 풀 창

마법사의 첫 번째 페이지에서 생성하려는 스토리지 풀 유형을 선택하고 Forward를 클릭합니다. 다음 페이지에서 스토리지 풀의 소스를 선택하고 Forward를 클릭합니다. 다음 페이지에서 스토리지 풀의 대상을 선택하고 Forward를 클릭합니다.

다음 페이지에 사용 가능한 저장 장치 목록이 표시됩니다. 사용할 저장 장치를 선택하고 전달을 클릭합니다. 다음 페이지에 사용 가능한 저장 형식 목록이 표시됩니다. 사용할 저장 형식을 선택하고 전달을 클릭합니다.

다음 페이지에 사용 가능한 할당 전략 목록이 표시됩니다. 사용할 할당 전략을 선택하고 전달을 클릭합니다. 다음 페이지에 사용 가능한 캐시 모드 목록이 표시됩니다. 사용하려는 캐시 모드를 선택하고 전달을 클릭합니다.

다음 페이지에서 사용 가능한 I/O 스케줄러 목록을 볼 수 있습니다. 사용할 I/O 스케줄러를 선택하고 Forward를 클릭하십시오. 다음 페이지에 사용 가능한 블록 크기 목록이 표시됩니다. 사용할 블록 크기를 선택하고 전달을 클릭합니다.

마지막 페이지에서 선택 사항을 검토하고 마침을 클릭합니다. 이제 virt-manager 도구가 스토리지 풀을 생성합니다.

## 결론

이 기사에서는 KVM 및 libvirt를 사용한 Linux 가상화의 기본 사항을 다루었습니다. KVM 및 libvirt 설치 방법, 가상 머신 생성 및 관리 방법, 스토리지 관리 방법을 살펴보았습니다.

이러한 지식을 바탕으로 KVM 및 libvirt를 사용하여 자체 Linux 환경을 가상화할 수 있어야 합니다.