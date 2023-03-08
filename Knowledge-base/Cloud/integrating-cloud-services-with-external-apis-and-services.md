---
title: 외부 API 및 서비스와 클라우드 서비스 통합
description: 
published: true
date: 2023-02-07T14:17:24.264Z
tags: 
editor: markdown
dateCreated: 2023-02-07T14:17:22.638Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Integrating Cloud Services with External APIs and Services***English** document is available*](/en/Knowledge-base/Cloud/integrating-cloud-services-with-external-apis-and-services)
{.links-list}


# 소개

개발자는 클라우드 서비스를 외부 API 및 서비스와 통합해야 하는 경우가 많습니다. 잠재적인 실패 지점이 많기 때문에 이는 어려운 작업이 될 수 있습니다. 이 기사에서는 가장 일반적인 문제 중 일부를 살펴보고 이를 극복하기 위한 실용적인 솔루션을 제공합니다.

## 인증

클라우드 서비스를 통합할 때 가장 일반적인 문제 중 하나는 인증입니다. 많은 클라우드 서비스는 외부 서비스와 통합하기 어려울 수 있는 독점 인증 메커니즘을 사용합니다.

한 가지 해결책은 [Auth0](https://auth0.com/)과 같은 통합 인증 계층을 제공하는 서비스를 사용하는 것입니다. Auth0은 단일 자격 증명 세트를 사용하여 여러 클라우드 서비스를 인증하는 데 사용할 수 있습니다.

또 다른 해결책은 인증을 위한 개방형 표준인 [OpenID Connect](https://openid.net/connect/)를 이용하는 것입니다. 많은 클라우드 서비스가 OpenID Connect를 지원하므로 여러 서비스와 통합해야 하는 개발자에게 적합합니다.

## 승인

클라우드 서비스를 통합할 때 또 다른 일반적인 문제는 권한 부여입니다. 많은 클라우드 서비스는 외부 서비스와 통합하기 어려울 수 있는 독점 권한 부여 메커니즘을 사용합니다.

한 가지 해결책은 [OAuth.io](https://oauth.io/)와 같은 통합 인증 계층을 제공하는 서비스를 사용하는 것입니다. OAuth.io는 단일 자격 증명 세트를 사용하여 여러 클라우드 서비스에 대한 액세스 권한을 부여하는 데 사용할 수 있습니다.

또 다른 해결책은 인증을 위한 개방형 표준인 [OpenID Connect](https://openid.net/connect/)를 이용하는 것입니다. 많은 클라우드 서비스가 OpenID Connect를 지원하므로 여러 서비스와 통합해야 하는 개발자에게 적합합니다.

## 속도 제한

많은 클라우드 서비스는 API에 대해 수행할 수 있는 요청 수에 속도 제한을 적용합니다. 만들 수 있는 요청 수가 제한되는 경우가 많기 때문에 외부 서비스와 통합할 때 문제가 될 수 있습니다.

한 가지 해결책은 [속도 제한](https://www.rate-limiting.com/)과 같은 통합 속도 제한 계층을 제공하는 서비스를 사용하는 것입니다. 속도 제한을 사용하여 여러 클라우드 서비스에 대한 요청 수를 제한할 수 있습니다.

또 다른 해결책은 인증을 위한 개방형 표준인 [OpenID Connect](https://openid.net/connect/)를 이용하는 것입니다. 많은 클라우드 서비스가 OpenID Connect를 지원하므로 여러 서비스와 통합해야 하는 개발자에게 적합합니다.

## 결론

클라우드 서비스를 외부 API 및 서비스와 통합하는 것은 어려운 작업일 수 있습니다. 이 기사에서는 가장 일반적인 문제 중 일부를 살펴보고 이를 극복하기 위한 실용적인 솔루션을 제공했습니다.