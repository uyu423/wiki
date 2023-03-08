---
title: Kubernetes RBAC: 클러스터 리소스에 대한 액세스 보안
description: 
published: true
date: 2023-02-09T00:32:28.957Z
tags: 
editor: markdown
dateCreated: 2023-02-09T00:32:27.317Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes RBAC: Securing Access to Cluster Resources***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-rbac-securing-access-to-cluster-resources)
{.links-list}


# Kubernetes RBAC: 클러스터 리소스에 대한 액세스 보안

RBAC(역할 기반 액세스 제어)는 컴퓨터 시스템, 애플리케이션 및 데이터에 대한 액세스를 규제하는 방법입니다. 모든 엔터프라이즈 환경에서 보안의 기본 구성 요소입니다.

Kubernetes에서 RBAC는 Kubernetes API에 대한 액세스를 제어하는 데 사용됩니다. Kubernetes API에 액세스해야 하는 모든 사용자, 그룹 또는 서비스 계정에는 보유한 액세스 수준을 정의하는 역할이 부여되어야 합니다.

Kubernetes에는 세 가지 유형의 역할이 있습니다.

- **ClusterRole**: ClusterRole은 클러스터의 모든 네임스페이스에 적용할 수 있는 권한 집합을 정의합니다.
- **역할**: 역할은 단일 네임스페이스에만 적용할 수 있습니다.
- **ServiceAccount**: ServiceAccount는 서비스 계정에 적용할 수 있는 권한 집합을 정의합니다.

역할은 `kubectl` 명령줄 도구를 사용하여 생성할 수 있습니다. 예를 들어 `my-cluster-role`이라는 ClusterRole을 생성하려면 다음 명령을 사용합니다.

```
kubectl create clusterrole my-cluster-role --verb=get,list,watch
```

이렇게 하면 `my-cluster-role`에 클러스터의 `get`, `list` 및 `watch` 리소스에 대한 권한이 부여됩니다.

YAML 파일을 사용하여 역할을 생성할 수도 있습니다. 다음은 ClusterRole에 대한 예제 YAML 파일입니다.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: my-cluster-role
rules:
- apiGroups: [""] # "" indicates the core API group
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
```

역할은 'RoleBinding' 또는 'ClusterRoleBinding'을 사용하여 사용자, 그룹 또는 서비스 계정에 결합될 수 있습니다. 예를 들어 다음 명령은 `my-user`에 `my-cluster-role`을 제공합니다.

```
kubectl create clusterrolebinding my-cluster-role-binding --clusterrole=my-cluster-role --user=my-user
```

이것은 `my-user`에게 `my-cluster-role`에 정의된 권한을 부여합니다.

 바인딩은 YAML 파일을 사용하여 만들 수도 있습니다. 다음은 ClusterRoleBinding에 대한 예제 YAML 파일입니다.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: my-cluster-role-binding
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: my-cluster-role
subjects:
- kind: User
  name: my-user
  apiGroup: rbac.authorization.k8s.io
```

이렇게 하면 `my-user`에 `my-cluster-role`이 부여됩니다.

RBAC를 사용하여 모든 사용자, 그룹 또는 서비스 계정의 Kubernetes API에 대한 액세스를 제어할 수 있습니다. 모든 Kubernetes 클러스터에서 보안의 기본 구성 요소입니다.