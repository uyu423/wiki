---
title: Istio를 사용한 Kubernetes: 애플리케이션을 위한 서비스 메시 구현
description: 
published: true
date: 2023-02-02T05:44:02.961Z
tags: 
editor: markdown
dateCreated: 2023-02-02T05:43:58.529Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kubernetes with Istio: Implementing Service Mesh for Your Applications***English** document is available*](/en/Knowledge-base/Kubernetes/kubernetes-with-istio-implementing-service-mesh-for-your-applications)
{.links-list}


# Kubernetes with Istio: 애플리케이션을 위한 서비스 메시 구현

Kubernetes는 컨테이너화된 애플리케이션 관리를 자동화하기 위한 오픈 소스 시스템입니다. Istio는 마이크로서비스를 연결, 관리 및 보호하기 위한 개방형 플랫폼입니다.

서비스 메시는 서비스 간 통신을 안정적이고 빠르고 안전하게 만드는 마이크로서비스 애플리케이션을 위한 구성 가능한 인프라 계층입니다. 서비스 메시는 일반적으로 데이터 평면과 제어 평면으로 구성됩니다. 데이터 플레인은 마이크로서비스 간의 통신을 중재하는 지능형 프록시 세트로 구성됩니다. 컨트롤 플레인은 프록시를 관리하고 구성합니다.

Istio는 Kubernetes용 서비스 메시입니다. 데이터 평면과 제어 평면으로 구성됩니다. 데이터 플레인은 마이크로서비스 간의 통신을 중재하는 지능형 프록시 세트로 구성됩니다. 컨트롤 플레인은 프록시를 관리하고 구성합니다.

Istio가 포함된 Kubernetes는 애플리케이션에 대한 서비스 메시를 구현하는 데 사용할 수 있습니다. 이 기사에서는 Kubernetes 클러스터에 Istio를 설치 및 구성하는 방법과 샘플 마이크로서비스 애플리케이션을 배포하는 방법을 보여줍니다.

## Kubernetes에 Istio 설치

Istio는 Helm 패키지 관리자를 사용하여 Kubernetes 클러스터에 설치할 수 있습니다. Helm은 Kubernetes 애플리케이션을 관리하기 위한 도구입니다.

Istio를 설치하려면 먼저 Helm을 설치하고 Istio Helm 리포지토리를 추가해야 합니다.

### 헬름 설치

