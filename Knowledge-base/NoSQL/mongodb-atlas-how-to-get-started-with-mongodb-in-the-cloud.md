---
title: MongoDB Atlas: 클라우드에서 MongoDB를 시작하는 방법
description: 
published: true
date: 2023-03-08T21:32:30.151Z
tags: 
editor: markdown
dateCreated: 2023-03-08T21:32:30.151Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MongoDB Atlas: How to Get Started with MongoDB in the Cloud***English** document is available*](/en/Knowledge-base/NoSQL/mongodb-atlas-how-to-get-started-with-mongodb-in-the-cloud)
{.links-list}

## 소개

MongoDB는 유연한 스키마 디자인과 확장성을 갖춘 오늘날 가장 인기 있는 NoSQL 데이터베이스 중 하나입니다. 그러나 MongoDB 배포를 설정하고 관리하는 것은 많은 사람들에게 어려운 작업일 수 있습니다. 다행스럽게도 MongoDB Atlas는 개발자의 데이터베이스 관리 부담을 덜어줄 수 있는 사용하기 쉬운 완전 관리형 클라우드 호스팅 데이터베이스 플랫폼을 제공합니다. 이 기사에서는 MongoDB Atlas를 시작하는 방법을 살펴보겠습니다.

## 계정 만들기

MongoDB Atlas를 시작하려면 먼저 계정을 만들어야 합니다. https://www.mongodb.com/cloud/atlas에서 무료 계정에 가입할 수 있습니다. 계정을 만들고 나면 MongoDB Atlas 대시보드에 로그인할 수 있습니다.

## 클러스터 생성

MongoDB Atlas 대시보드에 로그인한 후 첫 번째 단계는 클러스터를 생성하는 것입니다. 클러스터는 데이터를 저장하고 애플리케이션을 실행하는 시스템 그룹입니다. 새 클러스터를 생성하려면 대시보드에서 "Build a New Cluster" 버튼을 클릭하십시오.

### 공급자 및 지역 선택

새 클러스터를 만드는 첫 번째 단계는 클라우드 공급자와 지역을 선택하는 것입니다. MongoDB Atlas는 AWS(Amazon Web Services), GCP(Google Cloud Platform) 및 Microsoft Azure를 비롯한 여러 클라우드 공급자를 지원합니다. 요구 사항과 예산에 맞는 공급자를 선택할 수 있습니다.

### 클러스터 유형 선택

클라우드 공급자와 지역을 선택한 후 클러스터 유형을 선택해야 합니다. MongoDB Atlas는 M0, M2/M5 및 M10+의 세 가지 유형의 클러스터를 제공합니다. M0 클러스터는 무료 클러스터인 반면 M2/M5 및 M10+는 유료 클러스터입니다. M2/M5 및 M10+ 클러스터는 클러스터를 확장 및 축소하는 기능을 포함하여 M0 클러스터보다 더 많은 기능을 제공합니다.

### 추가 설정하기

클러스터를 생성하기 전에 노드 수, 노드 크기 및 백업 옵션과 같은 추가 설정을 구성할 수 있습니다. 사용하려는 MongoDB 버전을 선택할 수도 있습니다.

## 클러스터에 연결

클러스터를 생성한 후 MongoDB 셸, MongoDB Compass 또는 MongoDB 유선 프로토콜을 지원하는 기타 MongoDB 드라이버와 같은 MongoDB 클라이언트를 사용하여 클러스터에 연결할 수 있습니다.

### MongoDB 셸 사용

MongoDB 셸을 사용하여 클러스터에 연결하려면 MongoDB Atlas 대시보드에서 연결 문자열을 가져와야 합니다. 연결 문자열에는 클러스터에 연결하는 데 필요한 사용자 이름, 비밀번호 및 기타 매개변수가 포함됩니다. 연결 문자열을 얻으려면 대시보드에서 "연결" 버튼을 클릭하고 "MongoDB 셸과 연결"을 선택합니다.

```bash
mongo "mongodb+srv://cluster0.mongodb.net/test" --username myusername
```

### MongoDB 나침반 사용

MongoDB Compass는 데이터를 탐색하고 시각화할 수 있는 GUI 도구입니다. MongoDB Compass를 사용하여 클러스터에 연결하려면 MongoDB Atlas 대시보드에서 연결 문자열을 가져와야 합니다. 연결 문자열을 얻으려면 대시보드에서 "연결" 버튼을 클릭하고 "MongoDB Compass로 연결"을 선택합니다.

클러스터에 연결한 후 MongoDB Compass UI를 사용하여 데이터를 탐색할 수 있습니다.

## 결론

MongoDB Atlas는 개발자의 데이터베이스 관리 부담을 덜어줄 수 있는 사용하기 쉬운 완전 관리형 클라우드 호스팅 데이터베이스 플랫폼을 제공합니다. 이 기사에서는 계정 생성, 클러스터 생성 및 MongoDB 클라이언트를 사용하여 클러스터에 연결하는 것을 포함하여 MongoDB Atlas를 시작하는 기본 사항을 다뤘습니다.

## 외부 리소스

- [MongoDB 아틀라스 문서](https://docs.atlas.mongodb.com/)
- [MongoDB 나침반 문서](https://docs.mongodb.com/compass/current/)
- [MongoDB 셸 문서](https://docs.mongodb.com/manual/mongo/)