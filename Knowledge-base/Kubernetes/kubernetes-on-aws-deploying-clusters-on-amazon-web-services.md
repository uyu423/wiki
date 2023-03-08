---
title: AWS의 Kubernetes: Amazon Web Services에 클러스터 배포
description: 
published: true
date: 2023-02-01T00:06:05.623Z
tags: 
editor: markdown
dateCreated: 2023-02-01T00:06:03.874Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kubernetes on AWS: Deploying Clusters on Amazon Web Services***English** version of this document is available*](/en/Knowledge-base/Kubernetes/kubernetes-on-aws-deploying-clusters-on-amazon-web-services)
{.links-list}



# AWS의 쿠버네티스: Amazon Web Services에 클러스터 배포

Kubernetes는 애플리케이션 배포, 확장 및 관리를 자동화하기 위한 오픈 소스 컨테이너 오케스트레이션 시스템입니다. 애플리케이션을 구성하는 컨테이너를 논리 단위로 그룹화하여 쉽게 관리하고 검색할 수 있습니다.

AWS는 Amazon에서 제공하는 포괄적이고 진화하는 클라우드 컴퓨팅 플랫폼입니다. IaaS(Infrastructure as a Service), PaaS(Platform as a Service) 및 패키지형 SaaS(Software as a Service) 제품을 혼합하여 제공합니다.

AWS에서 Kubernetes를 사용하여 AWS에서 컨테이너화된 애플리케이션을 배포, 관리 및 확장할 수 있습니다. 이 기사에서는 AWS에서 Kubernetes 클러스터를 배포하는 방법을 보여줍니다.

## 전제 조건

이 가이드를 따르려면 다음이 필요합니다.

