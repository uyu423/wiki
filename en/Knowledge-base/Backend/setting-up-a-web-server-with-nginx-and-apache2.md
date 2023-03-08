---
title: Setting up a Web Server with nginx and Apache2
description: 
published: true
date: 2023-02-17T18:01:39.145Z
tags: 
editor: markdown
dateCreated: 2023-01-30T03:32:19.828Z
---

- [nginx 및 Apache2로 웹 서버 설정***Korean** version of this document is available*](/ko/Knowledge-base/Backend/setting-up-a-web-server-with-nginx-and-apache2)
{.links-list}


# Setting up a Web Server with nginx and Apache2

In this post, we'll go over how to set up a web server using nginx and Apache2. This is a pretty standard configuration, and it'll work for most server needs.

First, we'll need to install nginx. We can do this with apt:

```
sudo apt install nginx
```

Once nginx is installed, we'll need to configure it. We can do this by editing the `/etc/nginx/nginx.conf` file. We'll need to set up a few things here:

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

Let's go over what each of these sections does.

The `http` section is where we'll put our global configuration. This is stuff that'll apply to all of our server requests.

The `server` section is where we'll put our server-specific configuration. This is stuff like our server's domain name, and what files it should serve.

The `location` section is where we'll put our location-specific configuration. This is stuff like what files to serve for a specific URL.

Now that we have our nginx config set up, let's move on to Apache2.

Like nginx, we can install Apache2 with apt:

```
sudo apt install apache2
```

Once Apache2 is installed, we'll need to configure it. We can do this by editing the `/etc/apache2/apache2.conf` file. We'll need to set up a few things here:

```
<VirtualHost *:80>
  # We'll need to set up a few things here

  <Directory /var/www/html>
    # This is where we'll put our Directory config
  </Directory>
</VirtualHost>
```

Let's go over what each of these sections does.

The `<VirtualHost>` section is where we'll put our virtual host configuration. This is stuff like our server's domain name, and what files it should serve.

The `<Directory>` section is where we'll put our directory-specific configuration. This is stuff like what files to serve for a specific URL.

Now that we have our Apache2 config set up, we can start our web server. We can do this with the `service` command:

```
sudo service nginx start
sudo service apache2 start
```

You should now be able to access your web server at http://localhost:80.