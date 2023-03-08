---
title: Linux Web Server and Database Administration
description: 
published: true
date: 2023-02-12T11:33:46.179Z
tags: 
editor: markdown
dateCreated: 2023-02-12T11:33:39.249Z
---

- [Administración de servidor web y base de datos Linux***Spanish** document is available*](/es/Knowledge-base/Linux/linux-web-server-and-database-administration)
{.links-list}
- [Linux Web 服务器和数据库管理***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-web-server-and-database-administration)
{.links-list}
- [Linux 웹 서버 및 데이터베이스 관리***Korean** document is available*](/ko/Knowledge-base/Linux/linux-web-server-and-database-administration)
{.links-list}


# Linux Web Server and Database Administration

In this article, we will cover the basics of administering a Linux web server and database. We will start with an overview of the most common tasks and then dive into each one in more detail.

## Overview

The most common tasks when administering a Linux web server are:

- Configuring the web server software
- Setting up domain names and DNS
- Managing user accounts
- Securing the server
- Backup and disaster recovery
- Monitoring the server

We will cover each of these topics in more detail below.

## Configuring the web server software

The first task when setting up a new web server is to install and configure the web server software. The most popular web server software for Linux is Apache HTTP Server. Other popular web servers include nginx and lighttpd.

The web server software is responsible for handling requests from clients (browsers) and returning the appropriate response (usually a web page). It also provides other features such as CGI support, virtual hosting, and password protection.

The configuration of the web server software is usually done through a text file called ```httpd.conf```. This file is typically located in the ```/etc/apache2/``` directory on Debian and Ubuntu systems, and in the ```/etc/httpd/conf/``` directory on Red Hat and CentOS systems.

The ```httpd.conf``` file contains many different directives that can be used to configure the server. Some of the most common directives are:

- ```ServerRoot```: This directive specifies the directory where the server's configuration files are located.
- ```Listen```: This directive specifies the port number that the server should listen on. The default port for HTTP is 80.
- ```DocumentRoot```: This directive specifies the directory where the server's web files are located. This is usually the ```/var/www/html/``` directory.
- ```<Directory>```: This directive is used to specify the configuration for a specific directory.
- ```<VirtualHost>```: This directive is used to configure virtual hosts. Virtual hosts allow multiple websites to be hosted on the same server.

For more information on the Apache HTTP Server, please see the following resources:

- The Apache HTTP Server Documentation: https://httpd.apache.org/docs/
- The Apache HTTP Server Tutorial: https://httpd.apache.org/docs/2.4/en/tutorial.html

## Setting up domain names and DNS

The next task is to set up domain names and DNS. Domain names are used to identify websites on the Internet. They are usually in the form of ```www.example.com```.

DNS is the system that is used to map domain names to IP addresses. When you type a domain name into your browser, DNS is used to look up the IP address of the server that is hosting the website.

There are two parts to setting up domain names and DNS: registering the domain name and configuring DNS.

To register a domain name, you need to find a domain name registrar. This is a company that sells domain names. Once you have found a registrar, you can search for available domain names and purchase one.

Once you have registered a domain name, you need to configure DNS. This can be done using the ```dig``` and ```nslookup``` commands. For more information, please see the following resources:

- How to Use the Dig Command on Linux: https://www.howtogeek.com/427654/htg-explains-what-is-dig-and-how-to-use-it/
- How to Use the NSlookup Command on Linux: https://www.howtogeek.com/427950/htg-explains-what-is-nslookup-and-how-to-use-it/

## Managing user accounts

The next task is to manage user accounts. On a Linux server, there are two types of user accounts: system accounts and user accounts.

System accounts are used by the system to run certain services. They usually have a numeric UID and are not intended to be used by human users.

User accounts are used by human users to log in to the system. They usually have a username and a password.

To manage user accounts, you can use the ```useradd```, ```usermod```, and ```userdel``` commands. For more information, please see the following resources:

- How to Add and Delete Users on a Linux VPS: https://www.digitalocean.com/community/tutorials/how-to-add-and-delete-users-on-a-linux-vps
- How to Change a User's Password in Linux: https://www.digitalocean.com/community/tutorials/how-to-change-a-user-s-password-in-linux

## Securing the server

The next task is to secure the server. There are many ways to secure a Linux server, but we will cover the most common ones.

The first way to secure a server is to install a firewall. A firewall is a software or hardware device that filters traffic passing through it. It can be used to block unwanted traffic and to allow only specific traffic.

