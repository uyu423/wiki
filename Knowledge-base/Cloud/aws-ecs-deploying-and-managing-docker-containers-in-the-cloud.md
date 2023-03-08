---
title: AWS ECS: 클라우드에서 Docker 컨테이너 배포 및 관리
description: 
published: true
date: 2023-02-16T00:17:54.070Z
tags: 
editor: markdown
dateCreated: 2023-02-16T00:17:51.794Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS ECS: Deploying and Managing Docker Containers in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-ecs-deploying-and-managing-docker-containers-in-the-cloud)
{.links-list}


# AWS ECS: 클라우드에서 Docker 컨테이너 배포 및 관리

Docker 컨테이너는 최근 몇 년 동안 애플리케이션 패키징 및 배포의 표준이 되었습니다. 이동성, 리소스 오버헤드 감소, CI/CD(지속적인 통합/지속적인 전달) 파이프라인과의 손쉬운 통합 등 기존 가상 머신에 비해 많은 이점을 제공합니다.

AWS Elastic Container Service(ECS)는 클라우드에서 Docker 컨테이너를 쉽게 실행하고 관리할 수 있게 해주는 관리형 컨테이너 오케스트레이션 서비스입니다. 이 기사에서는 AWS ECS에서 Docker 컨테이너를 배포하고 관리하는 방법을 살펴보겠습니다.

## ECS 클러스터 생성

AWS ECS를 사용하는 첫 번째 단계는 ECS 클러스터를 생성하는 것입니다. ECS 클러스터는 Docker 컨테이너를 호스팅하는 데 사용되는 EC2 인스턴스의 논리적 그룹입니다. AWS Management Console, AWS 명령줄 인터페이스(CLI) 또는 AWS SDK를 사용하여 ECS 클러스터를 생성할 수 있습니다.

### AWS Management Console을 사용하여 ECS 클러스터 생성

AWS Management Console을 사용하여 ECS 클러스터를 생성하려면 먼저 Amazon ECS 콘솔을 열고 왼쪽 탐색에서 "클러스터" 링크를 선택합니다. 그런 다음 "클러스터 만들기" 버튼을 클릭합니다.

"클러스터 만들기" 페이지에서 "네트워킹 전용" 템플릿을 선택하고 클러스터 이름을 지정합니다. 그런 다음 "만들기" 버튼을 클릭합니다.

이제 클러스터가 생성되고 "클러스터" 목록에서 볼 수 있습니다.

### AWS CLI를 사용하여 ECS 클러스터 생성

AWS CLI를 사용하여 ECS 클러스터를 생성하려면 먼저 다음 내용으로 "ecs-cli-cluster.json"이라는 파일을 생성합니다.

```json
{
    "clusterName": "my-ecs-cluster",
    "networkConfiguration": {
        "awsvpcConfiguration": {
            "subnets": [
                "subnet-12345678",
                "subnet-87654321"
            ],
            "securityGroups": [
                "sg-12345678"
            ],
            "associatePublicIpAddress": true
        }
    }
}
```

"clusterName", "subnets" 및 "securityGroups" 필드의 값을 환경에 적합한 값으로 바꿉니다. 그런 다음 다음 명령을 실행하여 클러스터를 생성합니다.

```
aws ecs create-cluster --cli-input-json file://ecs-cli-cluster.json
```

## ECS 작업 정의 생성

이제 ECS 클러스터가 있으므로 여기에 애플리케이션을 배포할 수 있습니다. ECS의 애플리케이션은 애플리케이션을 실행하는 데 필요한 Docker 이미지 및 기타 리소스를 지정하는 작업 정의로 정의됩니다.

AWS Management 콘솔, AWS CLI 또는 AWS SDK를 사용하여 작업 정의를 생성할 수 있습니다.

### AWS Management Console을 사용하여 작업 정의 생성

AWS Management Console을 사용하여 작업 정의를 생성하려면 먼저 Amazon ECS 콘솔을 열고 왼쪽 탐색에서 "Task Definitions" 링크를 선택합니다. 그런 다음 "새 작업 정의 만들기" 버튼을 클릭합니다.

"시작 유형 선택" 페이지에서 "EC2" 시작 유형을 선택하고 "다음 단계" 버튼을 클릭합니다.

"작업 및 컨테이너 정의 구성" 페이지에서 작업 이름과 설명을 지정합니다. 그런 다음 "컨테이너 정의" 섹션까지 아래로 스크롤하고 "컨테이너 추가" 버튼을 클릭합니다.

"컨테이너 추가" 모달에서 다음 값을 입력합니다.

- **컨테이너 이름:** my-container
- **이미지:** nginx:최신
- **메모리 제한(MiB):** 512
- **포트 매핑:** 80:80

그런 다음 "추가" 버튼을 클릭합니다.

이제 컨테이너가 작업 정의에 추가됩니다. "작업 역할" 섹션까지 아래로 스크롤하고 "없음" 옵션을 선택합니다. 그런 다음 "네트워크 모드" 섹션까지 아래로 스크롤하고 "브리지" 옵션을 선택합니다. 마지막으로 "다음 단계" 버튼을 클릭합니다.

"검토" 페이지에서 작업 정의를 검토하고 "만들기" 버튼을 클릭합니다.

이제 작업 정의가 생성되고 "작업 정의" 목록에서 볼 수 있습니다.

### AWS CLI를 사용하여 작업 정의 생성

AWS CLI를 사용하여 작업 정의를 생성하려면 먼저 다음 내용으로 "ecs-cli-task-definition.json"이라는 파일을 생성합니다.

