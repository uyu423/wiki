---
title: Kubernetes 보안: 클러스터 강화를 위한 모범 사례
description: 
published: true
date: 2023-02-09T01:32:55.549Z
tags: 
editor: markdown
dateCreated: 2023-02-09T01:32:53.972Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes Security: Best Practices for Hardening Your Cluster***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-security-best-practices-for-hardening-your-cluster)
{.links-list}


# 쿠버네티스 보안: 클러스터 강화를 위한 모범 사례

Kubernetes를 채택하면 가용성이 높은 방식으로 컨테이너화된 애플리케이션을 배포, 확장 및 관리할 수 있는 유연성을 얻을 수 있습니다. 그러나 이러한 새로운 수준의 제어 및 책임에는 새로운 보안 문제가 수반됩니다.

Kubernetes는 많은 구성 요소와 움직이는 부분이 있는 복잡한 시스템이므로 기본적으로 보안을 유지하기 어렵습니다. 그러나 몇 가지 간단한 모범 사례를 따르면 Kubernetes 클러스터를 강화하고 일반적인 위협으로부터 애플리케이션을 보호할 수 있습니다.

이 기사에서는 다음을 포함하여 가장 중요한 Kubernetes 보안 모범 사례 중 일부를 다룹니다.

* Kubernetes 리소스에 대한 액세스를 제어하도록 RBAC 구성
* TLS로 네트워크 트래픽 암호화
* 포드 간 통신을 제한하는 네트워크 정책 구현
* 최소 권한 보안 컨텍스트에서 컨테이너 실행
* Kubernetes API 서버 보안
* 이미지 스캐너를 사용하여 보안 정책 시행

## Kubernetes 리소스에 대한 액세스를 제어하도록 RBAC 구성

RBAC(역할 기반 액세스 제어)는 Kubernetes 리소스에 액세스할 수 있는 사용자 및 서비스 계정을 세부적으로 제어할 수 있는 Kubernetes 기능입니다.

RBAC는 Kubernetes에서 기본적으로 비활성화되어 있으므로 클러스터를 보호하는 첫 번째 단계는 활성화하는 것입니다. Kubernetes 클러스터를 시작할 때 `--authorization-mode=RBAC` 플래그를 `kube-apiserver` 바이너리에 전달하면 됩니다.

RBAC가 활성화되면 'Role' 및 'ClusterRole' 객체를 생성하여 지정된 사용자 또는 서비스 계정에 부여해야 하는 권한을 정의할 수 있습니다. 예를 들어 사용자가 네임스페이스의 모든 리소스를 보고 나열할 수 있지만 리소스를 만들거나 삭제할 수는 없는 '역할'을 만들 수 있습니다.

그런 다음 'RoleBinding' 또는 'ClusterRoleBinding'을 생성하여 'Role' 또는 'ClusterRole'을 사용자 또는 서비스 계정에 바인딩할 수 있습니다. 이렇게 하면 사용자 또는 서비스 계정에 지정된 권한이 부여됩니다.

기본적으로 모든 인증된 사용자는 Kubernetes API에 대한 전체 액세스 권한을 가집니다. 즉, RBAC로 액세스를 명시적으로 제한하지 않는 한 Kubernetes 클러스터에 인증할 수 있는 모든 사용자는 클러스터의 모든 리소스 삭제를 포함하여 모든 작업을 수행할 수 있습니다.

## TLS로 네트워크 트래픽 암호화

TLS(전송 계층 보안)는 도청 및 변조를 방지하기 위해 네트워크 트래픽을 암호화할 수 있는 프로토콜입니다.

Kubernetes는 TLS를 사용하여 구성 요소 간의 모든 통신은 물론 Kubernetes API 서버와 클라이언트 간의 통신을 암호화합니다. 기본적으로 Kubernetes는 모든 구성 요소에 대해 자체 서명된 인증서를 생성합니다. 대부분의 개발 및 테스트 환경에서는 이 정도면 충분하지만 프로덕션에서는 서명된 인증서를 사용하여 트래픽을 가로채거나 변조할 수 없도록 해야 합니다.

선택한 인증 기관(CA)을 사용하여 서명된 인증서를 생성하거나 'kube-ssl'과 같은 도구를 사용하여 Kubernetes 클러스터에 대해 서명된 인증서를 자동으로 생성 및 배포할 수 있습니다.

## 포드 간 통신을 제한하는 네트워크 정책 구현

네트워크 정책은 서로 통신할 수 있는 Pod를 제어할 수 있는 Kubernetes 기능입니다. 기본적으로 Kubernetes 클러스터의 모든 포드는 서로 통신할 수 있지만 이로 인해 애플리케이션이 불필요한 위험에 노출됩니다.

예를 들어 중요한 데이터가 포함된 포드가 있는 경우 신뢰할 수 있는 포드의 통신만 허용하도록 통신을 제한할 수 있습니다. 또는 여러 마이크로 서비스로 구성된 애플리케이션이 있는 경우 서로 통신해야 하는 서비스 간의 통신만 허용하도록 통신을 제한할 수 있습니다.

