---
title: AWS CloudFormation: 클라우드 인프라 배포 자동화
description: 
published: true
date: 2023-02-19T02:32:50.365Z
tags: 
editor: markdown
dateCreated: 2023-02-19T02:32:48.970Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS CloudFormation: Automating Cloud Infrastructure Deployment***English** document is available*](/en/Knowledge-base/Cloud/aws-cloudformation-automating-cloud-infrastructure-deployment)
{.links-list}


# AWS CloudFormation: 클라우드 인프라 배포 자동화

CloudFormation은 개발자가 클라우드 인프라의 생성 및 배포를 자동화할 수 있는 강력한 AWS 서비스입니다. 이 기사에서는 CloudFormation이 무엇이며 이를 사용하여 클라우드 리소스 프로비저닝 및 관리 프로세스를 단순화하는 방법에 대해 자세히 살펴보겠습니다.

## CloudFormation이란 무엇입니까?

CloudFormation은 개발자가 JSON 또는 YAML로 작성된 템플릿을 사용하여 클라우드 인프라를 정의하고 프로비저닝할 수 있는 서비스입니다. 템플릿이 정의되면 CloudFormation을 사용하여 해당 템플릿을 기반으로 리소스 스택을 생성, 업데이트 및 삭제할 수 있습니다.

CloudFormation 사용의 이점 중 하나는 인프라를 코드로 정의할 수 있다는 것입니다. 이는 인프라가 다른 코드 리소스와 마찬가지로 버전 관리, 추적 및 자동화될 수 있음을 의미합니다.

CloudFormation의 또 다른 이점은 여러 AWS 계정 및 지역에 걸쳐 리소스를 프로비저닝하는 데 사용할 수 있다는 것입니다. 이는 개발, 테스트 및 프로덕션 환경을 위한 리소스를 관리할 때 유용할 수 있습니다.

## CloudFormation 템플릿 기본 사항

CloudFormation 템플릿은 AWS 리소스 스택을 정의하는 JSON 또는 YAML 문서입니다. 템플릿은 여러 리소스를 포함할 수 있으며 각 리소스는 단순 또는 중첩 형식을 사용하여 정의할 수 있습니다.

단순 형식 리소스는 단일 JSON 또는 YAML 개체로 정의됩니다. 이 객체는 만들 리소스의 유형을 지정하는 Type 속성과 리소스의 속성을 정의하는 Properties 속성을 포함해야 합니다.

중첩된 형식 리소스는 Type 속성 및 Properties 속성과 NestedStackId 속성을 포함하는 JSON 또는 YAML 객체로 정의됩니다. NestedStackId 속성에는 다른 스택 내에 생성된 스택인 중첩 스택의 스택 ID가 포함됩니다.

## CloudFormation 스택 생성

CloudFormation 템플릿이 정의되면 이를 사용하여 새 스택을 생성할 수 있습니다. 스택을 생성하려면 스택 이름, 템플릿 URL 및 매개변수 집합을 지정해야 합니다.

스택 이름은 스택을 고유하게 식별하는 데 사용됩니다. 템플릿 URL은 템플릿 파일의 위치입니다. 템플릿 파일은 Amazon S3 버킷에 저장하거나 인라인일 수 있습니다.

매개변수는 스택을 구성하는 데 사용되는 키-값 쌍 세트입니다. 템플릿에서 키를 지정해야 하며 스택이 생성될 때 값을 제공해야 합니다.

스택이 생성되면 CloudFormation은 템플릿에 정의된 리소스를 프로비저닝합니다. 이 프로세스를 완료하는 데 몇 분 정도 걸릴 수 있습니다.

## CloudFormation 스택 업데이트

스택이 생성되면 업데이트할 수 있습니다. 스택을 업데이트하려면 새 템플릿 URL과 매개변수 집합을 지정해야 합니다.

스택을 업데이트하면 CloudFormation은 먼저 새 템플릿을 기존 템플릿과 비교합니다. 변경 사항이 없으면 CloudFormation은 아무 작업도 수행하지 않습니다. 변경 사항이 있으면 CloudFormation이 스택을 업데이트합니다.

## CloudFormation 스택 삭제

