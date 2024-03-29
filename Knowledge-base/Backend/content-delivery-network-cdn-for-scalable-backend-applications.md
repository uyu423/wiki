---
title: 확장 가능한 백엔드 애플리케이션을 위한 콘텐츠 전송 네트워크(CDN)
description: 
published: true
date: 2023-02-18T19:06:29.428Z
tags: 
editor: markdown
dateCreated: 2023-02-18T19:06:28.077Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Content Delivery Network (CDN) for Scalable Backend Applications***English** document is available*](/en/Knowledge-base/Backend/content-delivery-network-cdn-for-scalable-backend-applications)
{.links-list}


# 확장 가능한 백엔드 애플리케이션을 위한 콘텐츠 전송 네트워크(CDN)

## CDN이란?

**콘텐츠 전송 네트워크(CDN)**는 인터넷 콘텐츠의 빠른 전송을 제공하기 위해 함께 작동하는 지리적으로 분산된 서버 모음입니다. CDN은 전 세계에 전략적으로 위치한 데이터 센터에 콘텐츠 사본을 저장하거나 캐시합니다. 사용자가 CDN에서 사용할 수 있는 콘텐츠를 요청하면 CDN은 사용자의 위치와 가장 가까운 서버에서 콘텐츠를 전달합니다. 이렇게 하면 대기 시간이 줄어들고 콘텐츠 전송 속도가 향상됩니다.

## CDN은 어떻게 작동하나요?

CDN은 두 가지 유형의 서버로 구성됩니다.

- 원본 서버: 원본 콘텐츠가 저장되는 서버입니다. 콘텐츠는 HTML 페이지 및 이미지와 같이 정적이거나 비디오 및 라이브 스트림과 같이 동적일 수 있습니다.
- 에지 서버: 이 서버는 전 세계의 전략적 지점에 위치하며 원본 서버의 콘텐츠를 캐시하거나 저장합니다. 사용자가 CDN에서 사용할 수 있는 콘텐츠를 요청하면 CDN은 사용자 위치와 가장 가까운 에지 서버에서 콘텐츠를 전달합니다.

## CDN을 사용하면 어떤 이점이 있나요?

CDN은 다음과 같은 많은 이점을 제공합니다.

- **향상된 콘텐츠 전송 속도:** CDN은 전 세계 전략적으로 위치한 데이터 센터에 콘텐츠 사본을 캐싱하거나 저장하여 콘텐츠 전송 속도를 향상시킬 수 있습니다. 사용자가 CDN에서 사용할 수 있는 콘텐츠를 요청하면 CDN은 사용자의 위치와 가장 가까운 서버에서 콘텐츠를 전달할 수 있으므로 지연 시간이 줄어들고 콘텐츠 전송 속도가 향상됩니다.

- **용량 및 안정성 증가:** CDN은 많은 수의 서버에 전송 로드를 분산하여 급증하는 수요에 맞춰 콘텐츠 전송을 확장하는 데 도움이 될 수 있습니다. 이렇게 하면 트래픽이 많은 기간 동안 콘텐츠를 사용할 수 없거나 로드 속도가 느려지는 것을 방지할 수 있습니다.

- **향상된 보안:** CDN은 원래 서버로 향하는 트래픽을 흡수하고 편향시켜 분산 서비스 거부(DDoS) 공격으로부터 콘텐츠를 보호할 수 있습니다.

## CDN의 일반적인 사용 사례는 무엇입니까?

CDN은 일반적으로 다음과 같은 콘텐츠를 제공하는 데 사용됩니다.

- **정적:** 정적 콘텐츠에는 HTML 페이지, 이미지, CSS 파일 및 JavaScript 파일이 포함됩니다.

- **동적:** 동적 콘텐츠에는 비디오, 라이브 스트림 및 오디오 파일이 포함됩니다.

- **애플리케이션 데이터:** 애플리케이션 데이터에는 API 호출, 데이터베이스 쿼리 및 애플리케이션에서 생성된 기타 데이터가 포함됩니다.

## CDN은 어떻게 선택하나요?

CDN을 선택할 때 고려해야 할 몇 가지 사항은 다음과 같습니다.

- **어떤 유형의 콘텐츠를 제공할 예정입니까?** HTML 페이지 및 이미지와 같은 정적 콘텐츠를 제공할 계획이라면 정적 콘텐츠 제공을 전문으로 하는 CDN을 선택할 수 있습니다. 비디오 및 라이브 스트림과 같은 동적 콘텐츠를 제공할 계획이라면 동적 콘텐츠 제공을 전문으로 하는 CDN을 선택할 수 있습니다.

- **예산은 얼마인가요?** CDN은 가격이 천차만별이므로 예산에 맞는 CDN을 선택하는 것이 중요합니다.

- **성능 목표는 무엇입니까?** CDN은 성능 측면에서 다양하므로 성능 목표를 달성하는 데 도움이 될 수 있는 CDN을 선택하는 것이 중요합니다.

- **귀하의 보안 요구 사항은 무엇입니까?** CDN은 보안 측면에서 다양하므로 보안 요구 사항을 충족하는 데 도움이 되는 CDN을 선택하는 것이 중요합니다.

## 결론

콘텐츠 전송 네트워크(CDN)는 빠른 콘텐츠 전송을 제공하기 위해 함께 작동하는 지리적으로 분산된 서버 모음입니다. CDN은 전 세계에 전략적으로 위치한 데이터 센터에 콘텐츠 사본을 저장하거나 캐시합니다. 사용자가 CDN에서 사용할 수 있는 콘텐츠를 요청하면 CDN은 사용자의 위치와 가장 가까운 서버에서 콘텐츠를 전달하므로 대기 시간이 줄어들고 콘텐츠 전송 속도가 향상됩니다.