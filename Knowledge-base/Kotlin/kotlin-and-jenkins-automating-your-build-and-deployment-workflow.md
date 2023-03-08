---
title: Kotlin 및 Jenkins: 빌드 및 배포 워크플로 자동화
description: 
published: true
date: 2023-01-31T16:24:40.957Z
tags: 
editor: markdown
dateCreated: 2023-01-31T16:24:39.371Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kotlin and Jenkins: Automating Your Build and Deployment Workflow***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-jenkins-automating-your-build-and-deployment-workflow)
{.links-list}




Kotlin은 IntelliJ IDEA Java IDE를 만든 회사인 JetBrains에서 만든 JVM 기반 언어입니다. 컴파일러가 컨텍스트에서 변수의 유형을 유추할 수 있음을 의미하는 유형 유추 기능이 있는 정적으로 유형이 지정되는 언어입니다. Kotlin은 Java와 완벽하게 호환되며 서버 측, 클라이언트 측 및 Android 개발에 사용할 수 있습니다.

Jenkins는 CI(연속 통합) 및 CD(연속 전달) 워크플로에 자주 사용되는 인기 있는 오픈 소스 자동화 서버입니다. Kotlin 애플리케이션의 빌드 및 배포 프로세스를 자동화하는 데 사용할 수 있습니다.

이 기사에서는 CI/CD용 Jenkins로 Kotlin 프로젝트를 설정하는 방법을 보여줍니다. 빌드 및 배포 프로세스를 시연하는 데 사용할 수 있는 샘플 Kotlin 애플리케이션도 제공합니다.

## Kotlin 프로젝트 설정

가장 먼저 해야 할 일은 Kotlin 프로젝트를 만드는 것입니다. 이 예시에서는 IntelliJ IDEA Kotlin 프로젝트 템플릿을 사용합니다.

IntelliJ IDEA를 열고 "새 프로젝트 만들기"를 선택합니다. "Kotlin/JVM" 프로젝트 유형을 선택하고 "다음"을 클릭합니다.

![새 프로젝트 만들기](https://i.imgur.com/EuYLb4z.png)

프로젝트에 이름을 지정하고 프로젝트 파일의 위치를 선택합니다. 또한 프로젝트에 대한 JDK를 선택해야 합니다. Kotlin과 호환되는 JDK 버전을 선택해야 합니다.

![프로젝트 설정](https://i.imgur.com/fvYg4UO.png)

"마침"을 클릭하여 프로젝트를 생성합니다.

## 샘플 Kotlin 애플리케이션 추가

이제 Kotlin 프로젝트가 있으므로 샘플 Kotlin 애플리케이션을 추가할 수 있습니다. 이 예에서는 간단한 "Hello, World!" 애플리케이션.

다음 코드를 사용하여 프로젝트에 새 Kotlin 파일을 만듭니다.

```kotlin
fun main(args: Array<String>) {
    println("Hello, World!")
}
```

이 코드는 "Hello, World!"를 인쇄합니다. 실행할 때 콘솔에.

## 젠킨스 설정

이제 Kotlin 프로젝트가 설정되었으므로 CI/CD 워크플로에 대해 Jenkins를 구성할 수 있습니다.

Kotlin 프로젝트에 Jenkins를 설정하기 위해 수행해야 할 몇 가지 작업이 있습니다.

- Kotlin 플러그인 설치
- Jenkins 작업 구성

### Kotlin 플러그인 설치

Jenkins용 Kotlin 플러그인은 Kotlin 프로젝트 빌드에 대한 지원을 추가합니다. 플러그인을 설치하려면 Jenkins 웹 인터페이스의 "플러그인 관리" 페이지로 이동하여 "사용 가능" 탭을 선택합니다. "kotlin"을 검색하고 결과 목록에서 "Kotlin Plugin"을 선택합니다. 플러그인을 설치하려면 "다시 시작하지 않고 설치"를 클릭하십시오.

![코틀린 플러그인](https://i.imgur.com/GtLbC5z.png)

### Jenkins 작업 구성

다음으로 Kotlin 프로젝트를 위한 Jenkins 작업을 생성해야 합니다. 이렇게 하려면 Jenkins 웹 인터페이스의 "새 항목" 페이지로 이동하여 "프리스타일 프로젝트" 옵션을 선택합니다.

![새 항목](https://i.imgur.com/SVxH7jy.png)

작업 이름을 지정하고 "확인"을 선택합니다.

작업 구성 페이지에는 작업을 설정하기 위해 수행해야 하는 몇 가지 작업이 있습니다.

- Kotlin 프로젝트용 Git 리포지토리 추가
- Kotlin 코드를 컴파일하는 빌드 단계 추가
- Kotlin 애플리케이션을 실행하기 위한 빌드 단계 추가

#### Git 저장소 추가

"소스 코드 관리" 섹션의 "SCM" 드롭다운 메뉴에서 "Git"을 선택합니다. "Repositories" 필드에 Kotlin 프로젝트의 Git 저장소 URL을 입력합니다.

![scm-설정](https://i.imgur.com/Vkzc0jA.png)

#### Kotlin 코드를 컴파일하는 빌드 단계 추가

"빌드" 섹션에서 "빌드 단계 추가"를 선택하고 옵션 목록에서 "Kotlin 컴파일러 호출"을 선택합니다.

"소스 파일" 필드에 프로젝트의 Kotlin 소스 파일 경로를 입력합니다. "Classpath" 필드에 Kotlin 표준 라이브러리의 경로를 입력합니다.

![빌드 설정](https://i.imgur.com/W0m7Ncu.png)

#### Kotlin 애플리케이션을 실행하기 위한 빌드 단계 추가

"빌드" 섹션에서 "빌드 단계 추가"를 선택하고 옵션 목록에서 "코틀린 스크립트 실행"을 선택합니다.

"스크립트" 필드에 다음 코드를 입력합니다.

```kotlin
println("Hello, World!")
```

이 코드는 "Hello, World!"를 인쇄합니다. 실행할 때 콘솔에.

![실행 설정](https://i.imgur.com/O0PFY0z.png)

작업 구성을 저장하려면 "저장"을 클릭하십시오.

## Jenkins 작업 실행

이제 Jenkins를 구성했으므로 작업을 실행할 수 있습니다. 이렇게 하려면 Jenkins 웹 인터페이스의 "지금 빌드" 페이지로 이동합니다.

![지금 빌드](https://i.imgur.com/pVk4U0N.png)

빌드 프로세스를 시작하려면 "지금 빌드"를 클릭하십시오.

빌드가 완료되면 "Hello, World!" 콘솔 출력에 인쇄된 메시지.

![빌드 출력](https://i.imgur.com/Vkzc0jA.png)

## 결론

이 기사에서는 Jenkins를 사용하여 CI/CD용 Kotlin 프로젝트를 설정하는 방법을 설명했습니다. 빌드 및 배포 프로세스를 시연하는 데 사용할 수 있는 샘플 Kotlin 애플리케이션도 제공했습니다.