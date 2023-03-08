---
title: Kotlin 및 서버리스 기능: 확장 가능하고 비용 효율적인 애플리케이션 구축
description: 
published: true
date: 2023-02-05T11:55:45.487Z
tags: 
editor: markdown
dateCreated: 2023-02-05T11:55:43.868Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Kotlin and Serverless Functions: Building Scalable and Cost-Effective Applications***English** document is available*](/en/Knowledge-base/Kotlin/kotlin-and-serverless-functions-building-scalable-and-cost-effective-applications)
{.links-list}


# Kotlin 및 서버리스 기능: 확장 가능하고 비용 효율적인 애플리케이션 구축

Kotlin은 JVM(Java Virtual Machine)에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어이며 JavaScript 소스 코드로 컴파일할 수도 있습니다. Kotlin은 Apache 2.0 라이선스에 따른 오픈 소스 프로젝트입니다.

서버리스 기능은 서버를 프로비저닝하거나 관리할 필요 없이 클라우드에서 코드를 실행하는 방법입니다. 이벤트 기반 애플리케이션에 적합하며 수요에 따라 자동으로 확장 또는 축소할 수 있습니다.

Kotlin 및 서버리스 함수는 확장 가능하고 비용 효율적인 애플리케이션을 구축하는 데 완벽한 조화를 이룹니다. Kotlin은 이해하고 유지 관리하기 쉬운 코드를 쉽게 작성할 수 있도록 하는 간결하고 표현력이 풍부한 언어입니다. 또한 서버리스 기능은 이벤트 기반이므로 수요에 따라 자동으로 확장 또는 축소할 수 있어 매우 비용 효율적입니다.

이 기사에서는 Kotlin 및 서버리스 기능을 사용하여 간단하고 확장 가능하며 비용 효율적인 애플리케이션을 구축하는 방법을 보여줍니다. 또한 Kotlin 및 서버리스 기능을 최대한 활용하는 방법에 대한 몇 가지 팁도 제공합니다.

## 시작하기

시작하려면 Kotlin 컴파일러와 서버리스 프레임워크를 설치해야 합니다.

### Kotlin 컴파일러 설치

Kotlin 컴파일러는 [Kotlin 웹사이트](https://kotlinlang.org/)에서 다운로드할 수 있습니다. Kotlin 컴파일러를 다운로드했으면 다음 명령을 사용하여 설치할 수 있습니다.

```
$ tar xzf kotlinc-1.3.61.tgz
$ cd kotlinc-1.3.61
$ bin/kotlinc-jvm
```

### 서버리스 프레임워크 설치

서버리스 프레임워크는 [서버리스 웹사이트](https://serverless.com/)에서 다운로드할 수 있습니다. Serverless Framework를 다운로드했으면 다음 명령을 사용하여 설치할 수 있습니다.

```
$ npm install -g serverless
```

## Kotlin 함수 작성

이제 Kotlin 컴파일러와 서버리스 프레임워크가 설치되었으므로 첫 번째 Kotlin 함수를 작성할 준비가 되었습니다.

Kotlin 함수는 ```fun``` 키워드를 사용하여 선언됩니다. ```fun``` 키워드 다음에는 함수 이름, 매개변수 목록 및 함수 본문이 옵니다.

다음은 두 개의 숫자를 매개변수로 사용하고 해당 숫자의 합계를 반환하는 간단한 Kotlin 함수입니다.

```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```

```kotlin
fun sum(a: Int, b: Int) = a + b
```코틀린
재미있는 합계(a: Int, b: Int) = a + b
```kotlin
fun apply(f: (Int) -> Int, a: Int): Int {
    return f(a)
}
```코틀린
fun 적용(f: (Int) -> Int, a: Int): Int {
    f(a) 반환
}
```kotlin
fun square(x: Int): Int {
    return x * x
}

fun main() {
    val result = apply(::square, 4)
    println(result) // 16
}
```코틀린
펀 스퀘어(x: Int): Int {
    반환 x * x
}

재미있는 메인() {
    값 결과 = 적용(::제곱, 4)
    println(결과) // 16
}
```yaml
runtime: java8

provider:
  name: aws
  region: us-east-1

functions:
  sum:
    handler: com.example.SumFunction
    events:
      - http:
          path: /sum
          method: GET
```serverless.yml```이라는 파일을 만들어야 합니다. ```serverless.yml``` 파일은 서버리스 프레임워크를 구성하는 데 사용됩니다.

```
$ serverless deploy
```serverless.yml``` 파일입니다.

```
$ serverless invoke -f sum -d '{"a": 1, "b": 2}'
3
```

이 ```serverless.yml``` 파일에서 ```runtime``` 설정은 함수가 Kotlin으로 작성되었음을 지정하는 ```java8```으로 설정됩니다. ```provider``` 설정은 ```aws```로 설정되어 함수가 AWS Lambda에 배포되도록 지정합니다. ```functions``` 설정에는 ```/sum``` 경로에 대한 HTTP GET 요청을 통해 호출되도록 구성된 단일 함수 ```sum```이 포함되어 있습니다.

함수를 배포하려면 ```serverless deploy``` 명령을 사용할 수 있습니다. 이 명령은 함수를 AWS Lambda에 배포하고 함수를 호출하는 데 사용할 수 있는 Amazon API Gateway 엔드포인트를 생성합니다.

```
$ 서버리스 배포
```

## Kotlin 함수 호출

이제 Kotlin 함수를 배포했으므로 호출할 준비가 되었습니다.

Kotlin 함수를 호출하려면 ```serverless invoke``` 명령을 사용할 수 있습니다. 이 명령은 함수를 호출하고 결과를 콘솔에 인쇄합니다.

```
$ 서버리스 호출 -f 합계 -d '{"a": 1, "b": 2}'
삼
```

이 예에서 ```-f``` 옵션은 호출할 함수의 이름을 지정합니다. ```-d``` 옵션은 함수에 전달할 JSON 인코딩 데이터를 지정합니다. 이 예에서 데이터는 ```a``` 및 ```b```라는 두 개의 키와 정수 값을 포함하는 맵입니다.

## 결론

이 기사에서는 Kotlin 및 서버리스 기능을 사용하여 간단하고 확장 가능하며 비용 효율적인 애플리케이션을 구축하는 방법을 보여주었습니다. 또한 Kotlin 및 서버리스 기능을 최대한 활용하는 방법에 대한 몇 가지 팁도 제공했습니다.

Kotlin에 대해 자세히 알아보려면 [Kotlin 웹사이트](https://kotlinlang.org/)를 확인하는 것이 좋습니다.

서버리스 기능에 대해 자세히 알아보고 싶다면 [서버리스 웹사이트](https://serverless.com/)를 확인하는 것이 좋습니다.