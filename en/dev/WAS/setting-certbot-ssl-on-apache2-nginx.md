---
title: Setting up SSL certificates with certbot on Apache2 and Nginx
description: 
published: true
date: 2023-02-17T18:00:20.282Z
tags: apache, certbot, english, nginx, ssl
editor: markdown
dateCreated: 2022-12-24T19:52:40.683Z
---

- [Apache2와 nginx에서 certbot으로 SSL 인증서 설정하기***Korean** version of this document is available*](/ko/dev/WAS/setting-certbot-ssl-on-apache2-nginx)
{.links-list}

## Install certbot

- Based on Ubuntu

```bash
sudo snap install --classic certbot
# sudo apt install certbot
```

> If you installed with snap, the following process may be required
> ```bash
> sudo ln -s /snap/bin/certbot /usr/bin/certbot
> ```

## Prepare

### apache2 conf

- The http information to be registered for SSL must be included in the Apache configuration. `/etc/apache2/sites-enabled`
- usually create configuration in `sites-available` directory, create symbolic link to `sites-enables`


> - Below is a sample Apache http virtual host configuration used as proxy configuration
> - You must have apache2 proxy mods to use proxy.
> - `014-yowuwiki-proxy.conf`
> ```bash
> <VirtualHost *:80>
> ProxyPreserveHost On
> ProxyRequests off
> ProxyPreserveHost On
> AllowEncodedSlashes NoDecode
>
> ProxyPass / http://localhost:3000/nocanon
> ProxyPassReverse / http://localhost:3000/
> ProxyPassReverse / http://wiki.yowu.dev/
>
> ServerName wiki.yowu.dev
>
> ErrorLog ${APACHE_LOG_DIR}/yowuwiki/proxy_error.log
> CustomLog ${APACHE_LOG_DIR}/yowuwiki/proxy_access.log combined
> </VirtualHost>
> ```

### nginx conf

- Like apache, http information must be included in nginx configuration. `/etc/nginx/sites-enabled/`

> - Below is a sample nginx http virtual host configuration used as proxy configuration
> - `001-wiki.conf`
> ```bash
> server {
>listen 80;
> server_name wiki.d8.company;
>
>location/{
> root /var/www/html;
>
> proxy_pass http://127.0.0.1:3000;
> proxy_set_header Connection "";
> proxy_http_version 1.1;
> proxy_set_header Host $host;
> proxy_set_header X-Real-IP $remote_addr;
> proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
> }
>
> gzip on;
> gzip_comp_level 4;
> gzip_types text/plain text/css application/json application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript;
> }
> ```

## Run certbot

```bash
$ sudo certbot --apache # or --nginx

Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator apache, Installer apache

Which names would you like to activate HTTPS for?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: wiki.yowu.dev
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate numbers separated by commas and/or spaces, or leave input
blank to select all options shown (Enter 'c' to cancel):
```

- If this is the first run, you will receive an email and agree to the terms and conditions. Just press <kbd>Y</kbd> appropriately.
### For apache
   - `http` -> `https` rewrite or other options appear, select them clearly
   - `*-le-ssl.conf` is created as a symbolic link under `/etc/apache2/sites-enables`, and SSL configuration is completed.
   - Perhaps the apache2 daemon restarted automatically, but if it doesn't seem to work, `sudo service apache2 reload`
### For nginx
   - The existing conf settings are overwritten, and even redirects are set together.

> - In the case of nginx, if the following message appears, an additional module is required.
> - `The requested nginx plugin does not appear to be installed`
>
> ```bash
> sudo add-apt-repository ppa:certbot/certbot
> sudo apt install python-certbot-nginx -y # or python3-certbot-nginx
> ```
>

## SSL certificate auto-renewal test

- By default, certbot is registered with systemd and automatically renews SSL certificates when they are nearing expiration.
- You can test SSL auto-renewal with the command below.

```bash
$ sudo certbot renew --dry-run

Saving debug log to /var/log/letsencrypt/letsencrypt.log

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Processing /etc/letsencrypt/renewal/wiki.yowu.dev.conf
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Cert not due for renewal, but simulating renewal for dry run
Plugins selected: Authenticator apache, Installer apache
Renewing an existing certificate
Performing the following challenges:
http-01 challenge for dev-server.d8.company
Waiting for verification...
Cleaning up challenges

The following certificates were successfully renewed:
   /etc/letsencrypt/live/wiki.yowu.dev/fullchain.pem (success)
```

---

> https://certbot.eff.org/

![certbot-logo.png](/certbot-logo.png){.align-center}