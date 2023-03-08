---
title: 소프트웨어 개발 075: 부하 테스트
description: 
published: true
date: 2023-02-04T20:17:29.574Z
tags: 
editor: markdown
dateCreated: 2023-02-04T20:17:24.209Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Software Development 075: Load Testing***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-075-load-testing)
{.links-list}


## 소개

부하 테스트는 시스템 또는 응용 프로그램에 대한 요구 사항을 입력하고 응답을 측정하는 프로세스입니다. 목표는 시스템이나 애플리케이션이 다양한 로드 조건에서 작동하는 방식을 결정하는 것입니다.

부하 테스트는 시스템 또는 애플리케이션에서 잠재적인 성능 병목 현상을 식별하는 데 도움이 될 수 있기 때문에 중요합니다. 또한 시스템 또는 애플리케이션이 처리할 수 있는 최대 사용자 수를 결정하는 데 도움이 될 수 있습니다.

부하 테스트에 사용할 수 있는 다양한 도구가 있습니다. 이 게시물에서는 널리 사용되는 오픈 소스 도구인 Apache JMeter에 중점을 둘 것입니다.

## 아파치 J미터 설치하기

Apache JMeter는 다음 링크에서 다운로드할 수 있습니다.

http://jmeter.apache.org/

파일을 다운로드한 후 압축을 풀면 다음과 같은 디렉터리 구조가 표시됩니다.

```
apache-jmeter-3.1
├── bin
├── docs
├── lib
└── printable_docs
```

## 테스트 계획 만들기

테스트 계획은 JMeter가 테스트를 실행하는 데 사용할 일련의 지침입니다. 테스트 계획에는 다음 요소가 포함되어야 합니다.

- 스레드 그룹: JMeter가 테스트를 실행하는 데 사용할 스레드 그룹입니다.
- 샘플러: 이것은 JMeter가 시스템 또는 애플리케이션에 요청을 보내는 데 사용할 요소입니다.
- 리스너: JMeter가 테스트 결과를 수집하고 표시하는 데 사용할 요소입니다.

테스트 계획을 만들려면 JMeter를 실행하면 다음 화면이 표시됩니다.

![JMeter 시작 화면](https://i.imgur.com/VkzMv9w.png)

스레드 그룹을 추가하려면 테스트 계획을 마우스 오른쪽 단추로 클릭하고 추가 > 스레드(사용자) > 스레드 그룹을 선택하십시오.

![JMeter 스레드 그룹](https://i.imgur.com/DYUi4T4.png)

샘플러를 추가하려면 스레드 그룹을 마우스 오른쪽 버튼으로 클릭하고 추가 > 샘플러 > HTTP 요청을 선택합니다.

![JMeter 샘플러](https://i.imgur.com/iLKVLCy.png)

수신기를 추가하려면 스레드 그룹을 마우스 오른쪽 버튼으로 클릭하고 추가 > 수신기 > 결과 트리 보기를 선택합니다.

![JMeter 수신기](https://i.imgur.com/qoWql3Y.png)

## 테스트 계획 구성

스레드 그룹, 샘플러 및 리스너를 테스트 계획에 추가했으면 이를 구성해야 합니다.

스레드 그룹을 구성하려면 해당 그룹을 선택하면 다음 옵션이 표시됩니다.

![JMeter 스레드 그룹 옵션](https://i.imgur.com/g4vO4jQ.png)

- 스레드 수(사용자): JMeter가 테스트를 실행하는 데 사용할 스레드 수입니다.
- 루프 수: JMeter가 테스트를 실행할 횟수입니다.
- 램프업 기간(초): JMeter가 스레드 수를 늘리는 데 걸리는 시간입니다.

샘플러를 구성하려면 샘플러를 선택하면 다음 옵션이 표시됩니다.

![JMeter 샘플러 옵션](https://i.imgur.com/A1mlvkx.png)

- 프로토콜: JMeter가 요청을 보내는 데 사용할 프로토콜입니다.
- 서버 이름 또는 IP: JMeter가 요청을 보낼 서버 이름 또는 IP 주소입니다.
- 포트 번호: JMeter가 요청을 보내는 데 사용할 포트 번호입니다.
- 경로: 이것은 JMeter가 요청을 보내는 데 사용할 경로입니다.

수신기를 구성하려면 수신기를 선택하면 다음 옵션이 표시됩니다.

![JMeter 수신기 옵션](https://i.imgur.com/OcTGiuk.png)

- 출력 파일: JMeter가 테스트 결과를 출력하는 데 사용할 파일입니다.
- 형식: 결과가 출력되는 형식입니다.

## 테스트 실행

테스트 계획을 구성했으면 테스트를 실행할 준비가 된 것입니다. 테스트를 실행하려면 테스트 계획을 선택하고 실행 버튼을 클릭합니다.

![JMeter 실행 테스트](https://i.imgur.com/L1G5fvk.png)

이제 JMeter가 테스트를 실행하고 리스너에서 결과를 볼 수 있습니다.

![JMeter 테스트 결과](https://i.imgur.com/Y6UgR8W.png)

## 결과 분석

테스트 결과를 분석하여 시스템 또는 애플리케이션의 성능을 확인할 수 있습니다.

다음 메트릭을 사용하여 결과를 분석할 수 있습니다.

- 처리량: 시스템 또는 애플리케이션이 초당 처리할 수 있는 요청 수입니다.
- 평균 응답 시간: 시스템 또는 애플리케이션이 요청에 응답하는 데 걸리는 평균 시간입니다.
- 백분위수: 응답하는 데 일정 시간이 걸리는 요청의 비율입니다.

## 추가 정보

- 시스템이나 애플리케이션의 버그를 찾기 위해 로드 테스트를 사용해서는 안 된다는 점에 유의해야 합니다.
- 부하 테스트를 사용하여 다양한 유형의 사용자 행동을 시뮬레이션할 수 있습니다.
- JMeter는 웹 애플리케이션과 웹 서비스를 모두 테스트하는 데 사용할 수 있습니다.

## 참조

- 아파치 JMeter: https://jmeter.apache.org/
- JMeter 튜토리얼: https://www.tutorialspoint.com/jmeter/jmeter_tutorial.pdf
- JMeter 사용자 설명서: https://jmeter.apache.org/usermanual/index.html