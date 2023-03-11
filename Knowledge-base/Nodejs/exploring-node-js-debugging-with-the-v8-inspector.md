---
title: V8 Inspector로 Node.js 디버깅 살펴보기
description: 
published: true
date: 2023-03-11T15:32:53.346Z
tags: 
editor: markdown
dateCreated: 2023-03-11T15:32:53.346Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Exploring Node.js Debugging with the V8 Inspector***English** document is available*](/en/Knowledge-base/Nodejs/exploring-node-js-debugging-with-the-v8-inspector)
{.links-list}

V8 Inspector로 Node.js 디버깅 살펴보기

Node.js 개발 세계에서 디버깅은 코드 오류를 찾아 수정하는 중요한 프로세스입니다. Node.js에는 기본 제공 디버거가 있으며 많은 타사 디버깅 도구를 사용할 수 있습니다. 가장 강력한 디버깅 도구 중 하나는 버전 6.3부터 Node.js와 통합된 V8 Inspector입니다.

이 기사에서는 V8 Inspector를 살펴보고 이를 Node.js 애플리케이션 디버깅에 사용하는 방법을 배웁니다. 또한 중단점 설정 및 메모리 사용 검사를 포함하여 V8 Inspector의 고급 기능 중 일부를 다룰 것입니다.

## V8 인스펙터란?

V8 Inspector는 Google Chrome 브라우저와 통합된 디버깅 도구입니다. 이를 통해 개발자는 V8 엔진에서 실행 중인 JavaScript 코드를 검사하고 디버그할 수 있습니다. V8 엔진은 Node.js와 Google Chrome 브라우저에서 사용되는 JavaScript 엔진입니다.

V8 Inspector에는 중단점 설정, 코드 단계별 실행 및 변수 검사와 같은 강력한 디버깅 도구가 되는 많은 기능이 있습니다. 또한 개발자가 메모리 사용량을 검사할 수 있으므로 메모리 누수를 진단하는 데 특히 유용합니다.

## V8 검사기 활성화

Node.js 애플리케이션 디버깅을 위해 V8 Inspector를 사용하려면 Node.js 프로세스를 시작할 때 이를 활성화해야 합니다. 이는 `--inspect` 또는 `--inspect-brk` 플래그를 Node.js 명령에 전달하여 수행할 수 있습니다.

```bash
node --inspect app.js
```

`--inspect` 플래그는 Node.js에게 V8 Inspector를 시작하고 기본 포트인 9229에서 들어오는 연결을 수신하도록 지시합니다. `--inspect-brk` 플래그는 동일한 작업을 수행하지만 Node.js도 중지합니다. 코드가 실행되기 전에 중단점을 설정할 수 있습니다.

V8 Inspector가 활성화된 상태에서 Node.js 프로세스가 실행되면 Google Chrome 브라우저를 열고 `chrome://inspect`로 이동할 수 있습니다. 그러면 Chrome DevTools가 열리고 사용 가능한 디버깅 대상 목록이 표시됩니다.

## V8 인스펙터로 디버깅하기

V8 Inspector로 디버깅을 시작하려면 사용 가능한 디버깅 대상 목록에서 디버깅하려는 Node.js 프로세스를 선택하세요. 그러면 Node.js 프로세스에 연결된 새 DevTools 창이 열립니다.

여기에서 소스 탭으로 이동하여 Node.js 애플리케이션의 소스 코드를 볼 수 있습니다. 소스 코드에서 줄 번호를 클릭하거나 줄을 마우스 오른쪽 버튼으로 클릭하고 "중단점 추가"를 선택하여 중단점을 설정할 수 있습니다.

중단점이 설정되면 DevTools 창의 오른쪽 상단 모서리에 있는 컨트롤을 사용하여 코드를 단계별로 실행할 수 있습니다. "Step Over" 버튼은 현재 코드 줄을 실행하고 다음 줄로 이동하는 반면 "Step Into" 버튼은 함수 호출을 시작합니다. "Step Out" 버튼은 함수 호출에서 나갑니다.

DevTools 창에서 Variables 탭으로 이동하여 변수를 검사할 수도 있습니다. 그러면 현재 범위의 모든 변수 목록이 표시됩니다. 각 변수를 확장하여 해당 값과 속성 또는 메서드를 볼 수 있습니다.

## V8 Inspector의 고급 기능

기본 디버깅 기능 외에도 V8 Inspector에는 복잡한 문제를 진단하는 데 유용한 몇 가지 고급 기능이 있습니다.

### 조건부 중단점 설정

특정 조건이 충족되는 경우에만 중단점을 설정하려는 경우가 있습니다. 코드 줄을 마우스 오른쪽 버튼으로 클릭하고 "중단점 편집"을 선택하면 됩니다. 여기에서 중단점이 적중되기 위해 참이어야 하는 조건을 설정할 수 있습니다.

### 메모리 사용량 검사

메모리 누수는 진단하기 어려운 문제일 수 있지만 V8 Inspector를 사용하면 메모리 사용량을 쉽게 검사할 수 있습니다. 이렇게 하려면 DevTools 창에서 Memory 탭으로 이동합니다. 그러면 시간 경과에 따른 메모리 사용량 그래프와 현재 메모리에 있는 개체 목록이 표시됩니다. 개체를 클릭하여 해당 속성 및 참조를 볼 수 있습니다.

### 명령줄 API 사용

V8 Inspector에는 Node.js 프로세스 컨텍스트에서 JavaScript 명령을 실행할 수 있는 명령줄 API도 있습니다. 이것은 변수를 검사하거나 Node.js 애플리케이션의 일부가 아닌 코드를 실행하는 데 유용할 수 있습니다. Command Line API에 액세스하려면 DevTools 창에서 Console 탭으로 이동합니다.

## 결론

V8 Inspector는 Node.js 애플리케이션에서 코드 오류를 찾고 수정하는 데 도움이 되는 강력한 디버깅 도구입니다. 중단점 설정, 변수 검사, 메모리 사용량 검사와 같은 기능을 갖춘 V8 Inspector는 모든 Node.js 개발자에게 필수적인 도구입니다.

외부 리소스:

- [Node.js 디버깅 가이드](https://nodejs.org/en/docs/guides/debugging-getting-started/)
- [Chrome DevTools로 Node.js 디버깅](https://blog.logrocket.com/debugging-node-js-with-chrome-devtools-7c4a1b5f81d1/)
- [V8 Inspector로 Node.js 디버깅하기](https://www.twilio.com/blog/debugging-node-js-v8-inspector)