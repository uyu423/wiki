---
title: Kubernetes ConfigMap 및 Secrets: 구성 데이터 관리
description: 
published: true
date: 2023-02-01T17:43:45.444Z
tags: 
editor: markdown
dateCreated: 2023-02-01T17:43:43.776Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kubernetes ConfigMaps and Secrets: Managing Configuration Data***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-configmaps-and-secrets-managing-configuration-data)
{.links-list}



# Kubernetes ConfigMaps 및 Secrets: 구성 데이터 관리

Kubernetes는 구성 데이터와 비밀을 저장하고 관리하기 위한 두 가지 메커니즘인 ConfigMap과 비밀을 제공합니다. 이 기사에서는 이들 각각이 무엇인지, 어떻게 작동하는지, Kubernetes 애플리케이션에서 효과적으로 사용하는 방법을 살펴보겠습니다.

## 컨피그맵이란?

ConfigMap은 구성 데이터를 키-값 쌍으로 저장하는 Kubernetes 리소스입니다. 이 데이터는 응용 프로그램에서 필요에 따라 읽고 사용할 수 있습니다. 예를 들어 데이터베이스 연결 문자열, API 키 또는 기타 암호를 ConfigMap에 저장할 수 있습니다.

ConfigMap은 Kubernetes가 클러스터 상태를 저장하는 것과 동일한 장소인 etcd에 저장됩니다. 즉, 가용성이 높고 클러스터의 모든 노드에서 사용할 수 있습니다.

## 시크릿이란?

시크릿은 비밀번호, API 키 또는 인증서와 같은 민감한 정보를 저장하는 Kubernetes 리소스입니다. 비밀은 암호화되며 비밀을 사용해야 하는 노드에서만 암호를 해독할 수 있습니다. 이는 비밀이 ConfigMap보다 더 안전하지만 관리하기도 더 어렵다는 것을 의미합니다.

 비밀도 etcd에 저장되지만 유휴 상태에서는 암호화됩니다.

## 컨피그맵 생성

ConfigMap을 만드는 것은 간단합니다. 구성 데이터로 YAML 파일을 생성하기만 하면 됩니다. 예를 들어 데이터베이스 연결 문자열에 대한 ConfigMap을 생성해 보겠습니다.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  database-connection-string: "user:password@host:port/database"
```

그런 다음 kubectl 명령줄 도구를 사용하여 ConfigMap을 생성할 수 있습니다.

```
$ kubectl create -f my-config.yaml
configmap/my-config created
```

## 비밀 만들기

시크릿 생성은 ConfigMap 생성과 유사합니다. 구성 데이터로 YAML 파일을 생성하기만 하면 됩니다. 예를 들어 API 키에 대한 비밀을 생성해 보겠습니다.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
type: Opaque
data:
  api-key: "Zm9vYmFy"
```

보안 비밀의 데이터는 base64로 인코딩되어야 합니다. 그런 다음 kubectl 명령줄 도구를 사용하여 시크릿을 생성할 수 있습니다.

```
$ kubectl create -f my-secret.yaml
secret/my-secret created
```

## 컨피그맵과 시크릿 사용하기

이제 ConfigMap과 Secret을 생성했으므로 애플리케이션에서 어떻게 사용할 수 있는지 살펴보겠습니다.

Kubernetes에서 ConfigMap과 Secret을 사용하는 방법에는 환경 변수와 볼륨의 두 가지가 있습니다.

### 환경 변수

환경 변수를 사용하여 ConfigMap 및 Secret의 데이터를 애플리케이션에 주입할 수 있습니다. 이렇게 하려면 ConfigMap 및 Secret에 다음 주석을 추가하기만 하면 됩니다.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
  annotations:
    "configmap.kubernetes.io/env": "MY_CONFIG"
data:
  database-connection-string: "user:password@host:port/database"
```

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
  annotations:
    "secret.kubernetes.io/env": "MY_SECRET"
type: Opaque
data:
  api-key: "Zm9vYmFy"
```

주석은 Kubernetes가 ConfigMap 및 Secret의 데이터를 애플리케이션 포드의 환경에 주입하도록 합니다. 데이터는 환경 변수 MY_CONFIG 및 MY_SECRET에서 사용할 수 있습니다.

### 볼륨

볼륨을 사용하여 ConfigMap 및 Secret의 데이터를 애플리케이션에 마운트할 수도 있습니다. 이렇게 하려면 ConfigMap 및 Secret에 다음 주석을 추가하기만 하면 됩니다.

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
  annotations:
    "configmap.kubernetes.io/volume": "my-config-volume"
data:
  database-connection-string: "user:password@host:port/database"
```

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
  annotations:
    "secret.kubernetes.io/volume": "my-secret-volume"
type: Opaque
data:
  api-key: "Zm9vYmFy"
```

주석으로 인해 Kubernetes는 ConfigMap 및 Secret에 대한 볼륨을 생성합니다. 이러한 볼륨은 /etc/config/my-config-volume 및 /etc/config/my-secret-volume 경로의 애플리케이션 포드에서 사용할 수 있습니다.

## 결론

ConfigMap과 Secrets는 Kubernetes에서 구성 데이터와 비밀을 관리하기 위한 두 가지 중요한 도구입니다. 둘 다 etcd에 저장되며 클러스터의 모든 노드에서 사용할 수 있습니다.

ConfigMap은 보안 비밀보다 덜 안전하지만 관리하기는 더 쉽습니다. 비밀은 더 안전하지만 관리하기가 더 어렵습니다.

환경 변수 또는 볼륨을 사용하여 ConfigMap 및 Secret의 데이터를 애플리케이션에 주입할 수 있습니다.