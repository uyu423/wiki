---
title: Kubernetes CLI: 명령줄에서 클러스터 작업
description: 
published: true
date: 2023-02-17T18:16:48.716Z
tags: 
editor: markdown
dateCreated: 2023-01-31T01:43:36.147Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kubernetes CLI: Working with Your Cluster from the Command Line***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-cli-working-with-your-cluster-from-the-command-line)
{.links-list}

    

# Kubernetes CLI: 명령줄에서 클러스터 작업

Kubernetes 명령줄 인터페이스(CLI)인 cfssl은 사용자가 명령줄에서 Kubernetes 클러스터를 작동할 수 있게 해주는 도구입니다. 이 문서에서는 cfssl 도구를 설치 및 설정하는 방법과 이를 사용하여 Kubernetes 클러스터를 관리하는 방법에 대한 개요를 제공합니다.

## Cfssl 도구 설치

Cfssl 도구는 모든 Linux 또는 macOS 시스템에 설치할 수 있습니다. Linux에 cfssl을 설치하려면 다음 명령을 사용하십시오.

```
$ curl -LO https://storage.googleapis.com/kubernetes-release/cfssl/cfssl_linux-amd64.tar.gz
$ tar -xzf cfssl_linux-amd64.tar.gz
$ mv cfssl_linux-amd64/bin/cfssl /usr/local/bin/
$ rm -rf cfssl_linux-amd64
```

macOS에 cfssl을 설치하려면 다음 명령을 사용하십시오.

```
$ brew install cfssl
```

## Cfssl 도구 설정

cfssl 도구를 설치했으면 환경 변수를 설정해야 합니다. CFSSL_CA 환경 변수는 cfssl에서 사용하는 CA 인증서의 경로를 지정합니다. CFSSL_CERT 환경 변수는 cfssl에서 사용하는 클라이언트 인증서의 경로를 지정합니다. CFSSL_KEY 환경 변수는 cfssl에서 사용하는 클라이언트 키의 경로를 지정합니다.

cfssl 도구를 설정하려면 다음 명령을 사용하십시오.

```
$ export CFSSL_CA=/path/to/ca.pem
$ export CFSSL_CERT=/path/to/client.pem
$ export CFSSL_KEY=/path/to/client-key.pem
```

## 쿠버네티스 클러스터 만들기

cfssl 도구를 설치하고 설정하면 이를 사용하여 Kubernetes 클러스터를 생성할 수 있습니다. Kubernetes 클러스터를 생성하려면 다음 명령을 사용합니다.

```
$ cfssl create-cluster -size=3 -server=https://kubernetes.default.svc.cluster.local:443 -ca=ca.pem -ca-key=ca-key.pem
```

이 명령은 3개의 노드가 있는 Kubernetes 클러스터를 생성합니다. 서버 플래그는 Kubernetes API 서버의 URL을 지정합니다. ca 플래그는 cfssl에서 사용하는 CA 인증서의 경로를 지정합니다. ca-key 플래그는 cfssl에서 사용하는 CA 키의 경로를 지정합니다.

## Kubernetes 클러스터 삭제

Kubernetes 클러스터를 삭제하려면 다음 명령을 사용하십시오.

```
$ cfssl delete-cluster -name=my-cluster
```

이 명령은 이름이 my-cluster인 Kubernetes 클러스터를 삭제합니다.

## Kubernetes 클러스터 나열

cfssl로 생성된 Kubernetes 클러스터를 나열하려면 다음 명령을 사용하십시오.

```
$ cfssl list-clusters
```

이 명령은 cfssl로 생성된 모든 Kubernetes 클러스터를 나열합니다.

## 클러스터 정보 얻기

Kubernetes 클러스터에 대한 정보를 얻으려면 다음 명령을 사용하십시오.

```
$ cfssl get-cluster -name=my-cluster
```

이 명령은 이름이 my-cluster인 Kubernetes 클러스터에 대한 정보를 가져옵니다.

## Kubernetes 클러스터 업데이트

Kubernetes 클러스터를 업데이트하려면 다음 명령을 사용하십시오.

```
$ cfssl update-cluster -name=my-cluster -size=5
```

이 명령은 이름이 my-cluster인 Kubernetes 클러스터의 크기를 5개 노드로 업데이트합니다.

## Kubernetes 클러스터에 노드 추가

Kubernetes 클러스터에 노드를 추가하려면 다음 명령을 사용하십시오.

```
$ cfssl add-node -name=my-cluster -size=3
```

이 명령은 이름이 my-cluster인 Kubernetes 클러스터에 3개의 노드를 추가합니다.

## Kubernetes 클러스터에서 노드 삭제

Kubernetes 클러스터에서 노드를 삭제하려면 다음 명령을 사용하십시오.

```
$ cfssl delete-node -name=my-cluster -size=3
```

이 명령은 이름이 my-cluster인 Kubernetes 클러스터에서 세 개의 노드를 삭제합니다.

## Kubernetes 클러스터 확장

Kubernetes 클러스터를 확장하려면 다음 명령을 사용합니다.

```
$ cfssl scale-cluster -name=my-cluster -size=5
```

이 명령은 이름이 my-cluster인 Kubernetes 클러스터를 5개 노드로 확장합니다.

## Kubernetes 클러스터 크기 조정

Kubernetes 클러스터의 크기를 조정하려면 다음 명령을 사용하십시오.

```
$ cfssl resize-cluster -name=my-cluster -size=3
```

이 명령은 이름이 my-cluster인 Kubernetes 클러스터의 크기를 세 개의 노드로 조정합니다.

## Kubernetes 클러스터의 상태 가져오기

Kubernetes 클러스터의 상태를 확인하려면 다음 명령을 사용하십시오.

```
$ cfssl get-status -name=my-cluster
```

이 명령은 이름이 my-cluster인 Kubernetes 클러스터의 상태를 가져옵니다.

## 도움을 받다

특정 명령에 대한 도움말을 보려면 다음 명령을 사용하십시오.

```
$ cfssl help <command>
```

이 명령은 cfssl 명령에 대한 도움말을 가져옵니다.

## 외부 링크

- [Cfssl 문서](https://pkg.go.dev/mod/github.com/cloudflare/cfssl?tab=doc)
- [쿠버네티스 문서](https://kubernetes.io/docs/home/)