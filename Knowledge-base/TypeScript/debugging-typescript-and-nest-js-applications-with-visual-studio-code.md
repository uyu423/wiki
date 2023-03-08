---
title: Visual Studio Code로 TypeScript 및 Nest.js 애플리케이션 디버깅
description: 
published: true
date: 2023-02-01T15:23:48.032Z
tags: 
editor: markdown
dateCreated: 2023-02-01T15:23:46.441Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Debugging TypeScript and Nest.js Applications with Visual Studio Code***English** version of this document is available*](/en/Knowledge-base/TypeScript/debugging-typescript-and-nest-js-applications-with-visual-studio-code)
{.links-list}



# Visual Studio Code로 TypeScript 및 Nest.js 애플리케이션 디버깅

TypeScript는 정적 유형 검사 및 코드 리팩토링을 제공하는 강력한 언어입니다. Nest.js는 확장 가능한 서버측 애플리케이션을 구축하기 위한 프레임워크입니다. Visual Studio Code는 TypeScript 및 Nest.js에 대한 뛰어난 지원을 제공하는 인기 있는 코드 편집기입니다.

이 기사에서는 Visual Studio Code를 사용하여 TypeScript 및 Nest.js 애플리케이션을 디버깅하는 방법에 대해 설명합니다. 중단점을 설정하고 변수를 검사하고 콘솔을 사용하는 방법을 살펴보겠습니다. 또한 호출 스택 및 디버거 콘솔과 같은 디버거의 일부 고급 기능에 대해서도 알아봅니다.

## 디버거 설정

가장 먼저 해야 할 일은 디버거를 설정하는 것입니다. 이렇게 하려면 Visual Studio Code를 열고 `Ctrl+Shift+P`(Windows) 또는 `Cmd+Shift+P`(macOS)를 눌러 명령 팔레트를 엽니다. `debug`를 입력하고 `Debug: Open launch.json` 명령을 선택합니다.

그러면 `.vscode/launch.json` 파일이 열립니다. TypeScript 애플리케이션에 대한 구성을 추가해야 합니다. 구성은 다음과 같아야 합니다.

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "Launch Program",
            "program": "${workspaceFolder}/dist/index.js",
            "outFiles": [
                "${workspaceFolder}/dist/**/*.js"
            ]
        }
    ]
}
```

이 구성을 분석해 보겠습니다. `type` 속성은 디버거 유형을 지정합니다. Node.js 애플리케이션을 디버깅하고 있기 때문에 `node` 디버거를 사용하려고 합니다. `request` 속성은 실행 유형을 지정합니다. 디버거가 프로그램을 시작할 수 있도록 `launch` 요청을 사용하려고 합니다.

`name` 속성은 구성의 이름입니다. 이것은 디버그 드롭다운 목록에 표시될 이름입니다. `program` 속성은 디버깅하려는 프로그램의 경로입니다. 이 경우 `dist` 디렉토리에 있는 `index.js` 파일을 디버깅합니다.

`outFiles` 속성은 디버깅을 위해 고려해야 하는 파일을 지정하는 glob 패턴의 배열입니다. 이 경우 `dist` 디렉토리에 있는 모든 JavaScript 파일을 포함하고 있습니다.

## 디버거 실행

이제 시작 구성을 만들었으므로 디버거를 시작할 수 있습니다. 이렇게 하려면 `F5`를 누르거나 명령 팔레트에서 `디버그: 디버깅 시작` 명령을 선택하십시오. 그러면 디버거가 시작되고 프로그램에 연결됩니다.

## 예외에서 깨기

디버거의 가장 유용한 기능 중 하나는 예외를 중단하는 기능입니다. 이는 버그를 추적하려고 할 때 매우 유용할 수 있습니다. 이 기능을 활성화하려면 `.vscode/launch.json` 파일을 열고 `"stopOnEntry": true` 속성을 구성에 추가합니다. 이로 인해 디버거가 프로그램의 첫 번째 줄에서 중단됩니다.

## 중단점 설정

디버거의 또 다른 유용한 기능은 중단점을 설정하는 기능입니다. 중단점은 프로그램의 상태를 검사할 수 있도록 프로그램 실행이 중단되는 코드의 지점입니다. 중단점을 설정하려면 중단하려는 코드 줄을 클릭하기만 하면 됩니다. 중단점이 설정되었음을 나타내는 빨간색 점이 나타납니다.

## 변수 검사

프로그램 실행이 중단점에서 중단되면 변수 값을 검사할 수 있습니다. 이렇게 하려면 변수 위로 마우스를 가져가면 됩니다. 변수 값은 툴팁에 표시됩니다.

`디버그 콘솔`을 사용하여 변수를 검사할 수도 있습니다. `디버그 콘솔`을 열려면 `Ctrl+Shift+Y`(Windows) 또는 `Cmd+Shift+Y`(macOS)를 누르십시오. 출력 패널에 '디버그 콘솔'이 표시됩니다.

## 호출 스택 사용

`Call Stack` 패널은 디버깅에 매우 유용한 도구입니다. 프로그램 실행의 현재 지점으로 이어지는 함수 호출 시퀀스를 보여줍니다. `Call Stack` 패널을 열려면 `Ctrl+\`(Windows) 또는 `Cmd+\`(macOS)를 누릅니다.

## 결론

이 기사에서는 Visual Studio Code를 사용하여 TypeScript 및 Nest.js 애플리케이션을 디버깅하는 방법을 배웠습니다. 중단점을 설정하고 변수를 검사하고 콘솔을 사용하는 방법을 살펴보았습니다. 또한 호출 스택 및 디버거 콘솔과 같은 디버거의 일부 고급 기능에 대해서도 배웠습니다.