---
title: OpenStack의 Kubernetes: OpenStack에 클러스터 배포
description: 
published: true
date: 2023-02-14T06:32:48.805Z
tags: 
editor: markdown
dateCreated: 2023-02-14T06:32:47.089Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes on OpenStack: Deploying Clusters on OpenStack***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-openstack-deploying-clusters-on-openstack)
{.links-list}


# OpenStack의 Kubernetes: OpenStack에 클러스터 배포

OpenStack은 데이터 센터 전체에서 대규모 컴퓨팅, 스토리지 및 네트워킹 리소스 풀을 제어하는 클라우드 운영 체제로, 모두 관리자가 제어할 수 있는 대시보드를 통해 관리되는 동시에 사용자가 웹 인터페이스를 통해 리소스를 프로비저닝할 수 있도록 합니다.

Kubernetes는 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하기 위한 오픈 소스 시스템입니다.

이 기사의 목표는 OpenStack에서 Kubernetes 클러스터를 배포하는 방법을 보여주는 것입니다. 다음 주제를 다룹니다.

- 전제 조건
- Kubernetes 클러스터 생성
- 클러스터에 애플리케이션 배포

## 전제 조건

이 가이드를 따르려면 다음이 필요합니다.

- 다음을 포함하는 OpenStack 클라우드:
  - 네트워크
  - 라우터
  - 서브넷
  - 보안 그룹
  - 키 쌍
  - 최소 3개의 컴퓨팅 노드
- OpenStack CLI 설치 및 구성
- Kubernetes CLI 설치 및 구성

## 쿠버네티스 클러스터 만들기

Kubernetes 클러스터를 배포하기 위해 `kube-up.sh` 스크립트를 사용할 것입니다. 이 스크립트는 컴퓨팅 인스턴스, 네트워크 및 로드 밸런서를 포함하여 OpenStack에 필요한 모든 리소스를 생성합니다.

먼저 Kubernetes 리포지토리를 복제합니다.

```
git clone https://github.com/kubernetes/kubernetes.git
```

다음으로 `kubernetes/cluster/openstack` 디렉터리로 변경합니다.

```
cd kubernetes/cluster/openstack
```

그런 다음 다음 내용으로 `cloud-config.yaml`이라는 파일을 생성합니다.

```yaml
#cloud-config

write_files:
- owner: root:root
  path: /etc/kubernetes/kube-up-config.yaml
  content: |
    CLOUD_PROVIDER=openstack
    OPENSTACK_AUTH_URL=https://identity.example.com:5000/v3
    OPENSTACK_USERNAME=admin
    OPENSTACK_PASSWORD=admin
    OPENSTACK_TENANT_NAME=admin
    OPENSTACK_REGION=regionOne
    OPENSTACK_CLUSTER_NAME=kubernetes
    OPENSTACK_CLUSTER_SIZE=3
    OPENSTACK_MASTER_FLAVOR=m1.small
    OPENSTACK_MASTER_IMAGE=ubuntu-16.04-x86_64-20170119
    OPENSTACK_WORKER_FLAVOR=m1.small
    OPENSTACK_WORKER_IMAGE=ubuntu-16.04-x86_64-20170119
    OPENSTACK_NETWORK_NAME=kubernetes
    OPENSTACK_MASTER_OS_DISTRIBUTION=ubuntu
    OPENSTACK_WORKER_OS_DISTRIBUTION=ubuntu
```

이 파일의 값을 자신의 OpenStack 자격 증명 및 설정으로 바꿉니다.

이제 `kube-up.sh` 스크립트를 실행하여 클러스터를 배포할 수 있습니다.

```
./kube-up.sh
```

완료하는 데 몇 분 정도 걸립니다. 완료되면 네트워크, 라우터 및 로드 밸런서와 함께 OpenStack 대시보드에 3개의 컴퓨팅 인스턴스가 표시되어야 합니다.

## 클러스터에 애플리케이션 배포

이제 Kubernetes 클러스터가 준비되어 OpenStack에서 실행 중이므로 여기에 간단한 애플리케이션을 배포해 보겠습니다. "Hello, World" 웹 애플리케이션에 대해 미리 빌드된 컨테이너 이미지를 사용합니다.

먼저 다음 내용으로 `hello-world.yaml`이라는 파일을 만들어야 합니다.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  replicas: 3
  selector:
    matchLabels:
      app: hello-world
  template:
    metadata:
      labels:
        app: hello-world
    spec:
      containers:
      - name: hello-world
        image: tutum/hello-world
        ports:
        - containerPort: 80
```

이 파일은 3개의 복제본 포드가 있는 "hello-world"라는 배포를 정의합니다. 포드는 간단한 "Hello, World" 웹 애플리케이션인 `tutum/hello-world` 컨테이너 이미지에서 생성됩니다. 포드는 포트 80에 노출됩니다.

이제 다음 명령을 실행하여 이 애플리케이션을 배포할 수 있습니다.

```
kubectl create -f hello-world.yaml
```

Pod를 만드는 데 몇 초가 걸립니다. 일단 실행되면 서비스를 생성하여 외부 세계에 노출할 수 있습니다.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-world
  labels:
    app: hello-world
spec:
  type: LoadBalancer
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: hello-world
```

이 파일을 `hello-world-service.yaml`로 저장하고 다음 명령으로 배포합니다.

```
kubectl create -f hello-world-service.yaml
```

이렇게 하면 로드 밸런서가 생성되고 포트 80에서 서비스가 노출됩니다. 다음 명령을 실행하여 로드 밸런서의 공용 IP 주소를 찾을 수 있습니다.

```
kubectl get service hello-world
```

다음과 유사한 출력이 표시되어야 합니다.

```
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP       PORT(S)        AGE
hello-world  LoadBalancer   10.0.0.1        1.2.3.4           80:31527/TCP   1m
```

이제 웹 브라우저에서 로드 밸런서의 공용 IP 주소를 방문하여 "Hello, World" 웹 애플리케이션에 액세스할 수 있습니다.

## 결론

이 기사에서는 OpenStack에 Kubernetes 클러스터를 배포하는 방법을 설명했습니다. 또한 클러스터에 간단한 웹 애플리케이션을 배포하는 방법도 보여 주었습니다.

자세한 내용은 다음 리소스를 확인하세요.

- [OpenStack의 Kubernetes: 참조 아키텍처](https://www.openstack.org/assets/pdf/kubernetes-on-openstack-a-reference-architecture.pdf)
- [오픈스택에 쿠버네티스 배포하기](https://www.mirantis.com/blog/deploying-kubernetes-on-openstack/)
- [Kubernetes 어려운 방법](https://github.com/kelseyhightower/kubernetes-the-hard-way)