```json
{
    "family": "my-task-definition",
    "networkMode": "bridge",
    "containerDefinitions": [
        {
            "name": "my-container",
            "image": "nginx:latest",
            "memory": 512,
            "portMappings": [
                {
                    "containerPort": 80,
                    "hostPort": 80
                }
            ]
        }
    ]
}
```

"family" 및 "containerDefinitions" 필드의 값을 환경에 적합한 값으로 바꿉니다. 그런 다음 다음 명령을 실행하여 작업 정의를 생성합니다.

```
aws ecs register-task-definition --cli-input-json file://ecs-cli-task-definition.json
```

## ECS 클러스터에 애플리케이션 배포

이제 ECS 클러스터와 작업 정의가 있으므로 애플리케이션을 클러스터에 배포할 수 있습니다. AWS Management Console, AWS CLI 또는 AWS SDK를 사용하여 ECS 클러스터에 애플리케이션을 배포할 수 있습니다.

### AWS Management Console을 사용하여 애플리케이션 배포

AWS Management Console을 사용하여 애플리케이션을 배포하려면 먼저 Amazon ECS 콘솔을 열고 왼쪽 탐색에서 "클러스터" 링크를 선택합니다. 그런 다음 배포할 클러스터를 선택하고 "작업" 탭을 클릭합니다.

"작업" 탭에서 "새 작업 실행" 버튼을 클릭합니다.

"작업 및 컨테이너 설정 구성" 페이지에서 "my-task-definition" 작업 정의를 선택하고 "다음 단계" 버튼을 클릭합니다.

"네트워크 구성" 페이지에서 "브리지" 네트워크 모드를 선택하고 "다음 단계" 버튼을 클릭합니다.

"검토" 페이지에서 작업 설정을 검토하고 "작업 실행" 버튼을 클릭합니다.

이제 작업이 클러스터에 배포되고 "작업" 탭에서 해당 상태를 볼 수 있습니다.

### AWS CLI를 사용하여 애플리케이션 배포

AWS CLI를 사용하여 애플리케이션을 배포하려면 먼저 다음 내용으로 "ecs-cli-run-task.json"이라는 파일을 생성합니다.

```json
{
    "taskDefinition": "my-task-definition",
    "networkConfiguration": {
        "awsvpcConfiguration": {
            "subnets": [
                "subnet-12345678",
                "subnet-87654321"
            ],
            "securityGroups": [
                "sg-12345678"
            ],
            "associatePublicIpAddress": true
        }
    }
}
```

"taskDefinition", "subnets" 및 "securityGroups" 필드의 값을 환경에 적합한 값으로 바꿉니다. 그런 다음 다음 명령을 실행하여 작업을 배포합니다.

```
aws ecs run-task --cli-input-json file://ecs-cli-run-task.json
```

## ECS 클러스터 모니터링

AWS ECS는 클러스터와 클러스터에서 실행 중인 작업을 모니터링하기 위한 다양한 도구를 제공합니다.

첫 번째 도구는 CloudWatch입니다. CloudWatch는 ECS 클러스터를 포함한 AWS 리소스에 대한 모니터링 데이터를 수집하고 처리하는 AWS 서비스입니다. CloudWatch를 사용하여 ECS 클러스터에 대한 지표를 보고, 경보를 설정하고, 로그를 볼 수 있습니다.

두 번째 도구는 Amazon CloudWatch Logs입니다. CloudWatch Logs는 ECS 클러스터를 비롯한 AWS 리소스의 로그 파일을 모니터링, 저장 및 액세스하는 데 사용할 수 있는 서비스입니다. CloudWatch Logs를 사용하여 ECS 클러스터 및 여기에서 실행 중인 작업에 대한 로그를 볼 수 있습니다.

세 번째 도구는 Amazon CloudWatch Events입니다. CloudWatch Events는 ECS 클러스터를 비롯한 AWS 리소스의 이벤트를 모니터링하는 데 사용할 수 있는 서비스입니다. CloudWatch 이벤트를 사용하여 ECS 클러스터에 대한 이벤트와 클러스터에서 실행 중인 작업을 볼 수 있습니다.

## ECS 클러스터 삭제

ECS 클러스터가 더 이상 필요하지 않으면 AWS Management Console, AWS CLI 또는 AWS SDK를 사용하여 삭제할 수 있습니다.

### AWS Management 콘솔을 사용하여 ECS 클러스터 삭제

AWS Management 콘솔을 사용하여 ECS 클러스터를 삭제하려면 먼저 Amazon ECS 콘솔을 열고 왼쪽 탐색에서 "클러스터" 링크를 선택하십시오. 그런 다음 삭제할 클러스터를 선택하고 "삭제" 버튼을 클릭합니다.

"클러스터 삭제" 페이지에서 클러스터에 대한 정보를 검토하고 "삭제" 버튼을 클릭합니다.

이제 클러스터가 삭제됩니다.

### AWS CLI를 사용하여 ECS 클러스터 삭제

AWS CLI를 사용하여 ECS 클러스터를 삭제하려면 다음 명령을 실행합니다.

```
aws ecs delete-cluster --cluster my-ecs-cluster
```

## 결론

이 기사에서는 AWS ECS에서 Docker 컨테이너를 배포하고 관리하는 방법을 살펴보았습니다. ECS 클러스터를 생성하고, 작업 정의를 생성하고, 클러스터에 애플리케이션을 배포하는 방법을 살펴보았습니다. 또한 CloudWatch를 사용하여 ECS 클러스터를 모니터링하는 방법도 살펴보았습니다. 마지막으로 ECS 클러스터를 삭제하는 방법을 살펴보았습니다.