---
title: 안정적인 AWS Serverless 서비스하기
description: 언제가의 AWS 관련 세미나 요약
published: true
date: 2023-02-17T17:58:36.521Z
tags: aws, serverless, seminar
editor: markdown
dateCreated: 2022-11-24T04:40:14.227Z
---

- 경주 지진시 국민안전처 사이트 7시간 동안 다운되었음
- 갑자기 몰린 서비스. 스케일 업 불가능.
  - 사이트 102 request, 820KB.
- 과거에 비해 가벼워진 사이트
  - 1천만명이 동시에 접속한다면?
    - 당연히 죽음.
    - Bandwidth가 오바됨.
    - 데이터 캐싱이 없으니 I/O하닥 죽어버림
    - Unknown Error. 개발자 계속 바뀌고 해서 유지보수가 안됨.
- 전문가들의 주장
  - 클라우드로 이동했으면 이 문제를 해결했을것이다.
    - 그럴리가 없다.. 클라우드는 만병 통치약이 아니다.

## Serverless Architecture
- FaaS (Function as a Service)
- 남는 CPU 자원, 리소스 자원을 어떻게 할것인가
  - 처음에 VM이 생겼따.
  - 그리고 나서 Servless가 생겼다.
  - AWS Lambda
- 코드만 개발자가 관리. 나머지는 Docker 컨테이너가 관리.
- 유저 스트레스에 따라 자동 스케일 up down.
- Where is RISK?
  - Docker가 부팅될 때까지 Slow 응답, 응답 없음 (흠????)
  - SLA (서비스 품질 협약)
    - AWS Lambda is NO SLA : 람다는 SLA에 대한 보장이 없다. -> 가끔 그냥 안될 수가 있음.
    - Azure Function : 가용성이 99.95 라고 한다.
    - SLA는 클라우드 공급자가 서비스를 얼마나 안정시켰는지 보여주는 척도
    - 3사 SLA 수준
      - 마소 : 99.9% (거의 모든 서비스, 장애나면 다 물어줌)
      - 아마존 : 없음. (EC2, RDS, S3, Route 53, CloudFront만 적용, 가끔 람다에서 400에러가 나는데 왜나는지 모름.)
      - 구글 : 99.9% (거의 모든 서비스, 장애나면 다 물어줌)
      - SLA가 없으면 미션 크리티컬한 서비스를 올렸을 때 x될 수도 있다는 소리임.
- 서버리스는 재난 상황에서 Standby 스케일업 가능하기는 함.

## 국민안전처. 뭐부터 바꿔야할까.
1. CDN 올려야된다. 당연한거다. 하지만 안하겠지. (99.99%~100%)
  - 서버리스 아키텍쳐 중 유일하게 안정화된 기술
  - AKAMAI, KT CDN은 100%
  - 클라우드 프론트는 99.9%
  - 에러를 보아하니 국민안전처는 CDN 조차 없었을 것으로 추정.
2. 서버리스 아키텍처 제안
  - 사진 참고
  - Azure App Service : 뭔지 까먹음. 좋다고 함.

## 하이브리드 클라우드
- 안타깝긴 하지만 기존 레거시와의 호환을 위해

## 장애 리스크도 있는데 우리는 왜 서버리스를 해야하나?
- 클라우드의 발전 방향 때문에 그렇다.
  - 언젠가 부터 System Enginner가 하는일이 자연스럽게 Dev에게 넘어왔다.
  - 다른말로 DevOps라고 한다......
  - 추천 책 : 그림자 노동의 역습 (DevOps)

## 2015년 자동차 사고 3만건 넘은
- 94%는 인간의 실수.
- 개발도 똑같음. 모든 패치는 대부분 인간의 실수.
- 인간이 뭔가를 하게되면 사이드 이펙트가 생긴다.
- 개발자는 코드만. 클라우드는 그 외 모든 것을! 그런 의미에서 구글 앱엔진이 좋은거다. 나머지는 사기 치는거임.
- 지구 온난화 CO2 절감을 위해 우리는 서버리스를 써야한다.버

## 서버리스 적용기
- 게임 이벤트 서버
  - 대부분의 모바일 게임은 on-demand로 통신할 필요가 없음.
  - 응답 없어도 모바일에서 캐시된 데이터를 불러오게함
  - 잃어버려도 타격이 적은 부분만 적용.
  - 그랬더니 비용절감 55% 달성
  - 패치 및 운영 비용 절감.

## 다가오는 클라우드 기술은?
- 사실상 인간의 실수를 줄여주는 방향으로 발전할 것임.
- 시간과 노력과 비용을 아끼자.

## 마무리
- 도커는 사랑이라고 한다..

## 질문
- 람다는 SLA가 없는데, 람다랑 비교햇을 때 대단한 차이가 있나염
  - SLA가 없다는 말이 뭐냐면, 해당 이벤트 콜을 할당할 수 없는 상황이 있음. 람다의 경우 이벤트 가용성이 굉장히 협소함. 제가 볼때는 1000만 콜 중에서 2건 3건정도 불량이 나온다고 보고있음. 당분간 서울리전 쓰지마세요. 서울리전은 특히 안정화가 안되어 있는 것 같음. 오래된 리전의 경우 안정화 되어있고, 스태프도 잘 되어있음. 도쿄의 경우도 안정화에 2년이 걸림. 결국 사람이 하기 때문에 스탭 안정화에도 시기가 필요하다.
- 아마존 람다에서 SQL을 연결해야할 상황이 있을 경우, SQL에 DB Connection을 올려야된다. 그런데 람다에 직접 DB Connection을 올리면 문제가 생길텐데 어떻게 해야될까염.
  - 솔직히 얘기하면 그렇게 하시면 안되염. Too many Connection으로 죽어버림. 걔네들이 말하는 오로라 디비나 스케일 업 디비를 써야되는데, 그럴 바에는 레디스나 몽고디비를 쓰는게 낫다. 중간에 캐시를 만들어서 쓰시면 좋다. 라프텐 같은 경우도 캐시를 응용하면 람다에도 충분히 사용할 수 있다. 쿼리가 있다고 해도 분석해보면 정적으로 떨어지는 부분이 있다. 그런 부분을 캐싱하는 방법을 고려해보식리. 특히 마리아 디비를 쓰면 스레드 풀을 지원한다. 메모리 캐시를 지원한다는 얘기다. 꼭 참고해보시길
