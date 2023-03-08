---
title: AWS Elastic Beanstalk: 간단한 웹 애플리케이션 배포 및 확장
description: 
published: true
date: 2023-02-09T12:18:12.562Z
tags: 
editor: markdown
dateCreated: 2023-02-09T12:18:10.840Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS Elastic Beanstalk: Deploying and Scaling a Simple Web Application***English** document is available*](/en/Knowledge-base/Cloud/aws-elastic-beanstalk-deploying-and-scaling-a-simple-web-application)
{.links-list}


# AWS Elastic Beanstalk: 간단한 웹 애플리케이션 배포 및 확장

AWS Elastic Beanstalk는 Java, .NET, PHP, Node.js, Python, Ruby on Rails 및 Docker on AWS와 같은 널리 사용되는 웹 애플리케이션 프레임워크로 개발된 웹 애플리케이션 및 서비스를 배포하고 확장하기 위한 사용하기 쉬운 서비스입니다.

Elastic Beanstalk는 Amazon EC2 인스턴스, 로드 밸런서 및 Auto Scaling 그룹과 같은 웹 애플리케이션의 기본 리소스를 관리하는 복잡성을 줄여줍니다. 또한 웹 애플리케이션의 상태와 성능을 모니터링하기 위한 통합 환경을 제공합니다.

이 기사에서는 AWS Elastic Beanstalk에서 간단한 웹 애플리케이션을 배포하는 방법을 보여줍니다. 또한 웹 애플리케이션을 수평(Amazon EC2 인스턴스 추가) 및 수직(Amazon EC2 인스턴스 크기 증가)으로 확장하는 것이 얼마나 쉬운지 보여줍니다.

## 전제 조건

시작하기 전에 다음이 필요합니다.