스택이 더 이상 필요하지 않으면 삭제할 수 있습니다. 스택을 삭제하면 스택에 정의된 모든 리소스가 삭제됩니다.

## CloudFormation 사용 사례

CloudFormation은 거의 모든 유형의 AWS 리소스를 프로비저닝하는 데 사용할 수 있습니다. CloudFormation의 몇 가지 일반적인 사용 사례는 다음과 같습니다.

- 가상 사설 클라우드(VPC) 생성
- Amazon EC2 인스턴스 시작
- Amazon RDS 데이터베이스 생성
- Amazon S3 버킷 생성

## CloudFormation 템플릿 예제

다음은 일반적인 AWS 리소스를 프로비저닝하는 데 사용할 수 있는 CloudFormation 템플릿의 몇 가지 예입니다.

### VPC 생성

이 템플릿을 사용하여 퍼블릭 및 프라이빗 서브넷이 있는 VPC를 생성할 수 있습니다.

```yaml
AWSTemplateFormatVersion: 2010-09-09

Description: A VPC with a public and private subnet.

Parameters:

  VpcCidr:
    Description: The CIDR block for the VPC.
    Type: String
    Default: 172.16.0.0/16

  PublicSubnet1Cidr:
    Description: The CIDR block for the public subnet.
    Type: String
    Default: 172.16.0.0/24

  PrivateSubnet1Cidr:
    Description: The CIDR block for the private subnet.
    Type: String
    Default: 172.16.1.0/24

Resources:

  Vpc:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: !Ref VpcCidr
      InstanceTenancy: default

  PublicSubnet1:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref Vpc
      CidrBlock: !Ref PublicSubnet1Cidr
      AvailabilityZone: us-east-1a

  PrivateSubnet1:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref Vpc
      CidrBlock: !Ref PrivateSubnet1Cidr
      AvailabilityZone: us-east-1a
```

### EC2 인스턴스 생성

이 템플릿은 EC2 인스턴스를 시작하는 데 사용할 수 있습니다.

```yaml
AWSTemplateFormatVersion: 2010-09-09

Description: A simple EC2 instance.

Parameters:

  KeyName:
    Description: The name of the SSH key pair to use.
    Type: String

  InstanceType:
    Description: The type of EC2 instance to launch.
    Type: String
    Default: t2.micro

  ImageId:
    Description: The ID of the AMI to use.
    Type: String

Resources:

  Ec2Instance:
    Type: AWS::EC2::Instance
    Properties:
      KeyName: !Ref KeyName
      InstanceType: !Ref InstanceType
      ImageId: !Ref ImageId
```

### RDS 데이터베이스 생성

이 템플릿을 사용하여 RDS 데이터베이스를 생성할 수 있습니다.

```yaml
AWSTemplateFormatVersion: 2010-09-09

Description: A simple RDS database.

Parameters:

  DbInstanceIdentifier:
    Description: The database instance identifier.
    Type: String

  DbInstanceClass:
    Description: The database instance class.
    Type: String
    Default: db.t2.micro

  DbName:
    Description: The database name.
    Type: String

Resources:

  DbInstance:
    Type: AWS::RDS::DBInstance
    Properties:
      DbInstanceIdentifier: !Ref DbInstanceIdentifier
      DbInstanceClass: !Ref DbInstanceClass
      Engine: MySQL
      MasterUsername: root
      MasterUserPassword: password
      AllocatedStorage: 5
      DbName: !Ref DbName
```

### S3 버킷 생성

이 템플릿을 사용하여 S3 버킷을 생성할 수 있습니다.

```yaml
AWSTemplateFormatVersion: 2010-09-09

Description: A simple S3 bucket.

Parameters:

  BucketName:
    Description: The name of the S3 bucket.
    Type: String

Resources:

  Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: !Ref BucketName
```

## 결론

CloudFormation은 개발자가 클라우드 인프라의 생성 및 배포를 자동화할 수 있는 강력한 AWS 서비스입니다. 이 기사에서는 CloudFormation이 무엇이며 이를 사용하여 클라우드 리소스 프로비저닝 및 관리 프로세스를 간소화하는 방법에 대해 자세히 살펴보았습니다.