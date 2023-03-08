---
title: 020: Nest.js에서 데이터 변환을 위한 파이프 사용
description: 
published: true
date: 2023-02-09T15:17:23.549Z
tags: 
editor: markdown
dateCreated: 2023-02-09T15:17:21.910Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [020: Using pipes for data transformation in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/020-using-pipes-for-data-transformation-in-nest-js)
{.links-list}


# Nest.js에서 데이터 변환을 위해 파이프 사용

Nest.js에서 파이프는 데이터 변환에 사용됩니다. 파이프는 데이터를 입력으로 받고 변환된 데이터를 출력으로 반환합니다.

파이프는 다음과 같은 다양한 작업에 사용할 수 있습니다.

- 검증
- 포맷팅
- 변신

파이프는 `@ Pipe` 데코레이터를 사용하여 만들 수 있습니다. `@ Pipe` 데코레이터는 파이프 이름을 인수로 받습니다.

```javascript
@ Pipe({
  name: 'myPipe'
})
```

파이프는 `.pipe()` 메서드를 사용하여 함께 연결할 수 있습니다. `.pipe()` 메서드는 파이프 이름을 인수로 받습니다.

```javascript
.pipe(myPipe)
```

파이프는 Nest.js 컨트롤러 및 서비스에서 사용할 수 있습니다. 컨트롤러에서 파이프를 사용하려면 `@ UsePipes` 데코레이터를 사용할 수 있습니다. `@ UsePipes` 데코레이터는 파이프 이름을 인수로 받습니다.

```javascript
@ UsePipes(myPipe)
```

서비스에서 파이프를 사용하려면 `.usePipe()` 메서드를 사용할 수 있습니다. `.usePipe()` 메서드는 파이프 이름을 인수로 받습니다.

```javascript
.usePipe(myPipe)
```

## 파이프 만들기

파이프를 생성하려면 `@ Pipe` 데코레이터를 사용할 수 있습니다. `@ Pipe` 데코레이터는 파이프 이름을 인수로 받습니다.

```javascript
@ Pipe({
  name: 'myPipe'
})
```

파이프에는 `transform()` 메서드가 있어야 합니다. `transform()` 메서드는 변환할 데이터를 인수로 받아 변환된 데이터를 반환합니다.

```javascript
transform(data: any) {
  return data;
}
```

## 체인 파이프

파이프는 `.pipe()` 메서드를 사용하여 함께 연결할 수 있습니다. `.pipe()` 메서드는 파이프 이름을 인수로 받습니다.

```javascript
.pipe(myPipe)
```

## 컨트롤러에서 파이프 사용하기

파이프는 Nest.js 컨트롤러 및 서비스에서 사용할 수 있습니다. 컨트롤러에서 파이프를 사용하려면 `@ UsePipes` 데코레이터를 사용할 수 있습니다. `@ UsePipes` 데코레이터는 파이프 이름을 인수로 받습니다.

```javascript
@ UsePipes(myPipe)
```

## 서비스에서 파이프 사용

서비스에서 파이프를 사용하려면 `.usePipe()` 메서드를 사용할 수 있습니다. `.usePipe()` 메서드는 파이프 이름을 인수로 받습니다.

```javascript
.usePipe(myPipe)
```

## 예

이 예에서는 문자열을 받아 모두 대문자로 된 문자열을 반환하는 파이프가 생성됩니다.

```javascript
@ Pipe({
  name: 'uppercasePipe'
})
export class UppercasePipe implements PipeTransform {
  transform(data: string) {
    return data.toUpperCase();
  }
}
```

이 파이프는 다음과 같이 컨트롤러에서 사용할 수 있습니다.

```javascript
@ Controller('/')
@ UsePipes(UppercasePipe)
export class MyController {
  @ Get('/')
  getData(@ Req() request: Request) {
    return {
      data: 'Hello, world!'
    };
  }
}
```

## 추가 정보

- [Nest.js 파이프](https://docs.nestjs.com/pipes)
- [Nest.js UsePipes](https://docs.nestjs.com/use-pipes)

## 경고

- 파이프는 연결된 순서대로 실행됩니다.

## 위험

- 파이프에서 오류가 발생하면 파이프 체인 실행이 중지됩니다.