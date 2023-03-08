---
title: 021: Nest.js에서 커스텀 파이프 만들기
description: 
published: true
date: 2023-02-15T02:32:19.000Z
tags: 
editor: markdown
dateCreated: 2023-02-15T02:32:17.104Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [021: Creating custom pipes in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/021-creating-custom-pipes-in-nest-js)
{.links-list}


# Nest.js에서 커스텀 파이프 만들기

파이프는 Nest.js에서 데이터를 변환하는 좋은 방법입니다. 이 게시물에서는 사용자 지정 파이프를 만드는 방법을 배웁니다.

## 파이프란?

파이프는 애플리케이션을 통해 데이터가 흐를 때 데이터를 변환할 수 있는 Nest.js의 기능입니다. 예를 들어 파이프를 사용하여 문자열을 대문자로 변환하거나 날짜 형식을 지정할 수 있습니다.

파이프는 다음을 포함하여 Nest.js의 다양한 위치에서 사용할 수 있습니다.

- 컨트롤러에서 경로에서 사용되기 전에 데이터를 변환하기 위해
- 서비스에서 데이터가 데이터베이스에 저장되기 전에 데이터 변환
- 클라이언트에 반환되기 전에 데이터를 변환하기 위해 파이프에서

## 커스텀 파이프 생성 방법

사용자 지정 파이프를 만드는 것은 간단합니다. 먼저 `pipes` 디렉토리에 새 파일을 만들어야 합니다. 파일 이름은 `.pipe.ts`로 끝나야 합니다.

다음으로 `@nestjs/common`에서 `PipeTransform` 인터페이스를 가져와야 합니다.

```typescript
import { PipeTransform } from '@nestjs/common';
```

`PipeTransform` 인터페이스는 `transform`이라는 단일 메서드를 정의합니다. 이 방법은 데이터를 변환하는 데 사용됩니다. 이 메서드는 두 가지 인수를 허용합니다.

- `값`: 변환할 데이터입니다. 모든 데이터 유형이 될 수 있습니다.
- `metadata`: 값에 대한 메타데이터입니다. 이것은 다음과 같은 속성을 가진 개체입니다.
  - `유형`: 값의 데이터 유형입니다. 이는 데이터가 올바른 유형인지 확인하는 데 유용합니다.
  - `데이터`: 값과 관련된 기타 모든 데이터입니다. 이는 변환에 컨텍스트를 제공하는 데 유용합니다.

`transform` 메서드는 변환된 데이터를 반환해야 합니다.

예를 들어 보겠습니다. 문자열 목록이 있고 문자열을 대문자로 변환하려고 한다고 가정합니다. 다음 파이프를 사용하여 이를 수행할 수 있습니다.

```typescript
import { PipeTransform } from '@nestjs/common';

export class StringToUppercasePipe implements PipeTransform {
  transform(value: string, metadata: PipeTransformMetadata) {
    return value.toUpperCase();
  }
}
```

## 커스텀 파이프 사용법

사용자 지정 파이프를 만든 후에는 `@UsePipes` 데코레이터로 컨트롤러 또는 서비스 메서드를 장식하여 응용 프로그램에서 사용할 수 있습니다.

```typescript
import { Controller, Get, UsePipes } from '@nestjs/common';
import { StringToUppercasePipe } from './string-to-uppercase.pipe';

@Controller('/')
export class AppController {
  @Get('/')
  @UsePipes(StringToUppercasePipe)
  getHello(): string {
    return 'Hello, world!';
  }
}
```

위의 예에서 `@UsePipes` 데코레이터는 `StringToUppercasePipe`를 `getHello` 메서드에 적용하는 데 사용됩니다. 즉, 메서드에서 반환되는 모든 문자열은 대문자로 변환됩니다.

## 요약

이 게시물에서는 Nest.js에서 사용자 지정 파이프를 만드는 방법을 배웠습니다. 파이프는 데이터가 응용 프로그램을 통해 흐를 때 데이터를 변환하는 좋은 방법입니다.