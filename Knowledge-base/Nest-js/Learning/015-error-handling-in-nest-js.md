---
title: 015: Nest.js의 오류 처리
description: 
published: true
date: 2023-02-11T01:17:27.204Z
tags: 
editor: markdown
dateCreated: 2023-02-11T01:17:25.630Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [015: Error handling in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/015-error-handling-in-nest-js)
{.links-list}


# Nest.js의 오류 처리

웹 애플리케이션 개발은 까다로울 수 있습니다. 특히 오류 처리와 관련하여 그렇습니다. Nest.js에서 오류를 처리하는 방법에는 여러 가지가 있으며 이 게시물에서는 가장 일반적인 방법 중 일부를 살펴보겠습니다.

## 시도/잡기

try/catch 방법은 Nest.js에서 오류를 처리하는 가장 기본적인 방법입니다. 이 방법을 사용하려면 코드를 try 블록으로 래핑한 다음 catch 블록을 추가하여 발생할 수 있는 오류를 처리하기만 하면 됩니다.

다음은 간단한 예입니다.

```javascript
try {
  // do something that might throw an error
} catch (err) {
  // handle the error
}
```

오류가 발생하면 catch 블록에 의해 포착되어 그에 따라 처리될 수 있습니다.

## 비동기 오류 처리

비동기 코드(예: Promises 또는 async/await를 사용하는 코드)를 사용하는 경우에도 여전히 try/catch 메서드를 사용할 수 있습니다. 그러나 비동기 코드에서 발생하는 오류는 실제로 이벤트 루프의 다음 틱에서 포착된다는 사실을 알고 있어야 합니다.

즉, 비동기 코드 주변에 try/catch 블록이 있는 경우 catch 블록은 이벤트 루프의 다음 틱까지 실행되지 않습니다. 혼란스러울 수 있으므로 예를 살펴보겠습니다.

```javascript
try {
  // do something that might throw an error
  setTimeout(() => {
    throw new Error('something went wrong');
  }, 1000);
} catch (err) {
  // this catch block will not be executed until 1000ms have passed
}
```

위의 예에서 오류는 1000ms가 지날 때까지 포착되지 않습니다. 이는 setTimeout 함수가 비동기식이고 이벤트 루프의 다음 틱에서만 오류가 발생하기 때문입니다.

이를 방지하기 위해 Promise.catch 메서드를 사용할 수 있습니다.

```javascript
try {
  // do something that might throw an error
  setTimeout(() => {
    throw new Error('something went wrong');
  }, 1000);
} catch (err) {
  // this catch block will not be executed until 1000ms have passed
}

Promise.catch((err) => {
  // this catch block will be executed immediately
});
```

## 오류 처리 미들웨어

오류 처리를 중앙 집중화하려면 Nest.js 미들웨어를 사용할 수 있습니다. 미들웨어는 요청이 컨트롤러 코드에 도달하기 전에 실행되는 기능입니다. 이것은 오류 처리 논리를 배치하기에 완벽한 장소입니다.

미들웨어 기능을 생성하려면 @UseMiddleware 데코레이터를 사용해야 합니다.

```javascript
import { UseMiddleware, Middleware } from '@nestjs/common';

@Middleware()
export class ErrorHandlerMiddleware implements NestMiddleware {
  // your middleware logic goes here
}
```

그런 다음 미들웨어를 사용하려면 Nest.js 모듈에 등록해야 합니다.

```javascript
@Module({
  imports: [],
  controllers: [],
  providers: [],
  middleware: [ErrorHandlerMiddleware],
})
export class AppModule {}
```

이제 애플리케이션에서 발생하는 모든 오류는 미들웨어 기능에 의해 처리됩니다.

## 결론

보시다시피 Nest.js에서 오류를 처리하는 방법에는 여러 가지가 있습니다. 선택하는 방법은 특정 요구 사항에 따라 다릅니다. 그러나 이 게시물에 설명된 모든 방법은 Nest.js 애플리케이션의 오류를 처리하기 위한 좋은 출발점을 제공해야 합니다.