[Helm 웹사이트](https://helm.sh/docs/using_helm/# installing-helm)에서 Helm 바이너리를 다운로드합니다.

helm 바이너리를 추출하여 PATH에 추가합니다.

```
tar xzf helm-v2.16.5-linux-amd64.tar.gz
sudo mv linux-amd64/helm /usr/local/bin/
```

Helm을 초기화하고 Helm의 서버 측 구성 요소인 Tiller를 설치합니다.

```
helm init
```

### Istio Helm 저장소 추가

Istio Helm 저장소를 추가하십시오.

```
helm repo add istio.io https://storage.googleapis.com/istio-release/releases/1.5.2/charts/
```

Helm 리포지토리를 업데이트합니다.

```
helm repo update
```

## 샘플 마이크로서비스 애플리케이션 배포

네 가지 서비스로 구성된 샘플 마이크로서비스 애플리케이션을 배포합니다.

- Node.js로 작성된 프론트엔드 서비스
- Golang으로 작성된 백엔드 서비스
- 데이터베이스 서비스
- 로드 밸런서 서비스

프런트엔드 및 백엔드 서비스는 별도의 포드에 배포됩니다. 데이터베이스 서비스는 별도의 포드에 배포됩니다. 로드 밸런서 서비스는 별도의 포드에 배포됩니다.

프런트엔드 서비스는 백엔드 서비스에 요청합니다. 백엔드 서비스는 데이터베이스 서비스에 요청합니다. 로드 밸런서 서비스는 프런트엔드 및 백엔드 서비스로 트래픽을 라우팅합니다.

Istio Helm 차트를 사용하여 애플리케이션을 배포합니다.

### Istio Helm 차트 설치

다음 명령을 사용하여 Istio Helm 차트를 설치합니다.

```
helm install --name istio-system -f /path/to/custom-values.yaml istio.io/istio
```

Istio Helm 차트는 `istio-system` 네임스페이스에 설치됩니다.

### 프런트엔드 서비스 배포

프런트엔드 서비스용 팟(Pod)을 작성하십시오.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: frontend
  labels:
    app: frontend
spec:
  containers:
  - name: frontend
    image: node:12-alpine
    ports:
    - containerPort: 3000
```

포드를 배포합니다.

```
kubectl apply -f /path/to/frontend-pod.yaml
```

### 백엔드 서비스 배포

백엔드 서비스용 포드를 만듭니다.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: backend
  labels:
    app: backend
spec:
  containers:
  - name: backend
    image: golang:1.14-alpine
    ports:
    - containerPort: 3000
```

포드를 배포합니다.

```
kubectl apply -f /path/to/backend-pod.yaml
```

### 데이터베이스 서비스 배포

데이터베이스 서비스에 대한 팟(Pod)을 작성하십시오.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: database
  labels:
    app: database
spec:
  containers:
  - name: database
    image: mysql:5.7
    ports:
    - containerPort: 3306
```

포드를 배포합니다.

```
kubectl apply -f /path/to/database-pod.yaml
```

### 로드 밸런서 서비스 배포

로드 밸런서 서비스에 대한 팟(Pod)을 작성하십시오.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: load-balancer
  labels:
    app: load-balancer
spec:
  containers:
  - name: load-balancer
    image: nginx:1.17.9-alpine
    ports:
    - containerPort: 80
```

포드를 배포합니다.

```
kubectl apply -f /path/to/load-balancer-pod.yaml
```

### 애플리케이션 테스트

애플리케이션을 테스트하기 위해 로드 밸런서 서비스에 요청을 보냅니다. 로드 밸런서 서비스는 요청을 프런트엔드 서비스로 라우팅합니다. 프런트엔드 서비스는 백엔드 서비스에 요청합니다. 백엔드 서비스는 데이터베이스 서비스에 요청합니다.

먼저 로드 밸런서 서비스의 IP 주소를 가져와야 합니다.

```
kubectl get svc
```

출력은 다음과 같아야 합니다.

```
NAME            TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
frontend        ClusterIP      10.108.1.194     <none>        3000/TCP         1m
backend         ClusterIP      10.96.247.199    <none>        3000/TCP         1m
database        ClusterIP      10.111.142.247   <none>        3306/TCP         1m
load-balancer   LoadBalancer   10.102.129.251   <pending>     80:32000/TCP     1m
```

로드 밸런서 서비스에는 '10.102.129.251'의 'ClusterIP'와 '80:32000'의 'PORT'가 있습니다.

이제 로드 밸런서 서비스에 요청을 보낼 수 있습니다.

```
curl -v http://10.102.129.251:80
```

출력은 다음과 같아야 합니다.

```
*   Trying 10.102.129.251:80...
* TCP_NODELAY set
* Connected to 10.102.129.251 (10.102.129.251) port 80 (#0)
> GET / HTTP/1.1
> Host: 10.102.129.251:80
> User-Agent: curl/7.64.1
> Accept: */*
>
< HTTP/1.1 200 OK
< Content-Type: text/html
< Content-Length: 28
<
<html>
<body>
Hello, World!
</body>
</html>
* Connection #0 to host 10.102.129.251 left intact
```

요청이 프런트엔드 서비스로 라우팅되었고 응답이 반환되었습니다.

## 결론

이 기사에서는 Kubernetes 클러스터에 Istio를 설치하고 구성하는 방법과 샘플 마이크로서비스 애플리케이션을 배포하는 방법을 보여주었습니다. Istio는 애플리케이션을 위한 서비스 메시를 구현하는 데 사용할 수 있습니다.