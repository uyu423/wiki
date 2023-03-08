---
title: TypeScript 애플리케이션 디버깅 및 문제 해결
description: 
published: true
date: 2023-02-24T04:32:17.464Z
tags: 
editor: markdown
dateCreated: 2023-02-24T04:32:16.131Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Debugging and Troubleshooting TypeScript Applications***English** document is available*](/en/Knowledge-base/TypeScript/debugging-and-troubleshooting-typescript-applications)
{.links-list}


# TypeScript 애플리케이션 디버깅 및 문제 해결

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 클래스, 모듈 및 인터페이스에 대한 지원을 제공합니다. TypeScript는 개발 프로세스 초기에 오류를 포착하는 데 도움이 되는 정적 유형 검사 때문에 웹 개발자들 사이에서 인기가 있습니다.

TypeScript 사용의 이점에도 불구하고 TypeScript 애플리케이션 디버깅은 어려울 수 있습니다. 이는 TypeScript가 런타임에 해석되는 JavaScript로 컴파일되기 때문입니다. 이것은 TypeScript 코드가 브라우저에서 직접 실행되지 않는다는 것을 의미합니다.

TypeScript 애플리케이션 디버깅에 도움이 되는 몇 가지 도구가 있습니다. 첫 번째는 TypeScript 컴파일러입니다. TypeScript 컴파일러는 TypeScript 코드에서 구문 오류를 찾는 데 도움이 될 수 있습니다. 두 번째는 Visual Studio Code의 디버거와 같은 디버깅 도구입니다. 디버거는 TypeScript 코드에서 런타임 오류를 찾는 데 도움이 될 수 있습니다.

TypeScript 컴파일러는 TypeScript 코드에서 구문 오류를 찾는 데 도움이 될 수 있습니다. TypeScript 컴파일러를 사용하려면 Visual Studio Code에서 TypeScript 파일을 엽니다. TypeScript 파일에서 왼쪽 여백에 있는 TypeScript 아이콘을 클릭합니다. 그러면 TypeScript 컴파일러 오류 출력 패널이 열립니다. TypeScript 컴파일러는 TypeScript 코드의 구문 오류를 보고합니다.

![TypeScript 컴파일러 오류](https://i.imgur.com/p0SfNcu.png)

디버거는 TypeScript 코드에서 런타임 오류를 찾는 데 도움이 될 수 있습니다. 디버거를 사용하려면 Visual Studio Code에서 TypeScript 파일을 엽니다. TypeScript 파일에서 코드 줄에 중단점을 설정합니다. 중단점은 디버거가 실행을 일시 중지하는 코드의 지점입니다. 중단점을 설정하려면 코드 행을 클릭하고 F9를 누르십시오.

![중단점 설정](https://i.imgur.com/FwRoJjl.png)

그런 다음 디버그 패널을 엽니다. 디버그 패널의 드롭다운에서 TypeScript 파일을 선택합니다. 이렇게 하면 디버거가 시작되고 브라우저에서 TypeScript 파일이 시작됩니다. 디버거는 중단점에서 실행을 일시 중지합니다.

![디버그 TypeScript](https://i.imgur.com/cgqUMjN.png)

디버그 패널에서 범위 섹션의 변수 값을 볼 수 있습니다. 호출 스택 섹션에서 호출 스택을 볼 수도 있습니다. 호출 스택은 현재 코드 라인으로 이어진 함수 호출 시퀀스를 보여줍니다.

![디버그 패널](https://i.imgur.com/eZUjPxa.png)

실행을 계속하려면 재생 버튼을 클릭하거나 F5를 누르십시오. 이렇게 하면 실행이 재개되고 디버거가 다음 중단점까지 실행됩니다.

TypeScript 애플리케이션 디버깅에 도움이 되는 다른 많은 도구가 있습니다. 보다 포괄적인 목록은 [디버깅 TypeScript](https://www.typescriptlang.org/docs/handbook/debugging.html)를 참조하세요.