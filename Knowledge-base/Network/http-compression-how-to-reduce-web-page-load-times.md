---
title: HTTP 압축: 웹 페이지 로드 시간을 줄이는 방법
description: 
published: true
date: 2023-03-03T23:32:21.250Z
tags: 
editor: markdown
dateCreated: 2023-03-03T23:32:21.250Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [HTTP Compression: How to Reduce Web Page Load Times***English** document is available*](/en/Knowledge-base/Network/http-compression-how-to-reduce-web-page-load-times)
{.links-list}
HTTP 압축: 웹 페이지 로드 시간을 줄이는 방법

인터넷 사용이 계속 증가함에 따라 웹 페이지 로드 시간은 사용자 경험에서 중요한 요소가 되었습니다. 느리게 로드되는 페이지는 사용자가 로드하는 데 너무 오래 걸리는 페이지를 포기할 수 있으므로 열악한 사용자 경험과 수익 손실로 이어질 수 있습니다. HTTP 압축은 웹 페이지 로드 시간을 줄여 사용자 경험을 향상시키는 데 사용할 수 있는 기술입니다. 이 기사에서는 HTTP 압축이 무엇인지, 어떻게 작동하는지, 웹 개발에서 어떻게 구현할 수 있는지 살펴보겠습니다.

## HTTP 압축이란 무엇입니까?

HTTP 압축은 인터넷을 통해 전송되는 데이터의 크기를 줄이는 데 사용되는 기술입니다. 네트워크를 통해 데이터를 보내기 전에 데이터를 압축하면 웹 페이지를 로드하는 데 걸리는 시간을 줄일 수 있습니다. HTTP 압축은 웹 페이지에서 중복 데이터를 제거하여 페이지 크기를 줄일 수 있다는 생각을 기반으로 합니다. 이렇게 페이지 크기가 줄어들면 로딩 시간이 빨라지고 사용자 경험이 향상됩니다.

## HTTP 압축은 어떻게 작동합니까?

HTTP 압축은 유선으로 전송되기 전에 데이터를 압축하는 방식으로 작동합니다. HTTP 압축에 사용되는 압축 알고리즘에는 gzip과 deflate의 두 가지 유형이 있습니다. Gzip은 가장 널리 사용되는 압축 알고리즘이며 대부분의 웹 브라우저에서 지원됩니다. Deflate는 gzip보다 압축률이 더 좋은 최신 알고리즘이지만 널리 지원되지는 않습니다.

브라우저가 웹 페이지를 요청하면 서버는 브라우저가 HTTP 압축을 지원하는지 확인합니다. 브라우저가 HTTP 압축을 지원하는 경우 서버는 gzip 또는 deflate를 사용하여 데이터를 압축하고 브라우저로 보냅니다. 그런 다음 브라우저는 데이터의 압축을 풀고 웹 페이지를 사용자에게 표시합니다.

## HTTP 압축 구현 방법

HTTP 압축 구현은 비교적 간단합니다. 대부분의 웹 서버는 기본적으로 HTTP 압축을 지원하며 이를 활성화하는 것은 서버를 올바르게 구성하는 문제입니다. 이 섹션에서는 Apache 및 Nginx 웹 서버에서 HTTP 압축을 활성화하는 방법을 살펴봅니다.

### Apache에서 HTTP 압축 활성화

Apache 웹 서버에서 HTTP 압축을 활성화하려면 서버의 구성 파일을 수정해야 합니다. 다음 단계를 사용하여 이를 수행할 수 있습니다.

1. 텍스트 편집기에서 Apache 구성 파일을 엽니다. 구성 파일의 위치는 사용되는 운영 체제 및 설치 방법에 따라 다릅니다. 예를 들어 Ubuntu에서 구성 파일은 `/etc/apache2/apache2.conf`에 있습니다.

2. 구성 파일에서 `mod_deflate` 모듈을 찾습니다. 이 모듈은 Apache 서버에서 HTTP 압축을 담당합니다.

3. HTTP 압축을 활성화하려면 다음 줄의 주석을 제거하십시오.

   ```
   # 필터 삽입
   SetOutputFilter DEFLATE
   
   # Netscape 4.x에 몇 가지 문제가 있습니다...
   BrowserMatch ^Mozilla/4 gzip-only-text/html
   
   # Netscape 4.06-4.08에는 몇 가지 더 많은 문제가 있습니다.
   BrowserMatch ^Mozilla/4\.0[678] no-gzip
   
   # MSIE는 Netscape로 가장하지만 괜찮습니다.
   BrowserMatch \bMSIE !no-gzip !gzip-only-text/html
   
   # 이미지를 압축하지 마세요
   SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
   
   # 프록시가 잘못된 콘텐츠를 전달하지 않도록 합니다.
   헤더 추가 Vary User-Agent env=!dont-vary
   ```

4. 구성 파일을 저장하고 Apache 웹 서버를 다시 시작합니다.

### Nginx에서 HTTP 압축 활성화

Nginx 웹 서버에서 HTTP 압축을 활성화하려면 서버의 구성 파일을 수정해야 합니다. 다음 단계를 사용하여 이를 수행할 수 있습니다.

1. 텍스트 편집기에서 Nginx 구성 파일을 엽니다. 구성 파일의 위치는 사용되는 운영 체제 및 설치 방법에 따라 다릅니다. 예를 들어 Ubuntu에서 구성 파일은 `/etc/nginx/nginx.conf`에 있습니다.

2. 구성 파일에서 `gzip` 모듈을 찾습니다. 이 모듈은 Nginx 서버에서 HTTP 압축을 담당합니다.

3. HTTP 압축을 활성화하려면 다음 줄의 주석을 제거하십시오.

   ```
   gzip 켜기;
   gzip_types 텍스트/일반 텍스트/css 애플리케이션/json 애플리케이션/자바스크립트 텍스트/xml 애플리케이션/xml 애플리케이션/xml+rss 텍스트/자바스크립트;
   ```

4. 구성 파일을 저장하고 Nginx 웹 서버를 다시 시작합니다.

## 결론

HTTP 압축은 웹 페이지 로드 시간을 줄여 사용자 경험을 향상시키는 데 사용할 수 있는 기술입니다. 네트워크를 통해 데이터를 보내기 전에 데이터를 압축하면 웹 페이지를 로드하는 데 걸리는 시간을 줄일 수 있습니다. 이 기사에서는 HTTP 압축이 무엇인지, 어떻게 작동하는지, 웹 개발에서 어떻게 구현할 수 있는지 살펴보았습니다. 또한 Apache 및 Nginx 웹 서버에서 HTTP 압축을 활성화하기 위한 실용적인 정보와 코드 예제를 제공했습니다.

## 외부 리소스

- [Apache에서 HTTP 압축](https://httpd.apache.org/docs/2.4/mod/mod_deflate.html)
- [Nginx의 HTTP 압축](https://www.nginx.com/blog/nginx-1-7-10-http-2-huge-pages-and-more/)
- [HTTP 압축 모범 사례](https://www.keycdn.com/blog/http-compression-best-practices/)