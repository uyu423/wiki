---
title: AWS 및 Azure에서 재해 복구 및 비즈니스 연속성 구현
description: 
published: true
date: 2023-02-01T14:58:18.332Z
tags: 
editor: markdown
dateCreated: 2023-02-01T14:58:16.792Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Implementing Disaster Recovery and Business Continuity on AWS and Azure***English** version of this document is available*](/en/Knowledge-base/Cloud/implementing-disaster-recovery-and-business-continuity-on-aws-and-azure)
{.links-list}


  ### AWS 및 Azure에서 재해 복구 및 비즈니스 연속성 구현

  재해 발생 시 재해 복구(DR) 및 비즈니스 연속성 계획(BCP)을 잘 구현하는 것은 비즈니스를 계속 운영하는 데 매우 중요합니다. DR 및 BCP를 구현하는 방법에는 여러 가지가 있지만 AWS(Amazon Web Services) 및 Microsoft Azure와 같은 공급자의 클라우드 서비스를 사용하는 것이 좋은 옵션이 될 수 있습니다.

  클라우드 기반 DR 및 BCP는 기존 온프레미스 솔루션에 비해 많은 이점을 제공할 수 있습니다. 예를 들어 클라우드 서비스는 필요에 따라 신속하게 프로비저닝 및 확장될 수 있으므로 대규모 재해가 발생한 경우에도 DR 및 BCP 솔루션이 비즈니스 요구 사항을 충족할 수 있습니다. 또한 클라우드 서비스는 인터넷 연결을 통해 어디에서나 액세스할 수 있으므로 재해로 인해 온프레미스 인프라가 손상되거나 파괴된 경우 큰 이점이 될 수 있습니다.

  그러나 AWS 및 Azure에서 DR 및 BCP를 구현하는 것은 어려울 수 있습니다. 이 기사에서는 이 두 클라우드 플랫폼에서 DR 및 BCP를 구현하기 위한 몇 가지 주요 고려 사항에 대한 개요를 제공합니다.

  #### AWS 및 Azure의 재해 복구에 대한 고려 사항

  AWS 또는 Azure에서 DR을 계획할 때 염두에 두어야 할 몇 가지 주요 고려 사항이 있습니다.

  - **가용 영역:** AWS와 Azure는 모두 각 지역에서 여러 가용 영역(AZ)을 제공합니다. AZ는 지연 시간이 짧은 네트워킹을 통해 연결된 물리적으로 분리된 데이터 센터입니다. 두 플랫폼 중 하나에서 DR을 계획할 때 애플리케이션과 데이터를 여러 데이터 센터에 복제할 수 있도록 여러 AZ가 있는 지역을 선택하는 것이 중요합니다.

  - **지역:** AWS와 Azure 모두 전 세계 여러 지역을 제공합니다. DR 솔루션에 대한 지역을 선택할 때 기본 지역에서 지리적으로 멀리 떨어진 지역을 선택하는 것이 중요합니다. 이렇게 하면 DR 솔루션이 기본 지역에 영향을 미치는 동일한 재해의 영향을 받지 않도록 할 수 있습니다. 또한 비즈니스 규정 준수 및 데이터 주권 요구 사항을 충족하는 지역을 선택하는 것이 중요합니다.

  - **VPC:** AWS와 Azure 모두 공용 인터넷에서 애플리케이션과 데이터를 격리하는 데 사용할 수 있는 가상 사설 클라우드(VPC)를 제공합니다. 각 플랫폼에서 DR을 계획할 때 DR 솔루션에 사용할 각 지역에 VPC를 생성하는 것이 중요합니다. 이렇게 하면 DR 솔루션이 공용 인터넷에 영향을 미치는 네트워크 중단 또는 보안 위반의 영향을 받지 않도록 할 수 있습니다.

  - **네트워킹:** AWS와 Azure 모두 VPN, Direct Connect 및 ExpressRoute를 비롯한 다양한 네트워킹 옵션을 제공합니다. 두 플랫폼 중 하나에서 DR을 계획할 때 성능 및 가용성 요구 사항을 충족하는 네트워킹 옵션을 선택하는 것이 중요합니다.

  - **스토리지:** AWS와 Azure 모두 객체 스토리지, 블록 스토리지, 파일 스토리지를 비롯한 다양한 스토리지 옵션을 제공합니다. 두 플랫폼 중 하나에서 DR을 계획할 때 성능 및 가용성 요구 사항을 충족하는 스토리지 옵션을 선택하는 것이 중요합니다.

  - **데이터베이스:** AWS와 Azure 모두 관계형 데이터베이스, NoSQL 데이터베이스, 메모리 내 데이터베이스를 비롯한 다양한 데이터베이스 옵션을 제공합니다. 두 플랫폼 중 하나에서 DR을 계획할 때 성능 및 가용성 요구 사항을 충족하는 데이터베이스 옵션을 선택하는 것이 중요합니다.

  - **보안:** AWS와 Azure 모두 방화벽, 침입 탐지 및 방지, 데이터 암호화를 비롯한 다양한 보안 옵션을 제공합니다. 두 플랫폼 중 하나에서 DR을 계획할 때 규정 준수 및 데이터 주권 요구 사항을 충족하는 보안 옵션을 선택하는 것이 중요합니다.

  - **비용:** AWS와 Azure 모두 종량제, 예약 인스턴스, 약정 사용 할인 등 다양한 가격 옵션을 제공합니다. 두 플랫폼 중 하나에서 DR을 계획할 때 예산 및 비즈니스 요구 사항을 충족하는 가격 옵션을 선택하는 것이 중요합니다.

  #### AWS의 재해 복구

  Amazon Web Services(AWS)는 재해 복구(DR) 및 비즈니스 연속성(BCP) 솔루션을 구현하는 데 사용할 수 있는 다양한 서비스를 제공합니다. 이 섹션에서는 DR 및 BCP에 사용할 수 있는 몇 가지 주요 AWS 서비스에 대한 개요를 제공합니다.

  - **AWS CloudFormation:** AWS CloudFormation은 템플릿을 사용하여 AWS 리소스를 생성하고 관리할 수 있는 서비스입니다. CloudFormation 템플릿을 사용하여 DR 솔루션을 위한 AWS 리소스를 프로비저닝하고 구성할 수 있습니다.

  - **AWS Elastic Beanstalk:** AWS Elastic Beanstalk는 AWS에서 웹 애플리케이션을 배포하고 관리할 수 있는 서비스입니다. Elastic Beanstalk는 DR 솔루션용 웹 애플리케이션을 배포하고 관리하는 데 사용할 수 있습니다.

  - **AWS Lambda:** AWS Lambda는 서버를 프로비저닝하거나 관리하지 않고도 코드를 실행할 수 있는 서비스입니다. Lambda를 사용하여 DR 솔루션용 코드를 실행할 수 있습니다.

  - **AWS OpsWorks:** AWS OpsWorks는 AWS 리소스의 배포 및 관리를 자동화할 수 있는 서비스입니다. OpsWorks는 DR 솔루션을 위한 AWS 리소스의 배포 및 관리를 자동화하는 데 사용할 수 있습니다.

  - **AWS Storage Gateway:** AWS Storage Gateway는 온프레미스 스토리지 시스템을 AWS에 연결할 수 있게 해주는 서비스입니다. Storage Gateway는 DR 솔루션을 위해 온프레미스 스토리지 시스템을 AWS에 연결하는 데 사용할 수 있습니다.

  - **AWS CloudTrail:** AWS CloudTrail은 AWS API 호출을 모니터링할 수 있는 서비스입니다. CloudTrail을 사용하여 DR 솔루션에 대한 AWS API 호출을 모니터링할 수 있습니다.

  - **AWS Config:** AWS Config는 AWS 리소스의 변경 사항을 추적할 수 있는 서비스입니다. 구성을 사용하여 DR 솔루션에 대한 AWS 리소스의 변경 사항을 추적할 수 있습니다.

  - **AWS CloudWatch:** AWS CloudWatch는 AWS 리소스를 모니터링할 수 있는 서비스입니다. CloudWatch를 사용하여 DR 솔루션에 대한 AWS 리소스를 모니터링할 수 있습니다.

  - **AWS Trusted Advisor:** AWS Trusted Advisor는 AWS 리소스를 최적화하는 방법에 대한 권장 사항을 제공하는 서비스입니다. Trusted Advisor를 사용하여 DR 솔루션을 최적화하는 방법에 대한 권장 사항을 제공할 수 있습니다.

  - **AWS Service Catalog:** AWS Service Catalog는 AWS 리소스를 관리할 수 있는 서비스입니다. Service Catalog를 사용하여 DR 솔루션에 대한 AWS 리소스를 관리할 수 있습니다.

  - **AWS Identity and Access Management:** AWS Identity and Access Management(IAM)는 사용자 및 권한을 관리할 수 있는 서비스입니다. IAM을 사용하여 DR 솔루션에 대한 사용자 및 권한을 관리할 수 있습니다.

  - **AWS Key Management Service:** AWS Key Management Service(KMS)는 암호화 키를 관리할 수 있는 서비스입니다. KMS를 사용하여 DR 솔루션의 암호화 키를 관리할 수 있습니다.

  - **AWS CloudHSM:** AWS CloudHSM은 하드웨어 보안 모듈을 관리할 수 있는 서비스입니다. CloudHSM을 사용하여 DR 솔루션의 하드웨어 보안 모듈을 관리할 수 있습니다.

  - **AWS Directory Service:** AWS Directory Service는 Active Directory를 관리할 수 있는 서비스입니다. 디렉터리 서비스를 사용하여 DR 솔루션의 Active Directory를 관리할 수 있습니다.

  - **AWS Certificate Manager:** AWS Certificate Manager는 SSL/TLS 인증서를 관리할 수 있는 서비스입니다. Certificate Manager를 사용하여 DR 솔루션에 대한 SSL/TLS 인증서를 관리할 수 있습니다.

  - **AWS WAF:** AWS WAF는 웹 애플리케이션 방화벽을 관리할 수 있는 서비스입니다. WAF는 DR 솔루션의 웹 애플리케이션 방화벽을 관리하는 데 사용할 수 있습니다.

  - **AWS Shield:** AWS Shield는 DDoS 공격으로부터 애플리케이션을 보호할 수 있는 서비스입니다. Shield는 DR 솔루션에 대한 DDoS 공격으로부터 애플리케이션을 보호하는 데 사용할 수 있습니다.

  - **AWS Inspector:** AWS Inspector는 AWS 리소스의 보안을 평가할 수 있는 서비스입니다. Inspector를 사용하여 DR 솔루션에 대한 AWS 리소스의 보안을 평가할 수 있습니다.

  - **AWS Artifact:** AWS Artifact는 규정 준수 문서를 관리할 수 있는 서비스입니다. Artifact를 사용하여 DR 솔루션에 대한 규정 준수 문서를 관리할 수 있습니다.

  #### Azure의 재해 복구

  Microsoft Azure는 DR(재해 복구) 및 BCP(비즈니스 연속성) 솔루션을 구현하는 데 사용할 수 있는 다양한 서비스를 제공합니다. 이 섹션에서는 DR 및 BCP에 사용할 수 있는 몇 가지 주요 Azure 서비스에 대한 개요를 제공합니다.

  - **Azure Site Recovery:** Azure Site Recovery는 Azure VM을 복제하고 복구할 수 있는 서비스입니다. Site Recovery를 사용하여 DR 솔루션용 Azure VM을 복제하고 복구할 수 있습니다.

  - **Azure Backup:** Azure Backup은 Azure VM을 백업 및 복원할 수 있는 서비스입니다. 백업은 DR 솔루션용 Azure VM을 백업 및 복원하는 데 사용할 수 있습니다.

  - **Azure Storage:** Azure Storage는 클라우드에 데이터를 저장하고 액세스할 수 있는 서비스입니다. 스토리지는 DR 솔루션의 데이터를 저장하는 데 사용할 수 있습니다.

  - **Azure SQL Database:** Azure SQL Database는 클라우드에서 관계형 데이터베이스를 실행할 수 있게 해주는 서비스입니다. SQL Database는 DR 솔루션을 위한 관계형 데이터베이스를 실행하는 데 사용할 수 있습니다.

  - **Azure Cosmos DB:** Azure Cosmos DB는 클라우드에서 NoSQL 데이터베이스를 실행할 수 있게 해주는 서비스입니다. Cosmos DB는 DR 솔루션용 NoSQL 데이터베이스를 실행하는 데 사용할 수 있습니다.

  - **Azure Table Storage:** Azure Table Storage는 데이터를 클라우드에 저장할 수 있는 서비스입니다. Table Storage는 DR 솔루션의 데이터를 저장하는 데 사용할 수 있습니다.

  - **Azure Blob Storage:** Azure Blob Storage는 데이터를 클라우드에 저장할 수 있는 서비스입니다. Blob Storage는 DR 솔루션의 데이터를 저장하는 데 사용할 수 있습니다.

  - **Azure File Storage:** Azure File Storage는 데이터를 클라우드에 저장할 수 있는 서비스입니다. File Storage는 DR 솔루션의 데이터를 저장하는 데 사용할 수 있습니다.

  - **Azure Virtual Network:** Azure Virtual Network는 가상 네트워크를 만들고 관리할 수 있는 서비스입니다. 가상 네트워크는 DR 솔루션에 대한 가상 네트워크를 만들고 관리하는 데 사용할 수 있습니다.

  - **Azure Load Balancer:** Azure Load Balancer는 여러 VM에 트래픽을 분산할 수 있는 서비스입니다. Load Balancer는 DR 솔루션을 위해 여러 VM에 트래픽을 분산하는 데 사용할 수 있습니다.

  - **Azure Traffic Manager:** Azure Traffic Manager는 트래픽을 다른 Azure 리소스로 라우팅할 수 있는 서비스입니다. Traffic Manager를 사용하여 DR 솔루션의 다른 Azure 리소스로 트래픽을 라우팅할 수 있습니다.

  - **Azure DNS:** Azure DNS는 DNS 레코드를 관리할 수 있는 서비스입니다. DNS는 DR 솔루션의 DNS 레코드를 관리하는 데 사용할 수 있습니다.

  - **Azure Active Directory:** Azure Active Directory는 사용자 및 권한을 관리할 수 있는 서비스입니다. Active Directory를 사용하여 DR 솔루션에 대한 사용자 및 권한을 관리할 수 있습니다.

  - **Azure Key Vault:** Azure Key Vault는 암호화 키를 관리할 수 있는 서비스입니다. Key Vault를 사용하여 DR 솔루션의 암호화 키를 관리할 수 있습니다.

  - **Azure Information Protection:** Azure Information Protection은 데이터를 보호할 수 있는 서비스입니다. 정보 보호는 DR 솔루션의 데이터를 보호하는 데 사용할 수 있습니다.

  - **Azure Security Center:** Azure Security Center는 Azure 리소스에 대한 보안을 모니터링하고 관리할 수 있는 서비스입니다. Security Center를 사용하여 DR 솔루션용 Azure 리소스의 보안을 모니터링하고 관리할 수 있습니다.

  - **Azure Monitor:** Azure Monitor는 Azure 리소스를 모니터링할 수 있는 서비스입니다. 모니터를 사용하여 DR 솔루션에 대한 Azure 리소스를 모니터링할 수 있습니다.

  - **Azure Policy:** Azure Policy는 규정 준수 정책을 관리하고 적용할 수 있는 서비스입니다. 정책을 사용하여 DR 솔루션에 대한 규정 준수 정책을 관리하고 시행할 수 있습니다.

  - **Azure Blueprints:** Azure Blueprints는 Azure 리소스를 생성하고 관리할 수 있는 서비스입니다. 청사진을 사용하여 DR 솔루션에 대한 Azure 리소스를 만들고 관리할 수 있습니다.

  - **Azure Resource Manager:** Azure Resource Manager는 Azure 리소스를 관리할 수 있는 서비스입니다. Resource Manager를 사용하여 DR 솔루션에 대한 Azure 리소스를 관리할 수 있습니다.

  ### 결론

  재해 복구(DR) 및 비즈니스 연속성(BCP) 구현은 어려울 수 있습니다. 그러나 AWS(Amazon Web Services) 및 Microsoft Azure와 같은 공급자의 클라우드 서비스를 사용하는 것이 좋은 선택이 될 수 있습니다. 이 문서에서는 AWS 및 Azure에서 DR 및 BCP를 구현하기 위한 몇 가지 주요 고려 사항에 대한 개요를 제공했습니다.