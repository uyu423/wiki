---
title: CNI를 사용한 Kubernetes: 클러스터에 대한 네트워킹 구성
description: 
published: true
date: 2023-02-05T14:17:33.180Z
tags: 
editor: markdown
dateCreated: 2023-02-05T14:17:26.759Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes with CNI: Configuring Networking for Your Clusters***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-cni-configuring-networking-for-your-clusters)
{.links-list}


# CNI를 사용한 Kubernetes: 클러스터를 위한 네트워킹 구성

Kubernetes는 개발자가 클라우드 네이티브 환경에서 확장 가능한 애플리케이션을 배포하고 관리할 수 있게 해주는 강력한 컨테이너 관리 시스템입니다. Kubernetes 클러스터를 실행하기 위해 개발자는 애플리케이션에 대한 네트워킹을 구성해야 합니다. 이는 CNI(컨테이너 네트워킹 인터페이스)를 사용하여 수행할 수 있습니다.

CNI는 컨테이너용 네트워크 인터페이스 구성을 단순화하기 위한 API를 제공하는 라이브러리입니다. 개발자에게 일관된 네트워크 구성 환경을 제공하기 위해 Kubernetes와 같은 컨테이너 런타임과 함께 사용하도록 설계되었습니다. CNI는 모든 컨테이너 런타임과 함께 사용할 수 있는 이식 가능하고 확장 가능한 네트워크 구성 솔루션을 제공합니다.

이 기사에서는 CNI를 사용하여 Kubernetes 클러스터에 대한 네트워킹을 구성하는 방법을 보여줍니다. 다음 주제를 다룰 것입니다.

- CNI란?
- CNI는 어떻게 작동합니까?
- CNI를 사용하여 Kubernetes용 네트워킹을 구성하는 방법은 무엇입니까?

## CNI란?

CNI는 컨테이너용 네트워크 인터페이스 구성을 단순화하기 위한 API를 제공하는 라이브러리입니다. 개발자에게 일관된 네트워크 구성 환경을 제공하기 위해 Kubernetes와 같은 컨테이너 런타임과 함께 사용하도록 설계되었습니다. CNI는 모든 컨테이너 런타임과 함께 사용할 수 있는 이식 가능하고 확장 가능한 네트워크 구성 솔루션을 제공합니다.

## CNI는 어떻게 작동하나요?

CNI는 각 컨테이너에 대한 네트워크 네임스페이스를 생성하여 작동합니다. 네트워크 네임스페이스는 자체 네트워크 구성을 포함하는 가상 환경입니다. 이렇게 하면 각 컨테이너가 고유한 IP 주소와 네트워킹 구성을 가질 수 있습니다. 그런 다음 CNI는 플러그인을 사용하여 각 컨테이너에 대한 네트워크 인터페이스를 구성합니다.

CNI 플러그인에는 두 가지 유형이 있습니다.

- **네트워크** 플러그인: 이 플러그인은 컨테이너의 네트워크 인터페이스를 구성합니다.
- **IPAM** 플러그인: 이 플러그인은 컨테이너에 대한 IP 주소를 할당합니다.

## CNI를 사용하여 Kubernetes용 네트워킹을 구성하는 방법은 무엇입니까?

Kubernetes는 CNI를 사용하여 컨테이너의 네트워킹을 구성합니다. Kubernetes에서 CNI를 사용하려면 CNI 플러그인을 설치해야 합니다. flannel, Weave Net 및 Calico와 같은 많은 CNI 플러그인을 사용할 수 있습니다.

이 섹션에서는 flannel CNI 플러그인을 설치하고 구성하는 방법을 보여줍니다.

### flannel CNI 플러그인 설치

flannel CNI 플러그인은 CNI GitHub 리포지토리에서 사용할 수 있습니다. 플러그인을 설치하려면 바이너리를 다운로드하여 `$PATH`에 배치해야 합니다.

```
$ wget https://github.com/containernetworking/cni/releases/download/v0.6.0/cni-amd64-v0.6.0.tgz
$ tar -xvzf cni-amd64-v0.6.0.tgz -C /usr/local/bin/
```

### flannel CNI 플러그인 구성

flannel CNI 플러그인이 설치되면 구성해야 합니다. flannel CNI 플러그인은 구성 파일을 사용하여 네트워크를 구성합니다. 구성 파일은 JSON 형식이며 다음 필드를 포함합니다.

- `이름`: 네트워크의 이름입니다.
- `유형`: 네트워크 유형입니다. flannel CNI 플러그인은 `flannel` 유형을 지원합니다.
- `delegate`: 사용할 위임 CNI 플러그인입니다. flannel CNI 플러그인은 기본적으로 `bridge` 대리자를 사용합니다.
- `bridge`: 사용할 브리지의 이름입니다. flannel CNI 플러그인은 기본적으로 이름이 'cni0'인 브리지를 생성합니다.
- `isGateway`: 브리지가 네트워크의 게이트웨이인지 여부를 지정합니다. flannel CNI 플러그인은 기본적으로 이를 'true'로 설정합니다.
- `ipMasq`: IP 매스커레이딩 활성화 여부를 지정합니다. flannel CNI 플러그인은 기본적으로 이를 'true'로 설정합니다.
- `mtu`: 네트워크의 MTU. flannel CNI 플러그인은 기본적으로 이를 '1500'으로 설정합니다.
- `hairpinMode`: 헤어핀 모드 활성화 여부를 지정합니다. flannel CNI 플러그인은 기본적으로 이를 'true'로 설정합니다.

다음은 flannel CNI 플러그인 구성의 예입니다.

```json
{
    "name": "my-network",
    "type": "flannel",
    "delegate": {
        "bridge": "cni0"
    },
    "isGateway": true,
    "ipMasq": true,
    "mtu": 1500,
    "hairpinMode": true
}
```

구성 파일을 `my-network.json`으로 저장하고 `/etc/cni/net.d/` 디렉터리에 배치합니다.

### 플란넬 CNI 네트워크 생성

flannel CNI 플러그인이 설치 및 구성되면 `cni-add` 명령을 사용하여 네트워크를 생성할 수 있습니다. `cni-add` 명령은 구성 파일의 경로를 인수로 사용합니다.

```
$ sudo cni-add my-network.json
```

그러면 `my-network`라는 이름의 네트워크가 생성됩니다. 네트워크는 `my-network.json` 파일의 설정을 사용하여 구성됩니다.

### 플란넬 CNI 네트워크 삭제

flannel CNI 네트워크를 삭제하려면 `cni-del` 명령을 사용할 수 있습니다. `cni-del` 명령은 구성 파일의 경로를 인수로 사용합니다.

```
$ sudo cni-del my-network.json
```

이름이 `my-network`인 네트워크가 삭제됩니다.

## 결론

이 기사에서는 CNI를 사용하여 Kubernetes 클러스터에 대한 네트워킹을 구성하는 방법을 설명했습니다. 우리는 다음 주제를 다루었습니다.

- CNI란?
- CNI는 어떻게 작동합니까?
- CNI를 사용하여 Kubernetes용 네트워킹을 구성하는 방법은 무엇입니까?

Kubernetes의 네트워킹 구성에 대해 궁금한 점이 있으면 아래에 의견을 남겨주세요.