The most common firewall software for Linux is iptables. Other popular firewalls include firewalld and ufw.

The second way to secure a server is to encrypt communications. The most common way to do this is to use SSL/TLS. SSL/TLS is a protocol that is used to encrypt communication between a server and a client.

To encrypt communications, you need to generate a certificate. A certificate is a file that contains information about the server and the encryption key. The certificate is then used by the server and the client to encrypt and decrypt communication.

To generate a certificate, you can use the ```openssl``` command. For more information, please see the following resources:

- How To Install an SSL/TLS Certificate In Apache: https://www.digitalocean.com/community/tutorials/how-to-install-an-ssl-certificate-from-a-commercial-certificate-authority
- How To Create a Self-Signed SSL Certificate for Apache in CentOS 7: https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-apache-in-centos-7

The third way to secure a server is to use a security scanner. A security scanner is a tool that is used to scan a system for security vulnerabilities. The most popular security scanner for Linux is Nessus.

For more information on securing a Linux server, please see the following resources:

- How To Secure a Server with Firewall Rules: https://www.digitalocean.com/community/tutorials/how-to-secure-a-server-with-firewall-rules-ufw
- How To Set Up a Firewall with UFW on an Ubuntu and Debian Cloud Server: https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-with-ufw-on-an-ubuntu-and-debian-cloud-server
- How To Harden SSH on an Ubuntu VPS: https://www.digitalocean.com/community/tutorials/how-to-harden-ssh-on-an-ubuntu-vps

## Backup and disaster recovery

The next task is to set up a backup and disaster recovery plan. There are many different ways to do this, but we will cover the most common ones.

The first way to set up a backup is to use a tool called ```rsync```. ```rsync``` is a tool that can be used to copy files from one location to another. It can be used to create backups of files and directories.

The second way to set up a backup is to use a tool called ```tar```. ```tar``` is a tool that can be used to create archives of files and directories. Archives can be used to compress files and to make backups.

The third way to set up a backup is to use a tool called ```dd```. ```dd``` is a tool that can be used to create disk images. Disk images can be used to backup entire partitions or disks.

For more information on backing up a Linux server, please see the following resources:

- How To Backup Your Server Files Using ```rsync```: https://www.digitalocean.com/community/tutorials/how-to-backup-your-server-files-using-rsync
- How To Backup Your Server Using ```tar```: https://www.digitalocean.com/community/tutorials/how-to-backup-your-server-using-tar
- How To Backup Your Server Using ```dd```: https://www.digitalocean.com/community/tutorials/how-to-backup-your-server-using-dd

The second part of setting up a backup and disaster recovery plan is to create a disaster recovery plan. This plan should outline how to recover from a major disaster, such as a server failure.

The first step in creating a disaster recovery plan is to identify the critical components of the system. This includes the web server software, the database software, and the data.

The second step is to identify the backup methods that will be used. This includes the tools that will be used to create the backups, the frequency of the backups, and the location of the backups.

The third step is to identify the recovery methods that will be used. This includes the tools that will be used to restore the backups, the order in which the components will be recovered, and the location of the backups.

For more information on creating a disaster recovery plan, please see the following resources:

- How To Create a Website Disaster Recovery Plan: https://www.digitalocean.com/community/tutorials/how-to-create-a-website-disaster-recovery-plan
- How To Prepare for a Server Migration: https://www.digitalocean.com/community/tutorials/how-to-prepare-for-a-server-migration

## Monitoring the server

The final task is to monitor the server. This includes monitoring the server's resources, such as CPU, memory, and disk usage, and monitoring the server's services, such as the web server and the database server.

There are many tools that can be used to monitor a server. Some of the most popular tools are:

- top
- htop
- iotop
- vmstat
- netstat

For more information on monitoring a Linux server, please see the following resources:

- How To Monitor System Metrics with ```netdata``` on Ubuntu 16.04: https://www.digitalocean.com/community/tutorials/how-to-monitor-system-metrics-with-netdata-on-ubuntu-16-04
- How To Monitor Your Server Resources with ```glances``` on Ubuntu 16.04: https://www.digitalocean.com/community/tutorials/how-to-monitor-your-server-resources-with-glances-on-ubuntu-16-04

## External resources

- https://www.digitalocean.com/community/tutorials/an-overview-of-linux-web-server-administration
- https://www.digitalocean.com/community/tutorials/an-overview-of-linux-server-administration
- https://www.digitalocean.com/community/tutorials/an-overview-of-linux-database-administration