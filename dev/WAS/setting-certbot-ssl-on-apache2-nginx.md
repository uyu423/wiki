---
title: Apache2와 nginx에서 certbot으로 SSL 인증서 설정하기
description: Apache2 / nginx 에서 certbot 으로 https 초간단 설정
published: true
date: 2023-02-17T17:59:44.955Z
tags: apache, ssl, certbot, nginx
editor: markdown
dateCreated: 2022-11-24T11:10:15.837Z
---

- [Setting up SSL certificates with certbot on Apache2 and nginx***English** version of this document is available*](/en/dev/WAS/setting-certbot-ssl-on-apache2-nginx)
{.links-list}


## Install certbot

- Ubuntu 기준

```bash
sudo snap install --classic certbot
# sudo apt install certbot
```

> snap 으로 설치 했다면 다음 과정이 필요할 수 있음
> ```bash
> sudo ln -s /snap/bin/certbot /usr/bin/certbot
> ```

## Prepare

### apache2 conf

- SSL 등록하려는 http 정보가 아파치 설정에 포함되어 있어야한다. `/etc/apache2/sites-enabled`
- 일반적으로 `sites-available` 디렉토리에 설정을 만들고, `sites-enables` 로 심볼릭 링크를 생성함


> - 아래는 proxy 설정으로 사용하는 아파치 http virtual host 설정 샘플
>   - proxy 를 사용하려면 apache2 proxy mods 가 있어야한다.
> - `014-yowuwiki-proxy.conf`
> ```bash
> <VirtualHost *:80>
> 	ProxyPreserveHost On
> 	ProxyRequests off
> 	ProxyPreserveHost On
> 	AllowEncodedSlashes NoDecode
> 
> 	ProxyPass / http://localhost:3000/ nocanon
> 	ProxyPassReverse / http://localhost:3000/
> 	ProxyPassReverse / http://wiki.yowu.dev/
> 
> 	ServerName wiki.yowu.dev
> 
> 	ErrorLog ${APACHE_LOG_DIR}/yowuwiki/proxy_error.log
> 	CustomLog ${APACHE_LOG_DIR}/yowuwiki/proxy_access.log combined
> </VirtualHost>
> ```

### nginx conf

- apache와 마찬가지로 http 정보가 nginx 설정에 포함되어 있어야 한다. `/etc/nginx/sites-enabled/`

> - 아래는 proxy 설정으로 사용하는 nginx http virtual host 설정 샘플
> - `001-wiki.conf`
> ```bash
> server {
>     listen 80;
>     server_name wiki.d8.company;
> 
>     location / {
> 			root /var/www/html;
> 
> 			proxy_pass  http://127.0.0.1:3000;
> 			proxy_set_header   Connection "";
> 			proxy_http_version 1.1;
> 			proxy_set_header        Host            $host;
> 			proxy_set_header        X-Real-IP       $remote_addr;
> 			proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
>     }
> 
>     gzip on;
>     gzip_comp_level 4;
>     gzip_types text/plain text/css application/json application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript;
> }
> ```

## Run certbot

```bash
$ sudo certbot --apache # or --nginx

Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator apache, Installer apache

Which names would you like to activate HTTPS for?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: wiki.yowu.dev
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate numbers separated by commas and/or spaces, or leave input
blank to select all options shown (Enter 'c' to cancel):
```

- 최초 실행이라면 이메일을 입력받고, 이것저것 약관 동의가 진행된다. 적당히 <kbd>Y</kbd> 를 눌러주면 된다.
###  apache 의 경우
  - `http` -> `https` rewrite 라던지 기타 등등 선택 옵션이 나오는데 알잘딱으로 선택
  - `/etc/apache2/sites-enables` 하위에 `*-le-ssl.conf` 가 심볼릭 링크로 생성되고, SSL 설정이 마무리됨
  - 아마 자동으로 apache2 데몬이 재시작 됥텐데 안된 것 같다면 `sudo service apache2 reload`
### nginx 의 경우
  - 기존 conf 설정을 뒤집어쓰고, redirect 까지 함께 설정된다.

> - nginx 의 경우 아래와 같은 메시지가 뜬다면 추가 모듈이 필요하다.
>   - `The requested nginx plugin does not appear to be installed`
> 
> ```bash
> sudo add-apt-repository ppa:certbot/certbot
> sudo apt install python-certbot-nginx -y # or python3-certbot-nginx
> ```
>

## SSL 인증서 자동 갱신 테스트

- 기본적으로 certbot은 systemd 에 등록이 되어서 만료 기간이 다가올 경우 SSL 인증서를 자동으로 갱신해준다.
- 아래 커맨드로 SSL 자동 갱신을 테스트해볼 수 있다.

```bash
$ sudo certbot renew --dry-run

Saving debug log to /var/log/letsencrypt/letsencrypt.log

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/wiki.yowu.dev.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Cert not due for renewal, but simulating renewal for dry run
Plugins selected: Authenticator apache, Installer apache
Renewing an existing certificate
Performing the following challenges:
http-01 challenge for dev-server.d8.company
Waiting for verification...
Cleaning up challenges

The following certs were successfully renewed:
  /etc/letsencrypt/live/wiki.yowu.dev/fullchain.pem (success)
```

---

> https://certbot.eff.org/

![certbot-logo.png](/certbot-logo.png){.align-center}