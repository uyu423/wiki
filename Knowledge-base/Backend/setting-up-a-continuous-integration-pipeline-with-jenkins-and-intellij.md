---
title: Jenkins 및 IntelliJ로 지속적인 통합 파이프라인 설정
description: 
published: true
date: 2023-02-13T13:18:15.332Z
tags: 
editor: markdown
dateCreated: 2023-02-13T13:18:08.213Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Setting up a Continuous Integration Pipeline with Jenkins and IntelliJ***English** document is available*](/en/Knowledge-base/Backend/setting-up-a-continuous-integration-pipeline-with-jenkins-and-intellij)
{.links-list}


# Jenkins 및 IntelliJ로 지속적인 통합 파이프라인 설정

## 소개

CI(연속 통합)는 개발자가 하루에 여러 번 코드를 공유 리포지토리에 통합해야 하는 개발 관행입니다. 각 체크인은 자동화된 빌드로 확인되어 팀이 문제를 조기에 감지할 수 있습니다.

CI 파이프라인 설정은 어려운 작업일 수 있지만 올바른 도구를 사용하면 상대적으로 간단할 수 있습니다. 이 기사에서는 Jenkins와 IntelliJ를 사용하여 CI 파이프라인을 설정하는 방법을 보여줍니다.

## 필요한 것

- GitHub 계정
- 젠킨스 서버
- IntelliJ IDEA

## 1단계: GitHub 리포지토리 생성

첫 번째 단계는 프로젝트에 대한 GitHub 리포지토리를 만드는 것입니다. 이렇게 하려면 GitHub로 이동하여 새 리포지토리를 만듭니다.

![새 GitHub 저장소 만들기](https://i.imgur.com/EuU8GtO.png)

리포지토리 이름을 지정하고 "리포지토리 생성"을 클릭합니다.

![저장소 이름 지정](https://i.imgur.com/VNcuCY5.png)

## 2단계: Jenkins 작업 생성

다음으로 Jenkins 작업을 생성해야 합니다. Jenkins 작업은 Jenkins가 실행할 수 있는 작업입니다. 우리의 경우 Jenkins 작업은 GitHub에서 코드를 체크아웃하고 빌드하고 테스트를 실행합니다.

Jenkins 작업을 만들려면 Jenkins 서버로 이동하여 "새 작업"을 클릭합니다.

![젠킨스 새 직업](https://i.imgur.com/pLJnV1N.png)

작업 이름을 지정하고 "자유 형식 프로젝트"를 선택합니다.

![ Jenkins 작업 이름](https://i.imgur.com/lGZm4z3.png)

"확인"을 클릭합니다.

다음 페이지에서 "소스 코드 관리" 섹션까지 아래로 스크롤하고 "Git"을 선택합니다.

![젠킨스 소스코드 관리](https://i.imgur.com/Lg4U4jf.png)

"리포지토리 URL" 필드에 GitHub 리포지토리의 URL을 입력합니다.

![Jenkins 저장소 URL](https://i.imgur.com/VkzM0cw.png)

"빌드" 섹션까지 아래로 스크롤하고 "빌드 단계 추가"를 클릭합니다. "셸 실행"을 선택합니다.

![Jenkins 빌드 섹션](https://i.imgur.com/KJ3fZUO.png)

"명령" 필드에 다음 명령을 입력합니다.

```
mvn clean install
```

이 명령은 프로젝트를 정리하고 종속성을 설치하고 테스트를 실행합니다.

"빌드 후 작업" 섹션까지 아래로 스크롤하고 "빌드 후 작업 추가"를 클릭합니다. "JUnit 테스트 결과 보고서 게시"를 선택합니다.

![Jenkins 빌드 후 작업](https://i.imgur.com/NDYaTGi.png)

"테스트 보고서 XML" 필드에 다음을 입력합니다.

```
**/target/surefire-reports/*.xml
```

이것은 Jenkins에게 테스트 결과를 게시하도록 지시합니다.

"저장"을 클릭합니다.

## 3단계: IntelliJ 설정

이제 Jenkins 작업이 설정되었으므로 IDE를 구성해야 합니다. 이 섹션에서는 코드를 변경할 때 Jenkins 서버에서 빌드를 트리거하도록 IntelliJ를 설정하는 방법을 보여줍니다.

IntelliJ를 열고 "파일" 메뉴로 이동합니다. "설정"을 선택합니다.

![IntelliJ 설정](https://i.imgur.com/mEUDKjK.png)

"설정" 창에서 "빌드, 실행, 배포" > "지속적인 통합"으로 이동합니다. "젠킨스"를 선택합니다.

![IntelliJ Jenkins](https://i.imgur.com/VkzM0cw.png)

"Jenkins URL" 필드에 Jenkins 서버의 URL을 입력합니다.

![IntelliJ Jenkins URL](https://i.imgur.com/dc9gKbD.png)

"프로젝트 이름" 필드에 Jenkins 작업의 이름을 입력합니다.

![IntelliJ 프로젝트 이름](https://i.imgur.com/P0zM0cw.png)

"확인"을 클릭합니다.

## 4단계: 빌드 트리거

이제 Jenkins 작업이 설정되고 IDE가 구성되었으므로 빌드를 트리거할 준비가 되었습니다. 이렇게 하려면 코드를 변경하고 GitHub에 푸시합니다.

![GitHub에 IntelliJ 푸시](https://i.imgur.com/VkzM0cw.png)

코드를 GitHub에 푸시하면 Jenkins가 자동으로 변경 사항을 감지하고 코드를 체크아웃하고 빌드하고 테스트를 실행합니다.

![젠킨스 빌드](https://i.imgur.com/u4JnV1N.png)

"빌드 기록" 섹션에서 "빌드" 링크를 클릭하여 빌드 결과를 볼 수 있습니다.

![Jenkins 빌드 히스토리](https://i.imgur.com/ VkzM0cw.png)

## 결론

이 기사에서는 Jenkins와 IntelliJ를 사용하여 CI 파이프라인을 설정하는 방법을 설명했습니다. 이것은 간단한 파이프라인이지만 스테이징 또는 프로덕션 환경에 배포하는 것과 같은 추가 단계를 포함하도록 쉽게 확장할 수 있습니다.