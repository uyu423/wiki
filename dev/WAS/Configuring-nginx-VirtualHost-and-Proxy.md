---
title: Nginx에서 VirtualHost/Proxy 설정하기
description: 
published: true
date: 2023-02-17T17:59:37.015Z
tags: nginx, virtualhost, proxy
editor: markdown
dateCreated: 2022-11-24T08:20:30.225Z
---

![nginx-logo.png](/nginx-logo.png){.align-center}

- 아파치에서는 한번씩 했지만 Nginx는 방법을 몰랐다. 하지만 아파치와 비슷하더라.
- 우분투 기준

## 뭐가 문제임?
- 나는 `example.com`이라는 도메인을 어느 nginx에 달아서 사용하고 있음. 하지만 Nginx 내에서 도메인 이름에 따른 프록시 분기를 하고 싶음.

## Nginx Site Configure 파일 수정
- `sites-available/default` 파일 수정
```bash
sudo vi /etc/nginx/sites-available/default
```
- 설정 구문 추가
```bash
server {
    listen 80;
    # The host name to respond to
    server_name virtualhost.example.com;

    location / {
        proxy_pass http://localhost:9000;
        proxy_set_header   Connection ""; # optional
        proxy_http_version 1.1; # optional
        proxy_set_header        Host            	$host; # optional
        proxy_set_header        X-Real-IP      		$remote_addr; #optional
        proxy_set_header        X-Forwarded-For		$proxy_add_x_forwarded_for; # optional
    }
}
```
- 이제 `virtualhost.example.com`으로 `example.com:9000`에 접속할 수 있다!

> - 설정이 더 추가 된다면 `/etc/nginx/sites-*/` 디렉토리 내에서 별도 conf 파일로 관리하는 것이 수월하다.
> - `/etc/nginx/sites-available/wiki.conf` 를 생성했다면, 아래와 같이 심볼릭 링크를 걸어서 관리할 수 있다.
> ```bash
> sudo ln -s /etc/nginx/sites-available/wiki.conf /etc/nginx/sites-enabled/
> ```
> - 별도의 sites enabled 시키는 명령어가 있다고는 들었는데, 귀찮아서 잘 안쓴다.

> nginx virtual host + ssl 로 https 를 구현했다면 `location /` 블럭 하위에 아래 구문을 추가한다.
> ```bash
> proxy_set_header        X-Forwarded-Proto	https;
> ```
> 일부 환경에서 https -> http reverse proxy 로 인한 다양한 문제가 해결 될 수도 있다. (wp-admin 이라던지..)
 
## 기타 사항
- 외부 포트 최소한으로 열어둘 수 있다. vHost를 사용하지 않았다면 9000 포트도 외부로 열어줘야 했던 상황. 최소한의 포트만을 열어두는 것이 보안적 측면에서 좋다.
- 도메인 레코드 설정에서 레코드 이름을 `*.example.com`로 꼭 설정해주자.
- 위 예제의 경우 당연히 9000번 포트는 `forever`와 같은 친구로 열려있는 상황이다.
