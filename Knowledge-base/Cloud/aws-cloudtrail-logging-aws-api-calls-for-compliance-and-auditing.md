---
title: AWS CloudTrail: 규정 준수 및 감사를 위해 AWS API 호출 로깅
description: 
published: true
date: 2023-02-05T07:56:03.204Z
tags: 
editor: markdown
dateCreated: 2023-02-05T07:56:01.428Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS CloudTrail: Logging AWS API Calls for Compliance and Auditing***English** document is available*](/en/Knowledge-base/Cloud/aws-cloudtrail-logging-aws-api-calls-for-compliance-and-auditing)
{.links-list}


AWS CloudTrail은 AWS API 호출을 기록하고 로그 파일을 전달하는 웹 서비스입니다. CloudTrail은 AWS Management Console, AWS SDK, 명령줄 도구 및 기타 AWS 서비스를 통해 수행된 작업을 포함하여 AWS 계정 활동의 이벤트 기록을 제공합니다. 이 이벤트 기록은 보안 분석, 리소스 변경 추적 및 규정 준수 감사를 단순화합니다.

CloudTrail은 설정하기 쉽습니다. 데이터를 Amazon S3 버킷, Amazon CloudWatch Logs 로그 그룹 또는 둘 다에 기록하거나 둘 다에 기록하지 않는 추적을 생성할 수 있습니다. 동일한 Amazon S3 버킷 또는 Amazon CloudWatch Logs 로그 그룹에 데이터를 전달하도록 여러 추적을 구성할 수 있습니다. AWS CloudTrail을 구성할 때 CloudTrail이 로그 파일을 전달할 Amazon S3 버킷 또는 Amazon CloudWatch Logs 로그 그룹을 지정합니다.

 추적은 AWS 계정의 모든 AWS 리전 또는 선택한 리전의 데이터를 기록할 수 있습니다. AWS 계정의 모든 리전에 대해 로깅을 활성화하거나 선택한 리전에 대해서만 로깅을 활성화할 수 있습니다. CloudTrail 로깅을 위해 리전을 활성화하면 CloudTrail이 해당 리전에 새 추적을 생성합니다.

## CloudTrail 설정

AWS 계정에 대한 로깅을 켜려면 추적을 생성하십시오. 트레일은 CloudTrail을 활성화하고 CloudTrail 로그 파일의 전달 방법을 지정합니다. AWS 계정의 모든 리전에 대해 또는 선택한 리전에 대해서만 데이터 이벤트를 기록하는 추적을 생성할 수 있습니다. 추적이 AWS 계정의 리소스에만 적용되는지 아니면 모든 AWS 리소스에 적용되는지 구성할 수도 있습니다. 추적을 생성하면 AWS CloudTrail 콘솔에서 거의 실시간으로 로그 파일을 보고 검색할 수 있습니다.

### 트레일 만들기

다음 절차를 사용하여 추적을 생성하고 CloudTrail이 로그 파일을 전달할 Amazon S3 버킷 또는 Amazon CloudWatch Logs 로그 그룹을 지정합니다.

1. https://console.aws.amazon.com/cloudtrail/에서 AWS CloudTrail 콘솔을 엽니다.

2. AWS CloudTrail 콘솔을 처음 사용하는 경우 메시지를 읽고 **시작하기**를 선택합니다.

3. **트레일 생성**을 선택합니다.

4. **이름**에 추적 이름을 입력합니다. 이름은 추적을 생성하는 리전에서 고유해야 합니다. 예를 들어 트레일 이름을 MyTrail로 지정할 수 있습니다.

5. **모든 지역에 추적 적용**에서 다음 중 하나를 수행합니다.

* 추적을 모든 지역에 적용하려면 **예, 모든 지역에 추적을 적용합니다**를 선택합니다.
* 선택한 지역에만 트레일을 적용하려면 **아니요, 선택한 지역에만 트레일을 적용합니다**를 선택한 다음 지역을 선택합니다.

6. **S3 버킷 이름**에 CloudTrail이 로그 파일을 전달할 Amazon S3 버킷의 이름을 입력합니다. 버킷은 추적을 생성하는 동일한 리전에 있어야 합니다. 기존 버킷의 이름을 입력하면 CloudTrail이 버킷에 로그 파일을 기록합니다. 버킷이 없으면 CloudTrail이 버킷을 생성합니다.

7. **S3 키 접두사**에 로그 파일 이름의 선택적 접두사를 입력합니다. 접두사를 지정하지 않으면 로그 파일이 접두사 없이 전달됩니다.

8. **CloudWatch Logs 로그 그룹 이름**에 CloudTrail이 로그 파일을 전달할 Amazon CloudWatch Logs 로그 그룹의 이름을 입력합니다. 로그 그룹은 추적을 생성하는 동일한 리전에 있어야 합니다.

9. **로그 파일 유효성 검사 활성화**에서 다음 중 하나를 수행합니다.

* 모든 로그 파일에 대해 디지털 서명을 생성하려면 **예**를 선택합니다. CloudTrail은 모든 로그 파일에 대한 디지털 서명을 생성합니다.
* 모든 로그 파일에 대한 디지털 서명을 거부하려면 **아니요**를 선택합니다.

10. **만들기**를 선택합니다.

추적을 생성한 후 추적에 이벤트를 게시하도록 Amazon S3를 설정해야 합니다.

### Amazon S3 설정

