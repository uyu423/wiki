---
title: Apache2 에서 https 사용을 위한 certbot SSL 인증서 초간단 설정
description: 
published: true
date: 2022-11-24T11:10:15.837Z
tags: apache, ssl, certbot
editor: markdown
dateCreated: 2022-11-24T11:10:15.837Z
---

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

## Prepare apache2 conf

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

## Run certbot

```bash
$ sudo certbot --apache

Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator apache, Installer apache

Which names would you like to activate HTTPS for?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: wiki.yowu.dev
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate numbers separated by commas and/or spaces, or leave input
blank to select all options shown (Enter 'c' to cancel):
```

- 이후에는 `http` -> `https` rewrite 라던지 기타 등등 선택 옵션이 나오는데 알잘딱으로 선택
- `/etc/apache2/sites-enables` 하위에 `*-le-ssl.conf` 가 심볼릭 링크로 생성되고, SSL 설정이 마무리됨
- 아마 자동으로 apache2 데몬이 재시작 됥텐데 안된 것 같다면 `sudo service apache2 reload`

## SSL 인증서 자동 갱신 등록

- 아래 커맨드를 한번 걸어두면 SSL 인증서 기한이 다가왔을 때 자동으로 갱신해준다.

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
