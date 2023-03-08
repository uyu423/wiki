---
title: AWS 및 Azure의 클라우드에서 데이터 보호
description: 
published: true
date: 2023-02-06T12:55:46.783Z
tags: 
editor: markdown
dateCreated: 2023-02-06T12:55:45.166Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Securing Data in the Cloud on AWS and Azure***English** document is available*](/en/Knowledge-base/Cloud/securing-data-in-the-cloud-on-aws-and-azure)
{.links-list}


# Cloud on AWS 및 Azure의 데이터 보안

클라우드는 확장성, 유연성, 비용 절감 등 클라우드의 많은 이점을 활용하려는 기업의 기본 옵션이 되었습니다. 그러나 이러한 이점에는 중요한 데이터를 보호하기 위해 관리해야 하는 보안 위험이 따릅니다. 이 기사에서는 AWS 및 Azure의 클라우드에서 데이터를 보호하는 방법을 살펴보겠습니다.

## AWS

AWS는 IAM(Identity and Access Management), KMS(Key Management Service) 및 CloudTrail을 포함하여 클라우드에서 데이터를 보호하는 데 도움이 되는 다양한 서비스를 제공합니다.

### ID 및 액세스 관리

IAM은 AWS 리소스에 대한 액세스를 안전하게 제어하는 데 도움이 되는 웹 서비스입니다. IAM을 사용하면 사용자와 그룹을 생성 및 관리하고 권한을 사용하여 AWS 리소스에 대한 액세스를 허용 및 거부할 수 있습니다. IAM은 추가 비용 없이 제공되는 AWS 계정의 기능입니다.

IAM은 AWS 클라우드 보안의 중요한 구성 요소입니다. 어떤 사용자가 어떤 AWS 리소스에 액세스할 수 있고 해당 리소스에서 수행할 수 있는 작업을 세밀하게 제어할 수 있습니다. 또한 IAM을 사용하면 사용자와 그룹을 생성 및 관리하고 권한을 사용하여 AWS 리소스에 대한 액세스를 허용 및 거부할 수 있습니다.

### 키 관리 서비스

KMS는 데이터를 암호화하는 데 사용되는 암호화 키를 쉽게 만들고 제어할 수 있게 해주는 관리형 서비스입니다. KMS는 데이터를 암호화하는 데 사용되는 키를 관리하는 안전하고 편리한 방법입니다. KMS는 키 생성, 순환 및 삭제와 키 사용 모니터링 및 감사를 위한 중앙 집중식 제어 지점을 제공합니다.

KMS는 AWS 클라우드 보안의 중요한 구성 요소입니다. 키 생성, 회전 및 삭제와 키 사용 모니터링 및 감사를 위한 중앙 집중식 제어 지점을 제공합니다. KMS는 데이터 암호화에 사용되는 키를 관리하는 편리하고 안전한 방법입니다.

### 클라우드트레일

CloudTrail은 계정에 대한 AWS API 호출을 기록하고 로그 파일을 전달하는 웹 서비스입니다. CloudTrail은 AWS Management Console, AWS SDK, 명령줄 도구 및 기타 AWS 서비스를 통해 이루어진 API 호출을 포함하여 계정에 대한 AWS API 호출 기록을 제공합니다. CloudTrail을 사용하면 AWS 계정에서 사용자 활동을 모니터링, 제어 및 감사할 수 있습니다.

CloudTrail은 AWS 클라우드 보안의 중요한 구성 요소입니다. AWS Management Console, AWS SDK, 명령줄 도구 및 기타 AWS 서비스를 통해 수행된 API 호출을 포함하여 계정에 대한 AWS API 호출 기록을 제공합니다. CloudTrail을 사용하면 AWS 계정에서 사용자 활동을 모니터링, 제어 및 감사할 수 있습니다.

## 아주르

Azure는 Azure AD(Active Directory), Azure Storage 및 Azure Key Vault를 포함하여 클라우드에서 데이터를 보호하는 데 도움이 되는 다양한 서비스를 제공합니다.

### 애저 액티브 디렉토리

Azure AD는 클라우드 기반 ID 및 액세스 관리 서비스입니다. Azure AD는 사용자 ID 및 Azure 리소스에 대한 액세스를 관리하기 위한 중앙 위치를 제공합니다. 또한 Azure AD를 사용하면 온-프레미스 Active Directory를 클라우드로 확장하여 하이브리드 클라우드를 위한 단일 ID 인프라를 제공할 수 있습니다.

Azure AD는 Azure 클라우드의 중요한 보안 구성 요소입니다. 사용자 ID 및 Azure 리소스에 대한 액세스를 관리하기 위한 중앙 위치를 제공합니다. 또한 Azure AD를 사용하면 온-프레미스 Active Directory를 클라우드로 확장하여 하이브리드 클라우드를 위한 단일 ID 인프라를 제공할 수 있습니다.

### Azure 저장소

Azure 저장소는 클라우드 기반 저장소 서비스입니다. Azure Storage는 클라우드의 데이터를 위한 확장 가능하고 안정적이며 안전한 스토리지 솔루션을 제공합니다. Azure Storage는 클라우드에 데이터를 저장하는 편리하고 안전한 방법입니다.

Azure Storage는 Azure 클라우드 보안의 중요한 구성 요소입니다. 클라우드의 데이터를 위한 확장 가능하고 안정적이며 안전한 스토리지 솔루션을 제공합니다. Azure Storage는 클라우드에 데이터를 저장하는 편리하고 안전한 방법입니다.

### Azure 키 자격 증명 모음

Azure Key Vault는 클라우드 기반 키 관리 서비스입니다. Azure Key Vault는 애플리케이션에서 사용하는 키와 비밀을 보호하는 데 도움이 됩니다. Azure Key Vault는 애플리케이션에서 사용하는 키와 비밀을 관리하는 편리하고 안전한 방법입니다.

Azure Key Vault는 Azure 클라우드 보안의 중요한 구성 요소입니다. 애플리케이션에서 사용하는 키와 비밀을 보호하는 데 도움이 됩니다. Azure Key Vault는 애플리케이션에서 사용하는 키와 비밀을 관리하는 편리하고 안전한 방법입니다.

## 결론

이 기사에서는 AWS 및 Azure의 클라우드에서 데이터를 보호하는 방법을 살펴보았습니다. 우리는 AWS와 Azure가 클라우드에서 데이터를 보호하는 데 도움이 되는 다양한 서비스를 제공하는 방법을 살펴보았습니다. 이러한 서비스는 클라우드 보안의 중요한 구성 요소입니다.

## 참조

- AWS 자격 증명 및 액세스 관리: https://aws.amazon.com/iam/
- AWS 키 관리 서비스: https://aws.amazon.com/kms/
- AWS CloudTrail: https://aws.amazon.com/cloudtrail/
- 애저 액티브 디렉터리: https://azure.microsoft.com/en-us/services/active-directory/
- Azure 저장소: https://azure.microsoft.com/en-us/services/storage/
- Azure 키 자격 증명 모음: https://azure.microsoft.com/en-us/services/key-vault/