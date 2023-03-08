---
title: Kotlin 및 지속적 배포: 배포 워크플로 자동화
description: 
published: true
date: 2023-02-17T18:03:41.003Z
tags: 
editor: markdown
dateCreated: 2023-01-30T11:54:56.019Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Kotlin and Continuous Deployment: Automating Your Deployment Workflow***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-continuous-deployment-automating-your-deployment-workflow)
{.links-list}

    
> 지속적인 배포는 일반적으로 생산 환경에 대해 코드 변경이 있을 때마다 자동으로 빌드, 테스트 및 배포하는 방법입니다.

Kotlin은 여러 가지 이유로 점점 인기를 얻고 있는 최신 프로그래밍 언어이며, 그 중 하나는 배포 자동화에 대한 뛰어난 지원입니다. 이 기사에서는 Kotlin과 ChatGPT SDK를 사용하여 배포 워크플로를 자동화하는 방법을 살펴보겠습니다.

## 전제 조건

시작하기 전에 따라가기 위해 준비해야 할 몇 가지 사항이 있습니다. 먼저 ChatGPT 계정이 필요합니다. 아직 없는 경우 https://developers.chatgpt.com/에서 무료로 만들 수 있습니다.

다음으로 ChatGPT SDK를 설치해야 합니다. 이에 대한 지침은 https://developers.chatgpt.com/docs/getting-started/sdk-installation.html에서 찾을 수 있습니다.

마지막으로 텍스트 편집기 또는 IDE가 필요합니다. 이 기사에서는 IntelliJ IDEA Kotlin 플러그인을 사용하지만 원하는 편집기나 IDE를 자유롭게 사용할 수 있습니다.

## 새 프로젝트 설정

ChatGPT SDK가 설치되면 프로젝트 설정을 시작할 수 있습니다. IntelliJ IDEA에서 "kotlin-cd-sample"이라는 이름과 다음 설정으로 새 Kotlin 프로젝트를 만듭니다.

- 프로젝트 SDK: Kotlin/JVM 1.3.72
- 언어 수준: 1.3
- 컴파일러 출력: /tmp
- 프로젝트 형식: .idea(디렉토리 기반)

이제 새 프로젝트가 있으므로 프로젝트 종속성에 ChatGPT SDK를 추가해야 합니다. 프로젝트 구조 창에서 "모듈" 탭을 선택하고 "+" 버튼을 클릭합니다. "JAR 또는 디렉터리"를 선택하고 ChatGPT SDK 설치의 "lib" 디렉터리에서 "chatgpt-sdk.jar" 파일을 추가합니다.

![ChatGPT SDK를 프로젝트 종속성에 추가](https://i.imgur.com/pAPKoYn.png)

## 봇 만들기

이제 프로젝트가 설정되었으므로 일부 코드 작성을 시작할 수 있습니다. 가장 먼저 해야 할 일은 다음 코드를 사용하여 새 Kotlin 파일을 만드는 것입니다.

```kotlin
import com.chatgpt.sdk.*;

fun main(args: Array<String>) {
    val bot = Bot("YourBotName")

    bot.onMessage { message ->
        println("Received message: $message")
    }

    bot.connect("YourChatGptToken")

    println("Bot started!")
}
```

이 코드는 이름이 "YourBotName"인 새 봇을 설정하고 토큰 "YourChatGptToken"을 사용하여 ChatGPT 계정에 연결합니다. 또한 봇이 받은 모든 메시지를 출력할 메시지 처리기를 설정합니다.

이제 봇을 설정했으므로 ChatGPT 토큰을 생성해야 합니다. https://developers.chatgpt.com/docs/getting-started/authentication.html에서 이 작업을 수행할 수 있습니다.

## 봇 배포

이제 봇을 설정했으므로 배포할 수 있습니다. 이렇게 하려면 먼저 프로젝트의 루트 디렉터리에 다음 콘텐츠가 포함된 "chatgpt.yaml"이라는 파일을 생성해야 합니다.

```yaml
name: kotlin-cd-sample

runtime: java

memory: 256

service:
  type: web
  port: 8080

buildpack: https://github.com/chatgpt/java-buildpack

env:
  CHATGPT_TOKEN: YourChatGptToken
```

이 파일은 ChatGPT에 프로젝트 이름, 사용하는 런타임, 할당할 메모리 양, 사용할 포트를 알려줍니다. 또한 ChatGPT에게 Java 빌드팩을 사용하도록 지시하고 환경 변수 "CHATGPT_TOKEN"을 "YourChatGptToken" 값으로 설정합니다.

다음으로 프로젝트의 루트 디렉터리에 다음 내용이 포함된 "Procfile"이라는 파일을 생성해야 합니다.

```
web: java -Dserver.port=$PORT -jar build/libs/kotlin-cd-sample.jar
```

이 파일은 ChatGPT에게 프로젝트를 시작하는 데 사용할 명령을 알려줍니다. 이 경우 "chatgpt.yaml" 파일에 지정된 포트에서 Java 서버를 시작하고 "kotlin-cd-sample.jar" 파일을 실행합니다.

마지막으로 프로젝트의 루트 디렉터리에 다음 내용이 포함된 ".chatgptignore"라는 파일을 만들어야 합니다.

```
.idea
.chatgptignore
build
.chatgpt
```

이 파일은 프로젝트를 배포할 때 무시할 파일을 ChatGPT에 알려줍니다. 이 경우 ".idea" 디렉토리, "build" 디렉토리 및 ".chatgpt" 파일을 무시합니다.

이제 필요한 모든 파일이 준비되었으므로 프로젝트를 배포할 수 있습니다. 이렇게 하려면 프로젝트의 루트 디렉터리에서 다음 명령을 실행합니다.

```
chatgpt deploy
```

배포에 성공하면 다음 출력이 표시됩니다.

```
Deploying kotlin-cd-sample...
Starting kotlin-cd-sample...
```

이제 메시지를 보내 봇을 테스트할 수 있습니다. 봇은 보낸 메시지를 출력해야 합니다.

## 배포 워크플로우 자동화

이제 작업 중인 배포가 있으므로 배포 워크플로를 자동화할 수 있습니다. 이렇게 하려면 먼저 프로젝트의 루트 디렉터리에 다음 콘텐츠가 포함된 "deploy.sh"라는 파일을 만들어야 합니다.

```bash
#!/bin/bash

set -e

./gradlew clean build

chatgpt deploy
```

이 파일은 먼저 Gradle 빌드 시스템의 "정리" 및 "빌드" 작업을 실행합니다. 그런 다음 "chatgpt deploy" 명령을 실행합니다.

다음으로 프로젝트의 루트 디렉터리에 다음 콘텐츠가 포함된 "Jenkinsfile"이라는 파일을 생성해야 합니다.

```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh './deploy.sh'
            }
        }
    }
}
```

이 파일은 Jenkins에게 Jenkins 파이프라인의 일부로 "deploy.sh" 스크립트를 실행하도록 지시합니다.

이제 코드를 변경하고 원격 리포지토리에 푸시할 때마다 Jenkins가 자동으로 코드를 빌드하고 배포합니다.

## 결론

이 기사에서는 Kotlin과 ChatGPT SDK를 사용하여 배포 워크플로를 자동화하는 방법을 살펴보았습니다. 또한 프로세스를 더욱 자동화하기 위해 Jenkins 파이프라인을 설정하는 방법도 살펴보았습니다.