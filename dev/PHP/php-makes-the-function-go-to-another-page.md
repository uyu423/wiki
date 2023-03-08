---
title: PHP에서 웹 브라우저를 다른 페이지로 이동시키기
description: 
published: true
date: 2023-02-17T18:00:09.445Z
tags: php
editor: markdown
dateCreated: 2022-12-24T16:29:12.043Z
---

- [Navigate web browser to another page in PHP***Korean** version of this document is available*](/en/dev/PHP/php-makes-the-function-go-to-another-page)
{.links-list}

## header() 함수 사용

- php의 `header()` 를 사용해서 웹 브라우져를 특정 페이지로 이동 시킬 수 있다.
- `header()` 는 클라이언트에 전송되는 HTTP Response Header 를 통해 동작한다.

```php
<?php
  // example.com으로 리디렉션
  header('Location: https://www.example.com');
  exit;
?>
```

- 페이지를 이동 시키기전에 지연 시간이 필요하다면 `refresh` 를 사용할 수 있다. 역시 HTTP Header 로 동작한다.

```php
<?php
  // 5초 후 example.com으로 리디렉션
  header('refresh: 5; url=https://www.example.com');
  exit;
?>
```

## \<script> 사용

- `headers()` 를 사용한 방식의 단점은 `<script>` 의 `alert()` 함수와 같이 동기식으로 동작하는 코드를 무시하게 된다.
- 예를 들어 아래와 같은 코드에서는 "Hello, World!" 라는 경고창 (Alert)이 표시되지 않고 바로 `example.com` 으로 이동한다.


```php
<?php
  // alert 이 표시되지 않고 바로 페이지 이동이 일어난다.
  echo '<script>alert("Hello, World!");</script>';
  header('Location: https://www.example.com');
?>
```

- 이런 케이스에서는 `header()` 사용하지 않고 javascript의 `window.location.href` 를 사용하는 것이 원하는 동작을 보장한다.

```php
<?php
  // "Hello, World!"라는 메시지와 함께 경고를 표시 후 example.com으로 이동
  echo '<script>
          alert("Hello, World!");
          window.location.href = "https://www.example.com";
        </script>';
?>
```

- 페이지 이동하기 전에 지연 시간이 필요하다면 `setTimeout` 과 조합하여 사용할 수 있다.


```php
<?php
  // "Hello, World!"라는 메시지와 함께 경고를 표시 후 5초 후에 example.com으로 이동
  echo '<script>
          alert("Hello, World!");
          setTimeout(function() {
            window.location.href = "https://www.example.com";
          }, 5000);
        </script>';
?>
```