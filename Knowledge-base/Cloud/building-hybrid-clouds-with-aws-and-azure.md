---
title: AWS 및 Azure로 하이브리드 클라우드 구축
description: 
published: true
date: 2023-02-17T18:12:13.136Z
tags: 
editor: markdown
dateCreated: 2023-01-30T19:04:19.547Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Building Hybrid Clouds with AWS and Azure***English** version of this document is available*](/en/Knowledge-base/Cloud/building-hybrid-clouds-with-aws-and-azure)
{.links-list}




# AWS와 Azure로 하이브리드 클라우드 구축

Azure Stack 및 AWS Outposts의 최신 릴리스를 통해 이제 Azure와 AWS를 모두 포괄하는 하이브리드 클라우드를 구축할 수 있습니다. 이 기사에서는 이를 수행하는 방법과 이를 수행할 때의 이점 및 단점에 대해 살펴보겠습니다.

## 하이브리드 클라우드란?

하이브리드 클라우드는 온프레미스와 클라우드 기반 리소스를 혼합하여 사용하는 클라우드 컴퓨팅 유형입니다. 퍼블릭 클라우드와 프라이빗 클라우드가 혼합되어 있거나 다양한 클라우드 공급자가 혼합되어 있을 수 있습니다.

하이브리드 클라우드의 일반적인 사용 사례 중 하나는 컴퓨팅 및 스토리지 리소스에 클라우드를 사용하는 동시에 보안 또는 규제상의 이유로 데이터를 온프레미스에 유지하는 것입니다.

또 다른 일반적인 사용 사례는 프로덕션을 온프레미스로 유지하면서 개발 및 테스트에 클라우드를 사용하는 것입니다. 이는 비용상의 이유로 또는 생산 데이터를 보다 안전한 네트워크에 유지하기 위해 수행할 수 있습니다.

## Azure Stack 및 AWS Outposts

Azure Stack은 하이브리드 클라우드를 구축하는 데 사용할 수 있는 Azure의 온-프레미스 버전입니다. 여기에는 Azure와 동일한 컴퓨팅, 스토리지 및 네트워킹 리소스가 모두 포함되며 동일한 Azure Portal을 사용하여 관리할 수 있습니다.

AWS Outposts는 하이브리드 클라우드를 구축하는 데 사용할 수 있는 AWS의 온프레미스 버전입니다. 여기에는 AWS와 동일한 컴퓨팅, 스토리지 및 네트워킹 리소스가 모두 포함되며 동일한 AWS 콘솔을 사용하여 관리할 수 있습니다.

## 하이브리드 클라우드 구축

Azure 및 AWS를 사용하여 하이브리드 클라우드를 구축하는 두 가지 주요 방법이 있습니다.

### 옵션 1: 컴퓨팅용 Azure Stack 및 스토리지용 AWS Outposts 사용

이 옵션에서는 모든 컴퓨팅 리소스에 Azure Stack을 사용하고 모든 스토리지 리소스에 AWS Outposts를 사용합니다. 데이터는 Outposts의 S3 버킷에 저장되고 Azure Stack에서 실행되는 애플리케이션에서 데이터에 액세스합니다.

이 옵션의 한 가지 이점은 하나의 리소스 집합만 관리하면 된다는 것입니다. 모든 컴퓨팅은 Azure Portal에서 관리되고 모든 스토리지는 AWS 콘솔에서 관리됩니다.

이 옵션의 단점은 Azure의 Blob 저장소 또는 AWS의 EBS 볼륨을 활용할 수 없다는 것입니다. 또한 Azure Stack 배포와 동일한 위치에 Outposts를 설치해야 합니다.

### 옵션 2: 스토리지용 Azure Stack 및 컴퓨팅용 AWS Outposts 사용

이 옵션에서는 모든 스토리지 리소스에 Azure Stack을 사용하고 모든 컴퓨팅 리소스에 AWS Outposts를 사용합니다. 데이터는 Azure Stack의 Blob 스토리지에 저장되고 AWS Outposts에서 실행되는 애플리케이션에서 데이터에 액세스합니다.

이 옵션의 한 가지 이점은 Azure의 Blob 저장소를 활용할 수 있다는 것입니다. 자주 액세스하지 않는 데이터 또는 안전한 위치에 저장해야 하는 데이터에 사용할 수 있습니다.

이 옵션의 단점은 AWS의 EBS 볼륨을 활용할 수 없다는 것입니다. 또한 Azure Stack 배포와 동일한 위치에 Outposts를 설치해야 합니다.

## 결론

Azure와 AWS를 사용하여 하이브리드 클라우드를 구축하는 것은 두 세계의 장점을 최대한 활용할 수 있는 좋은 방법입니다. Azure Stack 및 AWS Outposts를 사용하면 하이브리드 클라우드를 쉽게 배포하고 관리할 수 있습니다.