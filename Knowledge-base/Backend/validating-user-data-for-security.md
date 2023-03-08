---
title: 보안을 위해 사용자 데이터 검증
description: 
published: true
date: 2023-02-10T04:17:36.510Z
tags: 
editor: markdown
dateCreated: 2023-02-10T04:17:34.944Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Validating User Data for Security***English** document is available*](/en/Knowledge-base/Backend/validating-user-data-for-security)
{.links-list}


# 보안을 위해 사용자 데이터 유효성 검사

애플리케이션 개발자는 사용자가 입력한 데이터가 유효하고 안전한지 확인할 책임이 있습니다. 사용자가 유효하지 않은 데이터를 입력할 수 있는 방법이 많고 고려해야 할 보안 위험이 많기 때문에 이는 어려운 작업이 될 수 있습니다. 이 기사에서는 사용자 데이터의 유효성을 검사하는 몇 가지 모범 사례에 대해 논의하고 PHP의 몇 가지 코드 예제를 제공합니다.

## 사용자 입력 삭제

사용자 입력을 확인하는 첫 번째 단계는 데이터가 깨끗하거나 "삭제"되었는지 확인하는 것입니다. 이는 애플리케이션에 악성 코드를 삽입하는 데 사용할 수 있는 특수 문자를 제거하는 것을 의미합니다. 예를 들어 사용자가 자신의 이름을 입력할 것으로 예상하는 경우 숫자, 구두점 또는 공백과 같이 문자가 아닌 문자를 제거할 수 있습니다.

사용자 입력을 삭제하는 한 가지 방법은 PHP 함수 ```filter_var()```를 사용하는 것입니다. 이 함수는 필터링할 값과 적용할 필터의 두 가지 인수를 사용합니다. 예를 들어 이름 필드를 필터링하려면 태그나 특수 문자를 제거하는 ```FILTER_SANITIZE_STRING``` 필터를 사용할 수 있습니다.

```php
$name = "John Smith";

$sanitized_name = filter_var($name, FILTER_SANITIZE_STRING);

echo $sanitized_name; // John Smith
```

```php
$name = "John Smith";

$validated_name = filter_var($name, FILTER_VALIDATE_REGEXP, array("options"=>array("regexp"=>"/^[a-zA-Z]+$/")));

if($validated_name === false) {
  echo "Invalid name";
} else {
  echo "Valid name";
}
```FILTER_VALIDATE_*``` 필터와 함께 PHP 함수 ```filter_var()```를 사용하는 것입니다. 이러한 필터는 지정된 형식에 따라 데이터의 유효성을 검사합니다. 예를 들어 이름 필드의 유효성을 검사하려면 알파벳 문자만 허용하는 정규식과 함께 ```FILTER_VALIDATE_REGEXP``` 필터를 사용할 수 있습니다.

```php
$email = "john.smith@example.com";

$sanitized_email = filter_var($email, FILTER_SANITIZE_EMAIL);
$validated_email = filter_var($sanitized_email, FILTER_VALIDATE_EMAIL);

if($validated_email === false) {
  echo "Invalid email";
} else {
  echo "Valid email";
}
```

데이터가 유효하면 ```filter_var()```가 데이터를 반환합니다. 데이터가 잘못된 경우 ```filter_var()```는 ```false```를 반환합니다.

## 보안 고려 사항

사용자 입력의 유효성을 검사할 때 보안 위험을 고려하는 것이 중요합니다. 예를 들어 이메일 주소가 필요한 경우 데이터가 유효한 이메일 형식인지 확인해야 합니다. 그러나 이메일 주소에 악성 코드가 포함되어 있지 않은지 확인해야 합니다.

보안 위험을 고려하면서 사용자 입력의 유효성을 검사하는 한 가지 방법은 ```FILTER_SANITIZE_EMAIL``` 및 ```FILTER_VALIDATE_EMAIL`` 필터와 함께 PHP 함수 ```filter_var()```를 사용하는 것입니다. ```FILTER_SANITIZE_EMAIL``` 필터는 데이터에서 유효하지 않은 문자를 제거하고 ```FILTER_VALIDATE_EMAIL``` 필터는 이메일 형식에 따라 데이터의 유효성을 검사합니다.

```php
$email = "john.smith@example.com";

$sanitized_email = filter_var($email, FILTER_SANITIZE_EMAIL);
$validated_email = filter_var($sanitized_email, FILTER_VALIDATE_EMAIL);

if($validated_email === 거짓) {
  echo "잘못된 이메일";
} 또 다른 {
  echo "유효한 이메일";
}
```

## 결론

사용자 입력 유효성 검사는 애플리케이션의 보안을 보장하는 데 중요한 부분입니다. 사용자 데이터를 삭제하고 유효성을 검사하면 악성 코드 삽입 및 기타 보안 위험으로부터 애플리케이션을 보호할 수 있습니다.