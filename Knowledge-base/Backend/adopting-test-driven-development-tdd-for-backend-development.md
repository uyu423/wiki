---
title: 백엔드 개발을 위한 테스트 주도 개발(TDD) 채택
description: 
published: true
date: 2023-02-16T11:17:29.259Z
tags: 
editor: markdown
dateCreated: 2023-02-16T11:17:27.325Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Adopting Test Driven Development (TDD) for Backend Development***English** document is available*](/en/Knowledge-base/Backend/adopting-test-driven-development-tdd-for-backend-development)
{.links-list}


# 백엔드 개발을 위한 테스트 주도 개발(TDD) 채택

## 테스트 주도 개발이란?

테스트 주도 개발(TDD)은 매우 짧은 개발 주기의 반복에 의존하는 소프트웨어 개발 프로세스입니다. 먼저 개발자는 원하는 개선 또는 새로운 기능을 정의하는 (처음에는 실패하는) 자동화된 테스트 사례를 작성한 다음 최소량을 생성합니다. 해당 테스트를 통과하고 최종적으로 새 코드를 수용 가능한 표준으로 리팩토링합니다.

TDD는 코딩이 시작되기 전에 요구 사항이 수집되는 기존의 폭포수 개발 모델과 반대됩니다.

TDD를 사용하여 코드 품질을 개선하고 더 강력하게 만들 수 있습니다. 또한 재작업을 방지하여 개발 프로세스를 보다 효율적으로 만들 수 있습니다.

## TDD를 사용하는 이유

백엔드 개발에 TDD를 채택하는 데에는 여러 가지 이유가 있습니다. 가장 중요한 이점은 다음과 같습니다.

### 1. TDD는 더 나은 코드 작성을 도와줍니다.

TDD는 추가하거나 변경하려는 기능과 사용 방법에 대해 생각하도록 합니다. 이를 통해 더 이해하기 쉽고 유지 관리 및 테스트 가능한 코드를 작성할 수 있습니다.

### 2. TDD는 버그를 조기에 발견하도록 도와줍니다.

테스트가 실패하면 코드에 버그가 있음을 의미합니다. 코드를 작성하기 전에 테스트를 작성하면 버그를 조기에 발견하고 나중에 수정하지 않아도 됩니다.

### 3. TDD는 코드 작성을 줄이는 데 도움이 됩니다.

TDD는 불필요한 코드 작성을 피하는 데 도움이 됩니다. 테스트에서 다루지 않는 코드를 작성하고 있는 경우 해당 코드가 필요하지 않을 수 있습니다.

### 4. TDD는 마감일을 맞추는 데 도움이 됩니다.

TDD는 필요하지 않은 코드를 작성하지 않도록 도와줌으로써 기한을 맞추는 데 도움이 될 수 있습니다. 필요한 기능에 집중함으로써 필요하지 않은 코드 작성을 피하고 시간을 절약할 수 있습니다.

### 5. TDD는 회귀를 피하도록 도와줍니다.

회귀는 기존 기능을 손상시키는 변경 사항입니다. 코드를 작성하기 전에 테스트를 작성하면 회귀를 방지할 수 있습니다.

## TDD 사용 방법

TDD는 세 단계로 구성된 프로세스입니다.

### 1. 테스트 작성

첫 번째 단계는 추가하거나 변경하려는 기능을 정의하는 테스트를 작성하는 것입니다. 테스트는 코드가 실행될 때 실패하는 방식으로 작성되어야 합니다.

### 2. 코드 작성

두 번째 단계는 테스트를 통과할 코드를 작성하는 것입니다. 코드는 이해하고 유지하기 쉬운 방식으로 작성되어야 합니다.

### 3. 코드 리팩터링

세 번째 단계는 코드를 리팩토링하는 것입니다. 이는 코드의 품질을 개선하고 유지 관리하기 쉽게 하기 위해 수행됩니다.

## 예

섭씨를 화씨로 변환하는 백엔드에 새 기능을 추가하고 싶다고 가정해 보겠습니다. 새 함수에 대한 테스트를 작성하는 것으로 시작하겠습니다.

```
def test_celsius_to_fahrenheit(self):
    celsius = 100
    fahrenheit = 212
    self.assertEqual(celsius_to_fahrenheit(celsius), fahrenheit)
```

이 테스트는 새 기능의 기능을 정의합니다. 그런 다음 테스트를 통과하도록 코드를 작성합니다.

```
def celsius_to_fahrenheit(celsius):
    fahrenheit = celsius * 9 / 5 + 32
    return fahrenheit
```

마지막으로 코드를 리팩토링하여 품질을 개선합니다.

```
def celsius_to_fahrenheit(celsius):
    """Converts Celsius to Fahrenheit."""
    fahrenheit = celsius * 9 / 5 + 32
    return fahrenheit
```

## 결론

TDD는 더 나은 코드를 작성하고, 버그를 조기에 발견하고, 회귀를 방지하는 데 도움이 되는 소프트웨어 개발 프로세스입니다. 테스트 작성, 코드 작성, 코드 리팩터링의 세 단계로 구성된 프로세스입니다.