* AWS 계정. 없는 경우 [여기](https://aws.amazon.com/getting-started/)에서 무료로 만들 수 있습니다.
* Amazon EC2 인스턴스에 배포할 수 있는 웹 애플리케이션입니다. 이 기사에서는 간단한 Node.js 웹 애플리케이션을 사용합니다.
* 웹 애플리케이션의 소스 코드를 저장하는 Amazon S3 버킷.

## AWS Elastic Beanstalk에 웹 애플리케이션 배포

AWS Elastic Beanstalk에 웹 애플리케이션을 배포하려면 Elastic Beanstalk 환경을 생성하고 애플리케이션의 소스 코드를 Amazon S3 버킷에 업로드합니다. 그런 다음 Elastic Beanstalk는 Amazon EC2 인스턴스를 생성하고 여기에 웹 애플리케이션을 로드하고 트래픽을 처리하도록 구성합니다.

### Elastic Beanstalk 환경 만들기

Elastic Beanstalk 환경을 생성하려면 Elastic Beanstalk 콘솔을 열고 "Create New Application"을 클릭합니다.

![새 애플리케이션 생성](https://i.imgur.com/lpY7B0m.png)

애플리케이션 이름을 입력하고 "만들기"를 클릭합니다.

![응용 프로그램 이름 입력](https://i.imgur.com/fvqQYxo.png)

다음 페이지에서 사용하려는 웹 서버 플랫폼을 선택합니다. 이 문서에서는 "Node.js"를 사용합니다.

![플랫폼 선택](https://i.imgur.com/LJNcuAO.png)

다음 페이지에서 사용하려는 Amazon EC2 인스턴스 유형을 선택합니다. 이 문서에서는 "t2.micro" 인스턴스 유형을 사용합니다.

![select-ec2-instance-type](https://i.imgur.com/VkzM8JZ.png)

다음 페이지에서 웹 애플리케이션의 소스 코드를 저장하는 데 사용할 Amazon S3 버킷을 선택합니다.

![select-s3-bucket](https://i.imgur.com/y4FtJjl.png)

"배포"를 클릭하여 AWS Elastic Beanstalk에 웹 애플리케이션을 배포합니다.

![배포-응용 프로그램](https://i.imgur.com/BKW738u.png)

Elastic Beanstalk는 이제 Amazon EC2 인스턴스를 생성하고 여기에 웹 애플리케이션을 로드하고 트래픽을 처리하도록 구성합니다.

### 애플리케이션의 소스 코드를 Amazon S3에 업로드

이제 Elastic Beanstalk 환경을 만들었으므로 선택한 Amazon S3 버킷에 웹 애플리케이션의 소스 코드를 업로드해야 합니다.

이렇게 하려면 Amazon S3 콘솔을 열고 사용할 버킷을 선택합니다. 그런 다음 "업로드" 버튼을 클릭합니다.

![업로드 버튼](https://i.imgur.com/TXrQ8oA.png)

다음 페이지에서 업로드할 파일을 선택하고 "업로드"를 클릭합니다.

![업로드할 파일 선택](https://i.imgur.com/F3gG0CY.png)

이제 웹 애플리케이션의 소스 코드가 Amazon S3 버킷에 저장됩니다.

## 웹 애플리케이션 액세스

웹 애플리케이션이 AWS Elastic Beanstalk에 배포되면 환경의 URL로 이동하여 액세스할 수 있습니다.

환경의 URL을 찾으려면 Elastic Beanstalk 콘솔을 열고 생성한 환경을 클릭합니다. 그런 다음 "개요" 탭을 클릭합니다. 환경의 URL은 페이지 상단에 표시됩니다.

![환경-URL](https://i.imgur.com/vzMJO4F.png)

## 웹 애플리케이션 확장

AWS Elastic Beanstalk를 사용하면 웹 애플리케이션을 수평(Amazon EC2 인스턴스 추가) 및 수직(Amazon EC2 인스턴스 크기 증가)으로 쉽게 확장할 수 있습니다.

웹 애플리케이션을 수평으로 확장하려면 Elastic Beanstalk 콘솔을 열고 생성한 환경을 클릭합니다. 그런 다음 "구성" 탭을 클릭합니다.

![구성 탭](https://i.imgur.com/J3GfUxz.png)

다음 페이지에서 "용량" 탭을 클릭합니다.

![용량 탭](https://i.imgur.com/pLJgJw6.png)

다음 페이지에서 사용하려는 Amazon EC2 인스턴스 수를 선택하고 "적용"을 클릭합니다.

![인스턴스 선택 수](https://i.imgur.com/X3XWqlr.png)

Elastic Beanstalk는 이제 원하는 수의 Amazon EC2 인스턴스를 환경에 추가합니다.

웹 애플리케이션을 세로로 확장하려면 Elastic Beanstalk 콘솔을 열고 생성한 환경을 클릭합니다. 그런 다음 "구성" 탭을 클릭합니다.

![구성 탭](https://i.imgur.com/J3GfUxz.png)

다음 페이지에서 "용량" 탭을 클릭합니다.

![용량 탭](https://i.imgur.com/pLJgJw6.png)

다음 페이지에서 사용하려는 Amazon EC2 인스턴스 유형을 선택하고 "적용"을 클릭합니다.

![select-ec2-instance-type](https://i.imgur.com/IHLv4jO.png)

Elastic Beanstalk는 이제 원하는 Amazon EC2 인스턴스 유형을 사용하도록 환경을 재구성합니다.

## 웹 애플리케이션 모니터링

AWS Elastic Beanstalk는 웹 애플리케이션의 상태 및 성능을 모니터링하기 위한 통합 환경을 제공합니다.

웹 애플리케이션의 상태 및 성능 지표를 보려면 Elastic Beanstalk 콘솔을 열고 생성한 환경을 클릭하십시오. 그런 다음 "모니터링" 탭을 클릭합니다.

![모니터링 탭](https://i.imgur.com/VxKG0zJ.png)

다음 페이지에는 요청 수, 응답 시간 및 CPU 사용률과 같은 웹 애플리케이션에 대한 다양한 메트릭이 포함된 대시보드가 표시됩니다.

![모니터링-대시보드](https://i.imgur.com/ZDGxK5M.png)

웹 애플리케이션의 액세스 로그 및 오류 로그를 볼 수도 있습니다. 이렇게 하려면 Elastic Beanstalk 콘솔을 열고 생성한 환경을 클릭합니다. 그런 다음 "로그" 탭을 클릭합니다.

![로그 탭](https://i.imgur.com/D4Y4lkO.png)

다음 페이지에는 웹 애플리케이션의 액세스 로그 및 오류 로그 목록이 표시됩니다.

![로그](https://i.imgur.com/rAFwUOI.png)

## 웹 애플리케이션 업데이트

웹 애플리케이션을 업데이트하려면 웹 애플리케이션 소스 코드의 업데이트된 버전을 사용 중인 Amazon S3 버킷에 업로드하기만 하면 됩니다. Elastic Beanstalk는 변경 사항을 자동으로 감지하고 웹 애플리케이션의 업데이트된 버전을 배포합니다.

## 웹 애플리케이션 삭제

웹 애플리케이션을 삭제하려면 Elastic Beanstalk 콘솔을 열고 생성한 환경을 클릭합니다. 그런 다음 "작업" 드롭다운 메뉴를 클릭하고 "환경 삭제"를 선택합니다.

![환경 삭제](https://i.imgur.com/VxJN4jO.png)

다음 페이지에서 삭제하려는 환경의 이름을 입력하고 "삭제"를 클릭합니다.

![환경 이름 입력](https://i.imgur.com/uvaYG4Y.png)

이제 Elastic Beanstalk에서 웹 애플리케이션을 삭제합니다.

## 결론

이 기사에서는 AWS Elastic Beanstalk에서 간단한 웹 애플리케이션을 배포하는 방법을 보여주었습니다. 또한 웹 애플리케이션을 수평(Amazon EC2 인스턴스 추가) 및 수직(Amazon EC2 인스턴스 크기 증가)으로 확장하는 것이 얼마나 쉬운지 보여주었습니다. 마지막으로 웹 애플리케이션의 상태와 성능을 모니터링하는 방법도 보여 주었습니다.