네트워크 정책은 Kubernetes 리소스로 구현되며 이를 사용하여 서로 통신할 수 있는 포드를 지정할 수 있습니다. 예를 들어 다음 네트워크 정책은 `frontend` 및 `backend` 네임스페이스의 포드 간 통신을 허용하지만 `frontend` 네임스페이스의 포드와 `database` 네임스페이스의 포드 간 통신은 허용하지 않습니다.

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: frontend-backend
  namespace: frontend
spec:
  podSelector:
    matchLabels:
      app: frontend
  policyTypes:
  - Ingress
  - Egress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: backend
  egress:
  - to:
    - podSelector:
        matchLabels:
          app: backend
```

네트워크 정책은 복잡한 주제이며 이를 구성하는 방법에는 여러 가지가 있습니다. 자세한 내용은 네트워크 정책에 대한 Kubernetes 설명서를 읽는 것이 좋습니다.

## 최소 권한 보안 컨텍스트에서 컨테이너 실행

보안 컨텍스트는 팟(Pod) 또는 컨테이너에 적용할 수 있는 보안 관련 옵션 세트입니다. 이러한 옵션을 사용하여 포드 또는 컨테이너에 액세스할 수 있는 사용자 및 그룹과 허용되는 기능을 제어할 수 있습니다.

기본적으로 Kubernetes의 컨테이너는 호스트 시스템에 대한 전체 액세스 권한을 컨테이너에 부여하는 '루트' 사용자로 실행됩니다. 악의적인 컨테이너가 중요한 호스트 시스템 데이터에 잠재적으로 액세스하거나 전체 호스트 시스템을 장악할 수 있으므로 이는 주요 보안 위험입니다.

이 위험을 완화하려면 항상 최소 권한의 보안 컨텍스트에서 컨테이너를 실행해야 합니다. 이는 컨테이너를 실행할 루트가 아닌 사용자를 지정하고 컨테이너가 사용할 수 있는 기능을 지정하는 것을 의미합니다.

예를 들어 다음 `Pod` 정의는 `nginx` 컨테이너를 `nginx` 사용자로 실행하고 컨테이너가 어떤 기능도 사용할 수 없도록 합니다.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
  namespace: default
spec:
  securityContext:
    runAsUser: 1000
    fsGroup: 1000
  containers:
  - name: nginx
    image: nginx
    securityContext:
      capabilities: {}
```

루트가 아닌 사용자로 컨테이너를 실행하는 것은 일반적으로 좋은 보안 관행이며 컨테이너가 중요한 호스트 시스템 데이터에 잠재적으로 액세스할 수 있는 Kubernetes에서 특히 중요합니다.

## Kubernetes API 서버 보안

Kubernetes API 서버는 모든 Kubernetes 구성요소의 통신 중심점이며 모든 API 요청 처리를 담당합니다. 이것은 API 서버를 Kubernetes 시스템의 중요한 구성 요소로 만들고 무단 액세스를 방지하기 위해 이를 보호하는 것이 중요합니다.

API 서버를 보호하는 한 가지 방법은 TLS 인증서를 사용하여 API 서버로 들어오고 나가는 모든 트래픽을 암호화하는 것입니다. 앞에서 언급했듯이 Kubernetes는 기본적으로 모든 구성 요소에 대해 자체 서명된 인증서를 생성하지만 트래픽을 가로채거나 변조할 수 없도록 프로덕션 환경에서 서명된 인증서를 사용해야 합니다.

API 서버를 보호하는 또 다른 방법은 인증 플러그인을 사용하는 것입니다. 쿠버네티스에는 `HTTPBasicAuth`, `Token`, `X509` 및 `Webhook`을 비롯한 다양한 내장 인증 플러그인이 포함되어 있습니다. 'OIDC' 또는 'LDAP'와 같은 타사 인증 플러그인을 사용할 수도 있습니다.

## 이미지 스캐너를 사용하여 보안 정책 시행

이미지 스캐너는 컨테이너 이미지에 대한 보안 정책을 적용하는 데 도움이 되는 도구입니다. 예를 들어 이미지 스캐너를 사용하여 이미지의 알려진 취약성을 확인하거나 이미지에 신뢰할 수 있는 기관의 서명이 필요한 정책을 시행할 수 있습니다.

Kubernetes에는 이미지에서 알려진 취약점을 스캔하는 데 사용할 수 있는 'Clair'라는 이미지 스캐너가 내장되어 있습니다. Clair는 오픈 소스 프로젝트이며 프로젝트 웹 사이트에서 이에 대한 자세한 정보를 찾을 수 있습니다.

Clair 외에도 오픈 소스 및 상용 이미지 스캐너가 많이 있습니다. 특정 요구 사항을 충족하는 이미지 스캐너를 찾기 위해 몇 가지 조사를 수행하는 것이 좋습니다.

## 결론

이 기사에서는 가장 중요한 Kubernetes 보안 모범 사례 중 일부를 다루었습니다. 이러한 모범 사례를 따르면 Kubernetes 클러스터를 강화하고 일반적인 위협으로부터 애플리케이션을 보호할 수 있습니다.