---
title: AWS Certificate Manager: 보안 웹 애플리케이션용 SSL 인증서 관리
description: 
published: true
date: 2023-02-19T03:06:29.832Z
tags: 
editor: markdown
dateCreated: 2023-02-19T03:06:28.452Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS Certificate Manager: Managing SSL Certificates for Secure Web Applications***English** document is available*](/en/Knowledge-base/Cloud/aws-certificate-manager-managing-ssl-certificates-for-secure-web-applications)
{.links-list}


# AWS Certificate Manager: 보안 웹 애플리케이션을 위한 SSL 인증서 관리

AWS Certificate Manager(ACM)는 AWS에서 호스팅되는 웹 애플리케이션용 SSL/TLS 인증서를 관리하는 사용자 친화적이고 비용 효율적인 방법입니다. ACM은 다음과 같은 다양한 이점을 제공합니다.

- **보안**: ACM은 AWS Identity and Access Management(IAM)와 통합된 가용성과 확장성이 뛰어난 사설 CA 서비스인 AWS Certificate Manager 사설 인증 기관(CA)을 사용합니다. ACM 사설 CA는 조직 내부의 인증서를 발급하는 데 사용할 수 있는 사설 CA를 제공합니다.

- **사용 편의성**: ACM을 사용하면 웹 애플리케이션용 SSL/TLS 인증서를 쉽게 프로비저닝, 관리 및 배포할 수 있습니다. ACM을 사용하면 몇 번의 클릭만으로 인증서를 요청하고 AWS 리소스에 배포하고 갱신할 수 있습니다.

- **저렴한 비용**: ACM은 AWS 리소스에서 사용할 수 있는 무료 SSL/TLS 인증서를 제공하며 인증서 배포에 사용한 AWS 리소스에 대해서만 비용을 지불하면 됩니다.

## SSL/TLS 인증서란?

SSL/TLS 인증서는 SSL/TLS 프로토콜을 사용하여 웹 서버와 웹 브라우저 간의 통신을 암호화하는 디지털 인증서입니다. SSL/TLS 인증서는 일반적으로 웹 트래픽을 보호하고 웹 서버를 인증하는 데 사용됩니다.

## ACM은 어떻게 작동합니까?

ACM은 여러 AWS 서비스에서 웹 애플리케이션에 대한 SSL/TLS 인증서를 관리하기 위한 통합 환경을 제공합니다. ACM은 Elastic Load Balancing, Amazon CloudFront 및 Amazon API Gateway와 같은 AWS 서비스와 통합되어 인증서 프로비저닝, 배포 및 갱신을 위한 원활한 환경을 제공합니다.

또한 ACM을 사용하면 AWS 리소스와 함께 사용할 타사 SSL/TLS 인증서를 쉽게 가져올 수 있습니다. AWS Certificate Manager 콘솔을 사용하여 몇 번의 클릭만으로 인증서를 요청하고 AWS 리소스에 배포하고 갱신할 수 있습니다.

## ACM 사용의 이점

ACM은 다음을 포함하여 웹 애플리케이션에 대한 SSL/TLS 인증서 관리에 대한 여러 가지 이점을 제공합니다.

- **보안**: ACM은 AWS Identity and Access Management(IAM)와 통합된 가용성과 확장성이 뛰어난 사설 CA 서비스인 AWS Certificate Manager 사설 인증 기관(CA)을 사용합니다. ACM 사설 CA는 조직 내부의 인증서를 발급하는 데 사용할 수 있는 사설 CA를 제공합니다.

- **사용 편의성**: ACM을 사용하면 웹 애플리케이션용 SSL/TLS 인증서를 쉽게 프로비저닝, 관리 및 배포할 수 있습니다. ACM을 사용하면 몇 번의 클릭만으로 인증서를 요청하고 AWS 리소스에 배포하고 갱신할 수 있습니다.

- **저렴한 비용**: ACM은 AWS 리소스에서 사용할 수 있는 무료 SSL/TLS 인증서를 제공하며 인증서 배포에 사용한 AWS 리소스에 대해서만 비용을 지불하면 됩니다.

## ACM을 시작하는 방법

ACM을 시작하려면 AWS 계정을 만든 다음 ACM 콘솔에 로그인하기만 하면 됩니다. 여기에서 인증서를 요청하고 AWS 리소스에 배포하고 몇 번의 클릭만으로 갱신할 수 있습니다.

AWS 리소스와 함께 사용하려는 기존 SSL/TLS 인증서가 있는 경우 ACM으로 가져올 수 있습니다. ACM을 사용하여 테스트 목적으로 자체 서명된 인증서를 생성할 수도 있습니다.

## 결론

ACM은 웹 애플리케이션에 대한 SSL/TLS 인증서를 관리하는 사용자 친화적이고 비용 효율적인 방법입니다. ACM은 보안, 사용 용이성, 저렴한 비용 등 다양한 이점을 제공합니다. ACM을 시작하려면 AWS 계정을 만든 다음 ACM 콘솔에 로그인하기만 하면 됩니다.