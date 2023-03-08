---
title: AWS CloudFront: CDN으로 콘텐츠 전송 개선
description: 
published: true
date: 2023-02-01T14:17:42.941Z
tags: 
editor: markdown
dateCreated: 2023-02-01T14:17:41.534Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [AWS CloudFront: Improving Content Delivery with a CDN***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-cloudfront-improving-content-delivery-with-a-cdn)
{.links-list}


  기사의 시작 및 종료 문장을 포함합니다.

# AWS CloudFront: CDN으로 콘텐츠 전송 개선

웹사이트 또는 웹 애플리케이션의 성능을 개선하려는 경우 가장 먼저 살펴봐야 할 곳 중 하나는 콘텐츠 전송 네트워크(CDN)입니다. CDN은 사용자가 더 빠르게 액세스할 수 있도록 전 세계 위치에 콘텐츠를 캐싱하여 콘텐츠 로드 속도를 개선하는 데 도움이 될 수 있습니다.

가장 인기 있는 CDN 중 하나는 Amazon의 AWS 인프라 위에 있는 서비스인 Amazon CloudFront입니다. CloudFront는 엣지 로케이션 네트워크를 통해 콘텐츠를 제공하는 글로벌 CDN입니다. 설정 및 구성이 쉽고 다른 AWS 서비스와 통합됩니다.

이 기사에서는 CloudFront로 콘텐츠 전송을 개선하는 방법을 살펴보겠습니다. 다음 주제를 다룹니다.

- CloudFront 설정
- CloudFront 구성
- 다른 AWS 서비스와 함께 CloudFront 사용

## CloudFront 설정

CloudFront를 시작하려면 배포를 생성해야 합니다. 배포는 콘텐츠를 제공하는 데 사용되는 AWS 리소스 모음입니다. 배포를 만들려면 다음을 지정해야 합니다.

- 콘텐츠의 출처. 이는 Amazon S3 버킷, Amazon Elastic Compute Cloud(EC2) 인스턴스 또는 HTTP 서버일 수 있습니다.
- 배포판의 구성. 여기에는 배포의 캐시 동작 및 기타 설정이 포함됩니다.
- 유통의 가격 등급. 사용자가 콘텐츠에 액세스하는 지역에 따라 배포 가격이 결정됩니다.

배포를 만든 후에는 배포될 때까지 기다려야 합니다. 최대 15분이 소요될 수 있습니다. 배포가 배포되면 CloudFront URL을 통해 콘텐츠에 액세스할 수 있습니다.

## CloudFront 구성

CloudFront 배포를 설정했으면 웹 사이트 또는 웹 애플리케이션에서 작동하도록 구성해야 합니다. 가장 먼저 해야 할 일은 캐시 동작을 만드는 것입니다. 캐시 동작은 CloudFront에서 콘텐츠에 대한 요청을 처리하는 방법을 결정합니다.

캐시 동작에는 기본 및 사용자 지정의 두 가지 유형이 있습니다. 특정 파일 또는 폴더에 대한 사용자 지정 캐시 동작을 지정하지 않는 한 기본 캐시 동작은 배포의 모든 파일에 적용됩니다. 사용자 지정 캐시 동작은 특정 파일 또는 폴더에 적용되며 기본 캐시 동작보다 우선합니다.

캐시 동작을 생성하려면 다음을 지정해야 합니다.

- 캐시 동작이 적용되는 경로 패턴입니다. 이것은 특정 파일이나 폴더 또는 와일드카드 패턴일 수 있습니다.
- 캐시 동작이 적용되는 원본입니다. 이것은 CloudFront가 콘텐츠를 가져올 오리진입니다.
- 캐시 동작에 대한 기본 TTL(Time to Live)입니다. CloudFront에서 콘텐츠를 캐싱하는 시간입니다.
- 캐시 동작에 대한 최대 TTL입니다. CloudFront가 콘텐츠를 캐싱하는 최대 시간입니다.
- 캐시 동작에 대한 최소 TTL입니다. 이것은 CloudFront가 콘텐츠를 캐싱하는 최소 시간입니다.

캐시 동작을 만든 후에는 다음과 같은 추가 설정을 지정할 수 있습니다.

- 허용되는 HTTP 메서드. 이는 CloudFront에서 캐시 동작을 허용할 HTTP 메서드를 결정합니다.
- 캐시된 HTTP 메서드. 이는 CloudFront가 캐시 동작에 대해 캐시할 HTTP 메서드를 결정합니다.
- 전달된 헤더. 이는 CloudFront가 캐시 동작을 위해 오리진에 전달할 헤더를 결정합니다.

## 다른 AWS 서비스와 함께 CloudFront 사용

CloudFront는 다른 AWS 서비스와 함께 사용하여 웹 사이트 또는 웹 애플리케이션의 성능을 향상시킬 수 있습니다. 예를 들어 Amazon S3와 함께 CloudFront를 사용하여 S3 버킷에서 콘텐츠를 전달할 수 있습니다.

이렇게 하려면 버킷을 생성한 다음 버킷을 오리진으로 사용하도록 CloudFront를 구성해야 합니다. 버킷에 대한 캐시 동작을 생성하여 이를 수행할 수 있습니다.

이 작업을 완료하면 CloudFront를 사용하여 버킷의 콘텐츠를 사용자에게 전달할 수 있습니다. CloudFront는 사용자가 더 빠르게 액세스할 수 있도록 전 세계 엣지 위치에서 콘텐츠를 캐싱합니다.

Amazon EC2와 함께 CloudFront를 사용하여 EC2 인스턴스에서 콘텐츠를 전달할 수도 있습니다. 이렇게 하려면 인스턴스를 생성한 다음 인스턴스를 오리진으로 사용하도록 CloudFront를 구성해야 합니다. 인스턴스에 대한 캐시 동작을 생성하여 이를 수행할 수 있습니다.

이 작업을 완료하면 CloudFront를 사용하여 인스턴스의 콘텐츠를 사용자에게 전달할 수 있습니다. CloudFront는 사용자가 더 빠르게 액세스할 수 있도록 전 세계 엣지 위치에서 콘텐츠를 캐싱합니다.

## 결론

이 기사에서는 CloudFront로 콘텐츠 전송을 개선하는 방법을 살펴보았습니다. 우리는 다음 주제를 다루었습니다.

- CloudFront 설정
- CloudFront 구성
- 다른 AWS 서비스와 함께 CloudFront 사용

웹 사이트 또는 웹 애플리케이션의 성능을 개선하려는 경우 CloudFront는 훌륭한 옵션입니다. 설정 및 구성이 쉽고 다른 AWS 서비스와 통합됩니다.