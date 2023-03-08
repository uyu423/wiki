---
title: ElastiCache 및 ElasticBeanstalk로 애플리케이션 확장
description: 
published: true
date: 2023-02-17T18:14:16.744Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:23:16.326Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Scaling Applications with ElastiCache and ElasticBeanstalk***English** version of this document is available*](/en/Knowledge-base/Backend/scaling-applications-with-elasticache-and-elasticbeanstalk)
{.links-list}
 

## ElastiCache 및 ElasticBeanstalk로 애플리케이션 확장

이 기사에서는 애플리케이션 확장에 도움이 되는 두 가지 Amazon Web Services(AWS) 제품인 ElastiCache와 Elastic Beanstalk에 대해 살펴보겠습니다. 이러한 제품의 작동 방식과 애플리케이션을 확장하는 데 사용할 수 있는 방법에 대해 설명합니다.

ElastiCache는 클라우드에서 인 메모리 캐시를 쉽게 배포, 운영 및 확장할 수 있게 해주는 웹 서비스입니다. ElastiCache는 두 가지 오픈 소스 캐싱 엔진인 Memcached와 Redis를 지원합니다.

Elastic Beanstalk는 AWS 클라우드에서 웹 애플리케이션을 쉽게 배포하고 관리할 수 있게 해주는 웹 서비스입니다. Elastic Beanstalk는 웹 애플리케이션 배포 및 실행을 위한 플랫폼을 제공합니다. 용량 프로비저닝, 로드 밸런싱, 확장 및 애플리케이션 상태 모니터링의 세부 정보를 자동으로 처리합니다.

Elastic Beanstalk와 함께 ElastiCache를 사용하는 경우 ElastiCache의 수직 및 수평 확장 기능을 활용할 수 있습니다. 수직 확장이란 애플리케이션에서 사용할 수 있는 메모리 양 및/또는 CPU 수를 늘리는 것을 의미합니다. 수평 확장은 캐시 클러스터에 더 많은 노드를 추가하는 것을 의미합니다.

ElastiCache는 캐시 클러스터에 노드를 추가하여 수직으로 확장할 수 있습니다. 수평으로 확장하려면 ElastiCache 클러스터에 노드를 더 추가하면 됩니다. 샤딩을 사용하여 수평으로 확장할 수도 있습니다. 샤딩은 데이터를 여러 노드에 분산시키는 기술입니다.

Elastic Beanstalk는 환경에 더 많은 웹 서버를 추가하여 수평으로 확장할 수 있습니다. 웹 서버에서 사용할 수 있는 메모리 양 및/또는 CPU 수를 늘려 세로로 확장할 수도 있습니다.

다음은 ElastiCache 및 Elastic Beanstalk를 사용하여 애플리케이션을 확장하기 위한 몇 가지 팁입니다.

- ElastiCache를 사용하여 자주 액세스하는 데이터를 캐시합니다. 캐싱은 데이터베이스로의 이동 횟수를 줄여 애플리케이션의 성능을 향상시킬 수 있습니다.

- Elastic Beanstalk를 사용하여 웹 애플리케이션을 배포하고 관리합니다. Elastic Beanstalk는 웹 애플리케이션 배포 및 실행을 위한 플랫폼을 제공합니다. 용량 프로비저닝, 로드 밸런싱, 확장 및 애플리케이션 상태 모니터링의 세부 정보를 자동으로 처리합니다.

- ElastiCache를 Elastic Beanstalk와 함께 사용하여 ElastiCache의 수직 및 수평 확장 기능을 활용합니다. 수직 확장이란 애플리케이션에서 사용할 수 있는 메모리 양 및/또는 CPU 수를 늘리는 것을 의미합니다. 수평 확장은 캐시 클러스터에 더 많은 노드를 추가하는 것을 의미합니다.

- 샤딩을 사용하여 ElastiCache를 수평으로 확장합니다. 샤딩은 데이터를 여러 노드에 분산시키는 기술입니다.

- Elastic Beanstalk를 사용하여 환경에 더 많은 웹 서버를 추가하여 수평으로 확장합니다. 웹 서버에서 사용할 수 있는 메모리 양 및/또는 CPU 수를 늘려 세로로 확장할 수도 있습니다.