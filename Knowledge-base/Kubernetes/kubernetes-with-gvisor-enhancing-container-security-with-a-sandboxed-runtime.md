---
title: Kubernetes with gVisor: 샌드박스 런타임으로 컨테이너 보안 강화
description: 
published: true
date: 2023-02-14T11:33:10.568Z
tags: 
editor: markdown
dateCreated: 2023-02-14T11:33:08.988Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes with gVisor: Enhancing Container Security with a Sandboxed Runtime***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-gvisor-enhancing-container-security-with-a-sandboxed-runtime)
{.links-list}


# Kubernetes with gVisor: 샌드박스 런타임으로 컨테이너 보안 강화

Kubernetes는 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하기 위한 오픈 소스 시스템입니다. gVisor는 커널 기능을 사용하여 프로세스를 격리하고 보안을 개선하는 런타임 샌드박스입니다.

## gVisor란?

gVisor는 커널 기능을 사용하여 프로세스를 격리하고 보안을 개선하는 런타임 샌드박스입니다. 안전한 환경에서 신뢰할 수 없는 코드를 실행하도록 설계되었습니다. gVisor는 Google Cloud Platform에서 사용되며 오픈 소스로 제공됩니다.

gVisor는 Linux 커널 위에서 실행되는 사용자 공간 프로그램입니다. 기본 운영 체제 및 리소스에 대한 제한된 보기를 제공합니다. 이는 악성 프로그램이나 버그가 있는 프로그램으로 인해 발생할 수 있는 손상의 양을 제한합니다.

gVisor는 완전한 가상 머신이 아닙니다. 자체 커널 또는 장치 드라이버를 제공하지 않습니다. 대신 기본 운영 체제의 커널과 드라이버를 사용합니다. 따라서 gVisor는 전체 가상 머신보다 가볍고 사용하기 쉽습니다.

## gVisor는 어떻게 작동하나요?

gVisor는 Linux 커널 기능을 사용하여 프로세스를 격리합니다. 이러한 기능에는 네임스페이스, cgroups 및 seccomp-bpf가 포함됩니다.

네임스페이스는 프로세스 간 격리를 제공합니다. 이를 통해 프로세스는 자체 파일 시스템 및 네트워크를 포함하여 시스템에 대한 자체 보기를 가질 수 있습니다.

Cgroup은 프로세스가 사용할 수 있는 리소스를 제한합니다. 프로세스가 사용할 수 있는 CPU, 메모리 및 디스크 공간의 양을 제한하는 데 사용할 수 있습니다.

Seccomp-bpf는 프로세스를 샌드박스화할 수 있는 보안 기능입니다. 시스템 호출을 필터링하고 위험한 호출을 차단합니다.

## Kubernetes는 gVisor를 어떻게 사용하나요?

Kubernetes는 gVisor를 사용하여 컨테이너의 보안을 개선합니다. 기본적으로 컨테이너는 호스트 운영 체제와 동일한 커널을 공유합니다. 악성 컨테이너가 호스트 운영 체제에 액세스할 수 있기 때문에 이는 보안 위험이 될 수 있습니다.

gVisor는 컨테이너를 위한 샌드박스 런타임을 제공합니다. 이렇게 하면 호스트 운영 체제에서 컨테이너가 분리되고 보안이 향상됩니다.

## Kubernetes를 gVisor와 함께 사용하려면 어떻게 해야 하나요?

`kubelet` 명령에 `--runtime=runsc` 플래그를 추가하여 gVisor와 함께 Kubernetes를 사용할 수 있습니다. 그러면 gVisor가 컨테이너의 런타임으로 사용됩니다.

`kubelet` 명령에 `--runtime-provider=runsc` 플래그를 추가하여 gVisor와 함께 Kubernetes를 사용할 수도 있습니다. 그러면 gVisor가 컨테이너의 런타임 공급자로 사용됩니다.

## gVisor로 쿠버네티스를 어떻게 설치하나요?

`apt` 또는 `yum`과 같은 패키지 관리자를 사용하여 gVisor와 함께 Kubernetes를 설치할 수 있습니다.

```
apt install kubelet=1.10.11-00 runc=1.0.0-rc5-3
```

```
yum install kubelet-1.10.11-0 runc-1.0.0-rc5-3
```

## gVisor로 Kubernetes를 어떻게 업그레이드합니까?

`apt` 또는 `yum`과 같은 패키지 관리자를 사용하여 gVisor로 Kubernetes를 업그레이드할 수 있습니다.

```
apt upgrade kubelet=1.10.11-00 runc=1.0.0-rc5-3
```

```
yum upgrade kubelet-1.10.11-0 runc-1.0.0-rc5-3
```

## gVisor로 Kubernetes를 구성하려면 어떻게 해야 하나요?

`kubelet` 명령에 `--runtime=runsc` 플래그를 추가하여 gVisor로 Kubernetes를 구성할 수 있습니다. 그러면 gVisor가 컨테이너의 런타임으로 사용됩니다.

`kubelet` 명령에 `--runtime-provider=runsc` 플래그를 추가하여 gVisor와 함께 Kubernetes를 사용할 수도 있습니다. 그러면 gVisor가 컨테이너의 런타임 공급자로 사용됩니다.

## gVisor로 Kubernetes를 어떻게 제거합니까?

`apt` 또는 `yum`과 같은 패키지 관리자를 사용하여 gVisor로 Kubernetes를 제거할 수 있습니다.

```
apt remove kubelet runc
```

```
yum remove kubelet runc
```

## 결론

gVisor가 포함된 Kubernetes는 컨테이너를 실행하는 안전한 방법입니다. gVisor는 컨테이너를 위한 샌드박스 런타임을 제공합니다. 이렇게 하면 호스트 운영 체제에서 컨테이너가 분리되고 보안이 향상됩니다.