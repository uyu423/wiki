---
title: TypeScript 및 Node.js로 이미지 및 비디오 처리 애플리케이션 구축
description: 
published: true
date: 2023-02-08T20:17:42.070Z
tags: 
editor: markdown
dateCreated: 2023-02-08T20:17:40.454Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building Image and Video Processing Applications with TypeScript and Node.js***English** document is available*](/en/Knowledge-base/TypeScript/building-image-and-video-processing-applications-with-typescript-and-node-js)
{.links-list}


# TypeScript 및 Node.js로 이미지 및 비디오 처리 애플리케이션 구축

확장 가능한 이미지 및 비디오 처리 응용 프로그램을 만들려는 개발자는 프로그래밍 언어와 관련하여 다양한 선택을 할 수 있습니다. 종종 간과되는 한 가지 옵션은 TypeScript입니다. TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 초보자가 배우기 쉽고 숙련된 개발자가 활용할 수 있는 고급 기능이 있는 언어입니다.

Node.js는 Chrome의 V8 JavaScript 엔진에 구축된 JavaScript 런타임입니다. 서버 측 응용 프로그램을 개발하는 데 사용됩니다. Node.js 애플리케이션은 JavaScript로 작성되며 Windows, macOS 및 Linux를 비롯한 다양한 플랫폼에서 실행할 수 있습니다.

이 기사에서는 TypeScript와 Node.js를 사용하여 이미지 처리 애플리케이션을 빌드하는 방법을 보여줍니다. GraphicsMagick 라이브러리를 감싸는 TypeScript 라이브러리인 gm을 사용할 것입니다. GraphicsMagick은 이미지를 생성, 편집 및 변환하는 데 사용할 수 있는 크로스 플랫폼 이미지 처리 툴킷입니다.

gm 라이브러리는 이미지 크기 조정, 자르기 및 변환과 같은 일반적인 이미지 처리 작업을 수행하기 위한 간단한 API를 제공합니다. 명령줄 및 웹 응용 프로그램을 만드는 데 사용할 수 있습니다. 이 문서에서는 이미지 크기를 조정하는 명령줄 응용 프로그램을 만들 것입니다.

## TypeScript 및 Node.js 설치

애플리케이션 작성을 시작하기 전에 TypeScript와 Node.js를 설치해야 합니다. TypeScript는 Node.js 패키지 관리자인 npm을 사용하여 설치할 수 있습니다. TypeScript를 설치하려면 터미널을 열고 다음 명령을 실행합니다.

```
npm install -g typescript
```

이렇게 하면 TypeScript 컴파일러인 tsc와 TypeScript 언어 서버인 tsserver가 설치됩니다. TypeScript 컴파일러는 TypeScript 코드를 JavaScript 코드로 컴파일하는 데 사용됩니다. TypeScript 언어 서버는 TypeScript 코드에 대한 코드 완성 및 유형 검사와 같은 언어 서비스를 제공합니다.

Node.js는 Node.js 웹 사이트에서 다운로드할 수 있습니다. Node.js가 설치되면 npm 명령줄 인터페이스를 사용할 수 있습니다.

## TypeScript 프로젝트 만들기

이제 TypeScript와 Node.js가 설치되었으므로 TypeScript 프로젝트를 만들 수 있습니다. 이를 위해 npm init 명령을 사용합니다. 이 명령은 Node.js 프로젝트의 종속성을 관리하는 데 사용되는 package.json 파일을 생성합니다.

TypeScript 프로젝트를 만들려면 터미널을 열고 프로젝트를 만들 디렉터리로 이동합니다. 그런 다음 다음 명령을 실행합니다.

```
npm init
```

이렇게 하면 프로젝트의 이름 및 버전과 같은 여러 가지 질문이 표시됩니다. 프로젝트의 경우 이름을 "image-processing-app"으로, 버전을 "1.0.0"으로 설정합니다.

package.json 파일이 생성되면 프로젝트에 대한 종속성을 설치할 수 있습니다. 우리 프로젝트의 경우 gm TypeScript 정의와 gm 라이브러리를 설치해야 합니다. 이렇게 하려면 다음 명령을 실행합니다.

```
npm install --save @types/gm gm
```

그러면 gm TypeScript 정의와 gm 라이브러리가 node_modules 디렉토리에 설치됩니다. gm TypeScript 정의는 gm 라이브러리에 대한 TypeScript 바인딩을 제공합니다.

## 이미지 크기 조정

이제 프로젝트가 설정되었으므로 애플리케이션 작성을 시작할 수 있습니다. 가장 먼저 해야 할 일은 gm 라이브러리를 가져오는 것입니다. main.ts 파일 맨 위에 다음 줄을 추가하면 됩니다.

```typescript
import * as gm from "gm";
```

이렇게 하면 gm 네임스페이스를 파일로 가져옵니다. 이제 gm 네임스페이스를 사용하여 gm 라이브러리의 기능에 액세스할 수 있습니다.

다음으로 해야 할 일은 이미지를 여는 것입니다. gm.open() 함수를 사용하여 이를 수행할 수 있습니다. 이 함수는 이미지에 대한 경로를 첫 번째 인수로 사용하고 콜백 함수를 두 번째 인수로 사용합니다. 콜백 함수는 오류 개체 및 gm 개체와 함께 호출됩니다. gm 개체는 이미지에 대한 작업을 수행하는 데 사용할 수 있습니다.

다음과 같이 이미지를 열고 gm 객체를 resize() 함수에 전달할 수 있습니다.

```typescript
gm.open("input.jpg", (err, image) => {
  if (err) {
    console.log(err);
  } else {
    resize(image);
  }
});
```

resize() 함수는 gm 객체를 가져와 이미지 크기를 조정합니다. 다음과 같이 resize() 함수를 정의할 수 있습니다.

```typescript
function resize(image: gm.Image): void {
  image
    .resize(100, 100)
    .write("output.jpg", (err) => {
      if (err) {
        console.log(err);
      }
    });
}
```

이 함수는 이미지의 크기를 100x100픽셀로 조정하고 출력을 output.jpg 파일에 기록합니다.

애플리케이션을 실행하기 위해 TypeScript 컴파일러인 tsc를 사용할 수 있습니다. 다음 명령을 실행하여 코드를 컴파일할 수 있습니다.

```
tsc main.ts
```

그러면 현재 디렉토리에 main.js 파일이 생성됩니다. 다음 명령을 실행하여 애플리케이션을 실행할 수 있습니다.

```
node main.js
```

이렇게 하면 input.jpg 이미지의 크기가 조정되고 출력이 output.jpg 파일에 저장됩니다.

## 결론

이 기사에서는 TypeScript와 Node.js를 사용하여 이미지 처리 애플리케이션을 빌드하는 방법을 보여주었습니다. gm 라이브러리를 사용하여 이미지 크기를 조정하는 방법을 살펴보았습니다. 이 응용 프로그램은 이미지 자르기 및 변환과 같은 다른 이미지 처리 작업을 수행하도록 쉽게 확장할 수 있습니다.