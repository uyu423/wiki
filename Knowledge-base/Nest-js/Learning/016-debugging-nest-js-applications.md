---
title: 016: Nest.js 애플리케이션 디버깅
description: 
published: true
date: 2023-02-15T01:32:19.921Z
tags: 
editor: markdown
dateCreated: 2023-02-15T01:32:18.359Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [016: Debugging Nest.js applications***English** document is available*](/en/Knowledge-base/Nest-js/Learning/016-debugging-nest-js-applications)
{.links-list}


# Nest.js 애플리케이션 디버깅

Nest.js는 서버 측 애플리케이션을 구축하기 위한 Node.js 프레임워크입니다. TypeScript를 사용하며 Express를 기반으로 합니다.

Nest.js 애플리케이션 디버깅은 일반적으로 Node.js 애플리케이션을 디버그하는 여러 가지 방법이 있고 Nest.js는 그 위에 고유한 복잡성을 추가하기 때문에 어려울 수 있습니다. 이 게시물에서는 Nest.js 애플리케이션 디버깅의 몇 가지 기본 사항을 살펴보겠습니다.

## Node.js 애플리케이션 디버깅

Node.js 애플리케이션은 다양한 방법으로 디버깅할 수 있습니다. 가장 일반적인 방법은 `debug` 명령으로 호출할 수 있는 Node.js 디버거를 사용하는 것입니다.

```
$ node debug <script.js>
```

이렇게 하면 Node.js 디버거가 시작되고 명령을 입력할 수 있는 프롬프트가 표시됩니다. 전체 명령 목록을 보려면 프롬프트에 `help`를 입력하십시오.

Node.js 애플리케이션을 디버깅하는 또 다른 방법은 Visual Studio Code에서 제공하는 것과 같은 그래픽 디버거를 사용하는 것입니다. 이를 사용하려면 Visual Studio Code용 Node.js 확장을 설치해야 합니다.

확장이 설치되면 Visual Studio Code에서 Nest.js 프로젝트를 열고 코드에 중단점을 설정할 수 있습니다. 디버거를 시작하려면 F5 키를 누르거나 작업 표시줄에서 디버그 아이콘을 클릭합니다.

## Nest.js 애플리케이션 디버깅

Nest.js는 Node.js 위에 자체 계층을 추가하므로 Nest.js 애플리케이션 디버깅 방법은 Node.js 애플리케이션 디버깅 방법과 유사합니다.

Nest.js 애플리케이션을 디버그하는 가장 일반적인 방법은 Nest.js CLI에서 제공하는 `nest` 명령을 사용하는 것입니다.

```
$ nest debug <script.ts>
```

이렇게 하면 Nest.js 디버거가 시작되고 명령을 입력할 수 있는 프롬프트가 표시됩니다. 전체 명령 목록을 보려면 프롬프트에 `help`를 입력하십시오.

Nest.js 애플리케이션을 디버깅하는 또 다른 방법은 Visual Studio Code에서 제공하는 것과 같은 그래픽 디버거를 사용하는 것입니다. 이를 사용하려면 Visual Studio Code용 Nest.js 확장을 설치해야 합니다.

확장이 설치되면 Visual Studio Code에서 Nest.js 프로젝트를 열고 코드에 중단점을 설정할 수 있습니다. 디버거를 시작하려면 F5 키를 누르거나 작업 표시줄에서 디버그 아이콘을 클릭합니다.

## 추가 정보

- [Node.js 애플리케이션 디버깅](https://nodejs.org/en/docs/guides/debugging-getting-started/)
- [Nest.js 애플리케이션 디버깅](https://docs.nestjs.com/cli/debug)
- [Nest.js용 Visual Studio 코드 확장](https://marketplace.visualstudio.com/items?itemName=nestjs.nest-cli)