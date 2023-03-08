---
title: nginx 및 Apache2로 웹 서버 설정
description: 
published: true
date: 2023-02-17T18:01:40.579Z
tags: 
editor: markdown
dateCreated: 2023-01-30T03:32:19.828Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Setting up a Web Server with nginx and Apache2***English** version of this document is available*](/en/Knowledge-base/Backend/setting-up-a-web-server-with-nginx-and-apache2)
{.links-list}


# nginx와 Apache2로 웹 서버 설정하기

이 게시물에서는 nginx와 Apache2를 사용하여 웹 서버를 설정하는 방법을 살펴보겠습니다. 이것은 매우 표준적인 구성이며 대부분의 서버 요구에 적합합니다.

먼저 nginx를 설치해야 합니다. 우리는 이것을 apt로 할 수 있습니다:

```
sudo apt install nginx
```

nginx가 설치되면 구성해야 합니다. `/etc/nginx/nginx.conf` 파일을 편집하여 이를 수행할 수 있습니다. 여기서 몇 가지를 설정해야 합니다.

```
http {
  # We'll need to set up a few things here

  server {
    # This is where we'll put our server config

    location / {
      # This is where we'll put our location config
    }
  }
}
```

각 섹션이 수행하는 작업을 살펴보겠습니다.

`http` 섹션은 글로벌 구성을 넣을 곳입니다. 이것은 우리의 모든 서버 요청에 적용되는 것입니다.

`server` 섹션은 서버별 구성을 넣을 곳입니다. 이것은 우리 서버의 도메인 이름과 그것이 제공해야 하는 파일과 같은 것입니다.

`location` 섹션은 위치별 구성을 넣을 곳입니다. 이것은 특정 URL에 어떤 파일을 제공할지와 같은 것입니다.

이제 nginx 구성이 설정되었으므로 Apache2로 이동하겠습니다.

nginx와 마찬가지로 apt를 사용하여 Apache2를 설치할 수 있습니다.

```
sudo apt install apache2
```

Apache2가 설치되면 구성해야 합니다. `/etc/apache2/apache2.conf` 파일을 편집하여 이를 수행할 수 있습니다. 여기서 몇 가지를 설정해야 합니다.

```
<VirtualHost *:80>
  # We'll need to set up a few things here

  <Directory /var/www/html>
    # This is where we'll put our Directory config
  </Directory>
</VirtualHost>
```

각 섹션이 수행하는 작업을 살펴보겠습니다.

`<VirtualHost>` 섹션은 가상 호스트 구성을 넣을 위치입니다. 이것은 우리 서버의 도메인 이름과 그것이 제공해야 하는 파일과 같은 것입니다.

`<Directory>` 섹션은 디렉토리별 구성을 넣을 곳입니다. 이것은 특정 URL에 어떤 파일을 제공할지와 같은 것입니다.

이제 Apache2 구성이 설정되었으므로 웹 서버를 시작할 수 있습니다. 우리는 `service` 명령으로 이것을 할 수 있습니다:

```
sudo service nginx start
sudo service apache2 start
```

이제 http://localhost:80에서 웹 서버에 액세스할 수 있습니다.