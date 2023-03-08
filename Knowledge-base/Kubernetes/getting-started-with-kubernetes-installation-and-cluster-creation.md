---
title: Kubernetes 시작하기: 설치 및 클러스터 생성
description: 
published: true
date: 2023-02-08T17:32:54.414Z
tags: 
editor: markdown
dateCreated: 2023-02-08T17:32:52.667Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Getting Started with Kubernetes: Installation and Cluster Creation***English** document is available*](/en/Knowledge-base/Kubernetes/getting-started-with-kubernetes-installation-and-cluster-creation)
{.links-list}


# Kubernetes 시작하기: 설치 및 클러스터 생성

Kubernetes는 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하는 데 도움이 되는 강력한 컨테이너 오케스트레이션 도구입니다. 이 기사에서는 로컬 시스템에 Kubernetes를 설치하고 Kubernetes 클러스터를 생성하는 방법을 보여줍니다.

## 전제 조건

시작하기 전에 다음이 필요합니다.

- Linux 또는 Windows를 실행하는 로컬 시스템
- [Docker](https://docs.docker.com/install/) 설치 및 실행
- [Kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/) 설치
- [Minikube](https://kubernetes.io/docs/tasks/tools/install-minikube/) 설치

## 쿠버네티스 설치하기

Kubernetes는 Minikube를 사용하여 로컬 컴퓨터에 설치할 수 있습니다. Minikube는 개발 및 테스트 목적으로 사용할 수 있는 경량 Kubernetes 구현입니다.

Minikube를 사용하여 Kubernetes를 설치하려면 다음 명령을 실행하십시오.

```
$ minikube start
```

그러면 가상 머신이 시작되고 여기에 Kubernetes가 설치됩니다. 설치가 완료되면 다음 명령을 실행하여 설치를 확인할 수 있습니다.

```
$ kubectl get nodes
```

이 명령은 Minikube에서 생성한 노드를 나열해야 합니다.

## 쿠버네티스 클러스터 만들기

이제 Kubernetes가 실행 중이므로 Kubernetes 클러스터를 생성할 수 있습니다. 이렇게 하려면 [배포](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) 및 [서비스](https://kubernetes.io/docs/concepts)를 생성해야 합니다. /서비스-네트워킹/서비스/).

배포는 팟(Pod) 그룹의 원하는 상태를 설명하는 Kubernetes 객체입니다. 서비스는 포드 그룹을 외부 세계에 노출하는 Kubernetes 개체입니다.

배포 및 서비스를 생성하려면 다음을 포함하는 [YAML](https://en.wikipedia.org/wiki/YAML) 파일을 생성해야 합니다.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
---
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  ports:
  - port: 80
    nodePort: 30000
  selector:
    app: nginx
```

이 파일에서 우리는 [nginx](https://www.nginx.com/) 컨테이너의 세 가지 복제본과 배포를 외부 세계에 노출하는 서비스로 배포를 정의했습니다.

배포 및 서비스를 만들려면 다음 명령을 실행합니다.

```
$ kubectl apply -f deployment.yaml
```

이렇게 하면 배포 및 서비스가 생성됩니다. 다음 명령을 실행하여 배포 및 서비스가 생성되었는지 확인할 수 있습니다.

```
$ kubectl get deployments
```

```
$ kubectl get services
```

## Kubernetes 클러스터에 액세스

이제 배포 및 서비스가 생성되었으므로 로컬 시스템에서 Kubernetes 클러스터에 액세스할 수 있습니다. 이렇게 하려면 Minikube 가상 머신의 IP 주소와 서비스의 노드 포트를 가져와야 합니다.

Minikube 가상 머신의 IP 주소를 얻으려면 다음 명령을 실행하십시오.

```
$ minikube ip
```

서비스의 노드 포트를 가져오려면 다음 명령을 실행합니다.

```
$ kubectl describe service nginx-service
```

다음 출력이 표시되어야 합니다.

```
Name:              nginx-service
Namespace:         default
Labels:            <none>
Annotations:       <none>
Selector:          app=nginx
Type:              NodePort
IP:                10.0.0.1
Port:              <unnamed>  80/TCP
TargetPort:        80/TCP
NodePort:          <unnamed>  30000/TCP
Endpoints:         10.0.0.2:80,10.0.0.3:80,10.0.0.4:80
Session Affinity:  None
External Traffic Policy:  Cluster
Events:            <none>
```

노드 포트는 `NodePort` 필드의 값입니다. 이 경우 노드 포트는 '30000'입니다.

Kubernetes 클러스터에 액세스하려면 웹 브라우저를 열고 `http://<minikube-ip>:<node-port>`로 이동합니다. 이 예에서 URL은 `http://10.0.0.1:30000`입니다.

기본 nginx 페이지가 표시됩니다.

![nginx](https://www.nginx.com/wp-content/uploads/2018/08/nginx-logo.png)

## Kubernetes 클러스터 삭제

Kubernetes 클러스터를 삭제하려면 다음 명령을 실행합니다.

```
$ minikube delete
```

그러면 Minikube 가상 머신과 이전 단계에서 생성된 모든 리소스가 삭제됩니다.

## 결론

이 기사에서는 로컬 머신에 Kubernetes를 설치하고 Kubernetes 클러스터를 생성하는 방법을 설명했습니다. Kubernetes는 컨테이너화된 애플리케이션의 배포, 확장 및 관리를 자동화하는 데 도움이 되는 강력한 도구입니다.