추적을 생성할 때 CloudTrail이 로그 파일을 제공할 Amazon S3 버킷을 지정합니다. CloudTrail은 Amazon S3를 사용하여 AWS 계정의 각 리전에서 로그 파일을 보냅니다. 트레일에 이벤트를 게시하려면 Amazon S3를 설정해야 합니다.

1. https://console.aws.amazon.com/s3/에서 Amazon S3 콘솔을 엽니다.

2. Amazon S3 콘솔에서 추적을 생성할 때 지정한 버킷의 이름을 선택합니다.

3. **속성**을 선택합니다.

4. 속성 창에서 **이벤트**를 선택합니다.

5. **알림 추가**를 선택합니다.

6. **이름** 필드에 이벤트 이름을 입력합니다.

7. **이벤트**에서 **모든 객체 생성 이벤트**를 선택합니다.

8. **보내기**에서 **SNS 주제**를 선택합니다.

9. **SNS 주제 ARN**에 추적을 생성할 때 지정한 Amazon SNS 주제의 ARN을 입력합니다.

10. **저장**을 선택합니다.

추적에 이벤트를 게시하도록 Amazon S3를 설정하면 CloudTrail은 지정한 버킷의 리소스에 대한 AWS API 호출 로깅을 시작합니다. CloudTrail이 로그 파일을 버킷에 전달하는 데 최대 15분이 걸릴 수 있습니다.

## 로그 파일 보기

추적을 생성하고 이벤트를 게시하도록 Amazon S3를 설정한 후에는 AWS CloudTrail 콘솔에서 거의 실시간으로 로그 파일을 보고 검색할 수 있습니다.

1. https://console.aws.amazon.com/cloudtrail/에서 AWS CloudTrail 콘솔을 엽니다.

2. **트레일**을 선택합니다.

3. 트레일의 이름을 선택합니다.

4. **추적 구성** 페이지에서 **로그 파일 보기**를 선택합니다.

5. **로그 파일** 목록에서 로그 파일의 이름을 선택합니다.

6. **다운로드**를 선택합니다.

7. **로그 파일 다운로드** 대화 상자에서 **파일 저장**을 선택합니다.

## CloudTrail 로그 파일 형식

CloudTrail 로그 파일에는 하나 이상의 로그 항목이 포함되어 있습니다. 로그 항목은 모든 소스의 단일 요청을 나타내며 요청된 작업, 작업 날짜 및 시간, 요청 매개변수 등에 대한 정보를 포함합니다.

CloudTrail은 공백으로 구분된 형식을 사용하여 로그 파일에 로그 항목을 기록합니다. 각 로그 항목은 공백으로 구분되는 9개의 필드로 구성됩니다. 필드를 사용하면 이벤트를 시작한 사용자 또는 역할, 이벤트 발생 시기, 영향을 받은 리소스 등을 포함하여 발생한 이벤트의 순서를 재구성하고 이해할 수 있습니다.

다음 표에서는 CloudTrail 로그 항목의 필드를 설명합니다.

| 필드 | 설명 |
| --- | --- |
| **이벤트ID** | 이벤트의 고유 식별자입니다. 예: **eventID=55746930-A87B-4E50-95A7-12B80B6E8700**. |
| **행사명** | 이벤트의 이름입니다. 예: **eventName=RunInstances**. |
| **이벤트 소스** | 이벤트를 생성한 AWS 서비스입니다. 예: **eventSource=ec2.amazonaws.com** 또는 **eventSource=iam.amazonaws.com**. |
| **aws지역** | 이벤트가 발생한 AWS 리전입니다. 예: **awsRegion=us-east-1**. |
| **소스IP주소** | 요청자의 IP 주소입니다. |
| **유저에이전트** | 요청에 포함된 사용자 에이전트 정보입니다(있는 경우). |
| **요청 매개변수** | 이벤트에 포함된 모든 요청 매개변수(있는 경우). 요청 파라미터는 일반적으로 AWS Management Console 또는 AWS API를 통해 수행되는 작업에 포함됩니다. 요청 매개변수의 형식은 **eventName**에 따라 다릅니다. |
| **responseElements** | AWS 서비스에서 반환한 응답 요소입니다(있는 경우). 응답 요소는 일반적으로 AWS Management Console을 통해 수행되는 작업에 포함됩니다. 응답 요소의 형식은 **eventName**에 따라 다릅니다. |
| **추가 이벤트 데이터** | 이벤트에 대한 추가 정보입니다. |
| **요청 ID** | 요청을 식별하는 값입니다. |
| **이벤트 유형** | 이벤트 유형입니다. 유효한 값은 **AwsApiCall**, **AwsServiceEvent** 및 **AwsSdkCall**입니다. |
| **recipientAccountId** | 다른 AWS 계정에서 이벤트를 수신하는 AWS 계정 ID입니다. 예를 들어 조직의 구성원 계정에서 이벤트가 마스터 계정으로 전달됩니다. 이 필드는 교차 계정 이벤트에 대해서만 채워집니다. |
| **sharedEventId** | 마스터 계정에 있는 이벤트의 **eventID**입니다. 이 필드는 교차 계정 이벤트에 대해서만 채워집니다. |

## CloudTrail 로그 파일 예

다음은 CloudTrail 로그 파일의 예입니다.

```
55746930-A87B-4E50-95A7-12B80B6E8700 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Mozilla/5.0 aws-cli/1.7.28 Python/2.7.9 Windows/2012server botocore/1.3.22
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 사용자