---
title: AWS 및 Azure에서 규정 준수 및 거버넌스 관리
description: 
published: true
date: 2023-03-05T09:11:51.787Z
tags: 
editor: markdown
dateCreated: 2023-03-05T08:32:37.261Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Managing Compliance and Governance on AWS and Azure***English** document is available*](/en/Knowledge-base/Cloud/managing-compliance-and-governance-on-aws-and-azure)
{.links-list}

AWS 및 Azure에서 규정 준수 및 거버넌스 관리

기업이 계속해서 인프라를 클라우드 기반 플랫폼으로 이동함에 따라 규정 준수 및 거버넌스가 해결해야 하는 중요한 구성 요소가 되었습니다. AWS와 Azure는 규정 준수 및 거버넌스 관리를 위한 포괄적인 도구를 제공하는 널리 사용되는 두 가지 클라우드 플랫폼입니다. 이 기사에서는 AWS 및 Azure에서 규정 준수 및 거버넌스를 관리하는 방법을 살펴봅니다.

## 규정 준수 및 거버넌스

규정 준수는 조직의 운영이 법적, 규정 또는 계약 요구 사항을 준수하는지 확인하는 것을 의미합니다. 거버넌스는 목표를 달성하고 비즈니스 전략과 일치하도록 보장하기 위한 조직 운영의 전반적인 관리를 의미합니다.

규정 준수 및 거버넌스는 조직의 IT 인프라를 관리하는 데 중요한 요소입니다. 제대로 관리하지 않으면 벌금, 법적 조치 또는 명예 실추와 같은 심각한 결과를 초래할 수 있습니다.

## AWS의 규정 준수

AWS는 인프라가 필수 표준을 충족하는지 확인하기 위해 포괄적인 규정 준수 프로그램 및 인증 세트를 제공합니다. AWS에서 제공하는 일부 인증에는 SOC 1/2/3, PCI DSS, HIPAA 및 FedRAMP가 포함됩니다.

### AWS 구성

AWS Config는 AWS 리소스 구성을 평가, 감사 및 평가할 수 있는 서비스입니다. AWS 리소스 및 해당 구성에 대한 자세한 인벤토리를 제공하고 리소스가 조직의 정책 및 지침을 준수하는지 확인하는 데 도움이 됩니다.

AWS Config를 시작하려면 AWS Management Console에서 활성화해야 합니다. 활성화되면 리소스에 대한 구성 변경 사항을 자동으로 기록하고 S3 버킷에 저장합니다.

### AWS 클라우드트레일

AWS CloudTrail은 AWS 계정에 대한 모든 API 호출을 모니터링하고 기록할 수 있는 서비스입니다. API 호출을 한 사람, 호출 시간 및 호출이 이루어진 IP 주소를 포함하여 AWS 계정의 모든 활동에 대한 감사 추적을 제공합니다.

CloudTrail 로그는 규제 요구 사항 준수를 모니터링하고 보안 사고를 감지하며 운영 문제를 해결하는 데 사용할 수 있습니다. 로그를 사용하여 사용자 정의 보고서를 생성하거나 분석을 위해 타사 도구와 통합할 수 있습니다.

### AWS 자격 증명 및 액세스 관리(IAM)

AWS IAM을 사용하면 AWS 리소스에 대한 사용자 액세스를 관리할 수 있습니다. 이를 통해 사용자 계정을 생성 및 관리하고, 권한을 할당하고, AWS 리소스에 대한 액세스를 제어할 수 있습니다. IAM은 승인된 사용자만 리소스에 액세스할 수 있고 적절한 수준의 액세스 권한이 있는지 확인하는 데 도움이 됩니다.

IAM 정책을 사용하여 사용자, 그룹 및 역할에 대한 세분화된 권한을 설정할 수 있습니다. IAM 정책을 사용하여 사용자가 액세스할 수 있는 리소스와 해당 리소스에서 수행할 수 있는 작업을 정의할 수 있습니다.

## Azure의 규정 준수

Azure는 인프라가 필수 표준을 충족하는지 확인하기 위해 포괄적인 규정 준수 프로그램 및 인증 세트를 제공합니다. Azure에서 제공하는 일부 인증에는 SOC 1/2/3, PCI DSS, HIPAA 및 FedRAMP가 포함됩니다.

### Azure 정책

Azure Policy는 Azure 리소스에 대한 정책을 생성, 할당 및 관리할 수 있는 서비스입니다. 정책은 Azure 인프라 내에서 조직 표준 및 규정 준수 요구 사항을 적용하는 데 도움이 됩니다.

Azure Policy는 정책을 만들고 관리하기 위한 중앙 집중식 위치를 제공하고 정책이 모든 Azure 리소스에 적용되도록 합니다. 정책을 사용하여 리소스가 올바르게 구성되고 액세스가 적절하게 제한되며 보안 요구 사항이 충족되는지 확인할 수 있습니다.

### Azure 보안 센터

Azure Security Center는 Azure 인프라 전체에서 보안 태세의 통합 보기를 제공하는 서비스입니다. 보안 권장 사항, 위협 감지 및 사고 대응 기능을 제공합니다.

Security Center를 사용하여 규정 요구 사항 준수를 모니터링하고, 보안 사고를 감지하고, 보안 태세에 대한 인사이트를 제공할 수 있습니다. 보안 태세에 대한 포괄적인 보기를 제공하고 보안 태세를 개선하기 위한 조치를 취할 수 있습니다.

### 애저 액티브 디렉터리(AD)

Azure AD를 사용하면 Azure 리소스에 대한 사용자 액세스를 관리할 수 있습니다. 이를 통해 사용자 계정을 생성 및 관리하고, 권한을 할당하고, Azure 리소스에 대한 액세스를 제어할 수 있습니다. Azure AD는 인증된 사용자만 리소스에 액세스할 수 있고 적절한 수준의 액세스 권한이 있는지 확인하는 데 도움이 됩니다.

Azure AD 정책을 사용하여 사용자, 그룹 및 역할에 대한 세분화된 권한을 설정할 수 있습니다. Azure AD 정책을 사용하여 사용자가 액세스할 수 있는 리소스와 해당 리소스에서 수행할 수 있는 작업을 정의할 수 있습니다.

## 결론

AWS 및 Azure에서 규정 준수 및 거버넌스를 관리하는 것은 인프라가 필수 표준을 충족하는지 확인하는 데 중요합니다. AWS와 Azure는 AWS Config, AWS CloudTrail, AWS IAM, Azure Policy, Azure Security Center 및 Azure AD를 포함하여 규정 준수 및 거버넌스를 관리하기 위한 포괄적인 도구를 제공합니다.

이러한 도구를 사용하여 인프라가 법률, 규정 및 계약 요구 사항을 준수하고 운영이 비즈니스 전략에 부합하는지 확인할 수 있습니다.

## 외부 리소스

- [AWS 규정 준수](https://aws.amazon.com/compliance/)
- [AWS 구성](https://aws.amazon.com/config/)
- [AWS CloudTrail](https://aws.amazon.com/cloudtrail/)
- [AWS Identity and Access Management(IAM)](https://aws.amazon.com/iam/)
- [Azure 규정 준수](https://azure.microsoft.com/en-us/overview/trusted-cloud/compliance/)
- [Azure 정책](https://azure.microsoft.com/en-us/services/azure-policy/)
- [Azure 보안 센터](https://azure.microsoft.com/en-us/services/security-center/)
- [Azure Active Directory(AD)](https://azure.microsoft.com/en-us/services/active-directory/)