- AWS 계정. 계정이 없으면 [여기](https://aws.amazon.com/)에서 생성할 수 있습니다.

- 컴퓨터에 설치 및 구성된 AWS 명령줄 인터페이스(CLI). 이를 수행하는 방법에 대한 지침은 [여기](https://docs.aws.amazon.com/cli/latest/userguide/installing.html)에서 찾을 수 있습니다.

- 컴퓨터에 설치된 kubectl 명령줄 도구. 이를 수행하는 방법에 대한 지침은 [여기](https://kubernetes.io/docs/tasks/tools/install-kubectl/)에서 찾을 수 있습니다.

- 도메인 이름. [Freenom](https://www.freenom.com/)과 같은 서비스에서 무료로 받을 수 있습니다.

## AWS Kubernetes 클러스터 설정

AWS에서 Kubernetes 클러스터를 설정하는 방법에는 여러 가지가 있습니다. 이 기사에서는 AWS Management Console을 사용하여 클러스터를 설정합니다.

먼저 AWS Management Console에 로그인하고 Amazon EKS 서비스로 이동합니다.

![](https://i.imgur.com/LDAd5u8.png)

"클러스터 생성" 버튼을 클릭합니다.

![](https://i.imgur.com/p0bJUO4.png)

다음 페이지에서 클러스터 이름을 입력하고 배포할 지역을 선택합니다. 그런 다음 사용할 Kubernetes 버전을 선택합니다. 작성 당시 최신 버전인 1.17을 사용하겠습니다.

![](https://i.imgur.com/Ft7YIxu.png)

다음으로 작업자 노드를 구성해야 합니다. 작업자 노드는 애플리케이션을 실행할 클러스터의 머신입니다. 작업자 노드에 Amazon EC2 인스턴스를 사용합니다.

"CloudFormation 스택 시작" 버튼을 클릭합니다.

![](https://i.imgur.com/O4E0b4I.png)

다음 페이지에서 "AWS CloudFormation이 IAM 리소스를 생성할 수 있음을 확인합니다." 확인란을 선택하고 "스택 생성" 버튼을 클릭합니다.

![](https://i.imgur.com/VkzM0Ss.png)

다음 페이지에서 CloudFormation에서 생성되는 스택을 볼 수 있습니다. 이 작업은 몇 분 정도 소요됩니다.

![](https://i.imgur.com/W0Qiu8D.png)

스택이 생성되면 "출력" 탭을 클릭하여 작업자 노드 구성의 세부 정보를 볼 수 있습니다.

![](https://i.imgur.com/tY0NVT3.png)

나중에 필요하므로 "NodeInstanceRole" 및 "WorkerNodeSecurityGroup" 값을 기록해 둡니다.

이제 작업자 노드가 설정되었으므로 Amazon EKS 콘솔로 돌아가서 클러스터를 생성할 수 있습니다.

"다음 단계" 버튼을 클릭합니다.

![](https://i.imgur.com/Ft7YIxu.png)

다음 페이지에서 작업자 노드를 구성해야 합니다. 원하는 작업자 노드 수를 선택하고 이전에 기록한 "NodeInstanceRole" 및 "WorkerNodeSecurityGroup" 값을 입력합니다.

![](https://i.imgur.com/vALDKQi.png)

다음으로 네트워킹을 구성해야 합니다. "VPC" 옵션을 선택하고 CloudFormation 스택에서 생성한 VPC를 선택합니다. 그런 다음 "서브넷" 옵션을 선택하고 CloudFormation 스택에서 생성한 두 개의 서브넷을 선택합니다.

![](https://i.imgur.com/7DpjTGi.png)

이제 Kubernetes 클러스터 엔드포인트 액세스 유형을 선택해야 합니다. "공개" 옵션을 선택합니다.

![](https://i.imgur.com/DY0b4oI.png)

다음으로 보안 그룹을 구성해야 합니다. "보안 그룹" 옵션을 선택하고 CloudFormation 스택에서 생성한 보안 그룹을 선택합니다.

![](https://i.imgur.com/4JcM0Ss.png)

이제 Kubernetes 클러스터 로깅 유형을 선택해야 합니다. "Amazon CloudWatch" 옵션을 선택합니다.

![](https://i.imgur.com/BkzM0Ss.png)

다음으로 Kubernetes 클러스터 모니터링 유형을 선택해야 합니다. "Amazon CloudWatch" 옵션을 선택합니다.

![](https://i.imgur.com/nALDKQi.png)

이제 Kubernetes 클러스터 암호화 유형을 선택해야 합니다. "AES-256" 옵션을 선택합니다.

![](https://i.imgur.com/p0bJUO4.png)

이제 Kubernetes 클러스터 자동 확장 그룹 유형을 선택해야 합니다. "AsgBasedAutoScaling" 옵션을 선택합니다.

![](https://i.imgur.com/FkzM0Ss.png)

이제 작업자 노드 Auto-Scaling 그룹을 구성해야 합니다. "WorkerNodesAsg" 옵션을 선택하고 CloudFormation 스택에서 생성한 자동 확장 그룹을 선택합니다.

![](https://i.imgur.com/VkzM0Ss.png)

이제 Kubernetes 클러스터 확장 구성 유형을 선택해야 합니다. "기본값" 옵션을 선택합니다.

![](https://i.imgur.com/p0bJUO4.png)

다음 페이지에서 클러스터 구성을 검토하고 "클러스터 만들기" 버튼을 클릭합니다.

![](https://i.imgur.com/LDAd5u8.png)

다음 페이지에서 클러스터가 생성되는 것을 볼 수 있습니다. 이 작업은 몇 분 정도 소요됩니다.

![](https://i.imgur.com/W0Qiu8D.png)

클러스터가 생성되면 "kubectl 구성" 버튼을 클릭하여 클러스터와 통신하도록 kubectl 명령줄 도구를 구성할 수 있습니다.

![](https://i.imgur.com/nALDKQi.png)

다음 페이지에서 "구성 다운로드" 버튼을 클릭합니다.

![](https://i.imgur.com/7DpjTGi.png)

이렇게 하면 kubeconfig 파일이 컴퓨터에 다운로드됩니다. 이 파일을 ~/.kube 디렉터리로 이동하고 이름을 config로 바꿉니다.

이제 다음 명령을 실행하여 클러스터가 작동하는지 테스트할 수 있습니다.

```
kubectl get svc
```

모든 것이 올바르게 작동하면 클러스터에 서비스 목록이 표시되어야 합니다.

## Kubernetes 클러스터에 애플리케이션 배포

이제 Kubernetes 클러스터가 가동되어 실행 중이므로 여기에 애플리케이션을 배포할 수 있습니다. 이 예에서는 Go로 작성된 간단한 "Hello World" 애플리케이션을 배포합니다.

먼저 애플리케이션을 위한 Dockerfile을 생성해야 합니다. 다음 내용으로 프로젝트의 루트에 "Dockerfile"이라는 파일을 만듭니다.

```
FROM golang:1.13-alpine

RUN mkdir /app

ADD . /app/

WORKDIR /app

RUN go build -o main .

CMD ["/app/main"]
```

다음으로 애플리케이션 코드를 작성해야 합니다. 다음 내용으로 프로젝트의 루트에 "main.go"라는 파일을 만듭니다.

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello World!")
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}
```

이제 Docker 이미지를 빌드하고 Docker 레지스트리에 푸시할 수 있습니다. Docker 레지스트리에 Amazon ECR을 사용합니다.

먼저 Amazon ECR에서 새 리포지토리를 생성해야 합니다. Amazon ECR 콘솔에 로그인하고 "리포지토리 생성" 버튼을 클릭합니다.

![](https://i.imgur.com/tY0NVT3.png)

다음 페이지에서 리포지토리 이름을 입력하고 "리포지토리 생성" 버튼을 클릭합니다.

![](https://i.imgur.com/nALDKQi.png)

이제 Docker 이미지를 빌드하고 새 리포지토리로 푸시할 수 있습니다.

다음 명령을 실행하여 Docker 이미지를 빌드하고 푸시합니다.

```
$ docker build -t {your_aws_account_id}.dkr.ecr.{your_region}.amazonaws.com/{your_repository_name} .

$ docker push {your_aws_account_id}.dkr.ecr.{your_region}.amazonaws.com/{your_repository_name}
```

{your_aws_account_id}, {your_region} 및 {your_repository_name}을 계정 및 리포지토리에 적합한 값으로 바꿉니다.

이제 Docker 이미지가 리포지토리로 푸시되었으므로 Kubernetes 클러스터에 배포할 수 있습니다.

먼저 배포 파일을 만들어야 합니다. 다음 내용으로 프로젝트의 루트에 "deployment.yaml"이라는 파일을 만듭니다.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hello-world
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
        image: {your_aws_account_id}.dkr.ecr.{your_region}.amazonaws.com/{your_repository_name}
        ports:
        - containerPort: 8080
```

{your_aws_account_id}, {your_region} 및 {your_repository_name}을 계정 및 리포지토리에 적합한 값으로 바꿉니다.

이제 다음 명령을 실행하여 Kubernetes 클러스터에 애플리케이션을 배포할 수 있습니다.

```
kubectl apply -f deployment.yaml
```

이렇게 하면 3개의 복제본이 있는 "hello-world"라는 배포가 생성됩니다.

실제 배치를 보려면 이를 외부 세계에 노출해야 합니다. 서비스를 생성하여 이를 수행할 수 있습니다.

먼저 서비스 파일을 생성해야 합니다. 다음 내용으로 프로젝트의 루트에 "service.yaml"이라는 파일을 만듭니다.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: hello-world
spec:
  type: LoadBalancer
  ports:
  - port: 80
    protocol: TCP
    targetPort: 8080
  selector:
    app: hello-world
```

이제 다음 명령을 실행하여 서비스를 배포할 수 있습니다.

```
kubectl apply -f service.yaml
```

이렇게 하면 "LoadBalancer" 유형의 "hello-world"라는 서비스가 생성됩니다. 이러한 유형의 서비스는 AWS에서 로드 밸런서를 생성하고 배포를 외부 세계에 노출합니다.

로드 밸런서의 URL을 찾으려면 다음 명령을 실행하십시오.

```
kubectl get svc hello-world
```

다음과 유사한 출력이 표시되어야 합니다.

```
NAME           TYPE           CLUSTER-IP      EXTERNAL-IP                                                              PORT(S)        AGE
hello-world    LoadBalancer   10.100.200.16   aaa.bbb.ccc.ddd   80:32000/TCP,443:31943/TCP   5m29s
```

"EXTERNAL-IP" 값은 로드 밸런서의 URL입니다.

## Kubernetes 클러스터 삭제

Kubernetes 클러스터를 삭제하려는 경우 Amazon EKS 콘솔에서 삭제할 수 있습니다.

먼저 Amazon EKS 콘솔에 로그인하고 "클러스터" 페이지로 이동합니다.

![](https://i.imgur.com/LDAd5u8.png)

다음 페이지에서 삭제하려는 클러스터 옆의 확인란을 선택하고 "삭제" 버튼을 클릭합니다.

![](https://i.imgur.com/7DpjTGi.png)

다음 페이지에서 "클러스터 이름" 필드에 클러스터 이름을 입력하고 "클러스터 삭제" 버튼을 클릭합니다.

![](https://i.imgur.com/p0bJUO4.png)

## 결론

이 기사에서는 AWS에 Kubernetes 클러스터를 배포하는 방법을 설명했습니다. 또한 클러스터에 애플리케이션을 배포하는 방법도 보여 주었습니다.

Kubernetes에 대해 자세히 알아보려면 다음 리소스를 권장합니다.

- 쿠버네티스 공식 문서: https://kubernetes.io/docs/

- 공식 Amazon EKS 문서: https://docs.aws.amazon.com/eks/latest/userguide/what-is-eks.html

- 공식 Amazon ECR 문서: https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html