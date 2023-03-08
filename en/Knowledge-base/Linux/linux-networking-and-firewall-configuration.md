---
title: Linux Networking and Firewall Configuration
description: 
published: true
date: 2023-02-11T23:32:35.405Z
tags: 
editor: markdown
dateCreated: 2023-02-11T23:32:27.477Z
---

- [Configuración de red y firewall de Linux***Spanish** document is available*](/es/Knowledge-base/Linux/linux-networking-and-firewall-configuration)
{.links-list}
- [Linux 网络和防火墙配置***Chinese Simplified** document is available*](/zh/Knowledge-base/Linux/linux-networking-and-firewall-configuration)
{.links-list}
- [Linux 네트워킹 및 방화벽 구성***Korean** document is available*](/ko/Knowledge-base/Linux/linux-networking-and-firewall-configuration)
{.links-list}


# Linux Networking and Firewall Configuration

With the vast majority of threats coming from the internet, a good firewall configuration is critical for any Linux server. This guide will introduce the basics of configuring a firewall with the popular iptables tool.

## Table of Contents

- [What is a Firewall?](#what-is-a-firewall)
- [iptables](#iptables)
  - [Installing iptables](#installing-iptables)
  - [Configuring iptables](#configuring-iptables)
- [Conclusion](#conclusion)
- [Resources](#resources)

## What is a Firewall?

In computing, a firewall is a network security system that monitors and controls the incoming and outgoing network traffic based on predetermined security rules. A firewall typically establishes a barrier between a trusted internal network and an untrusted external network, such as the internet.

## iptables

Iptables is a popular firewall tool included with most Linux distributions. It uses a set of rules to determine what traffic to allow or block.

### Installing iptables

Iptables is included with most Linux distributions and can be installed with the package manager. For example, on Debian-based systems:

```
$ sudo apt-get install iptables
```

### Configuring iptables

Iptables uses a set of chains to determine what to do with a packet. A packet can be dropped, rejected, or accepted. The default chains are `INPUT`, `FORWARD`, and `OUTPUT`.

#### Rules

A rule in iptables consists of a number of match criteria and a target. The match criteria can be things like the protocol (e.g. TCP, UDP), source and destination IP addresses, and source and destination port numbers. The target can be `DROP`, `REJECT`, or `ACCEPT`.

##### Adding a rule

Rules can be added with the `iptables` command. For example, to drop all incoming traffic:

```
$ iptables -A INPUT -j DROP
```

This rule will be added to the `INPUT` chain and will have the `DROP` target, which will drop the packet.

##### Deleting a rule

Rules can be deleted with the `iptables` command. For example, to delete the previous rule:

```
$ iptables -D INPUT 1
```

This will delete the first rule in the `INPUT` chain.

##### Saving rules

Rules can be saved with the `iptables-save` command. For example:

```
$ iptables-save > /etc/iptables.rules
```

This will save the rules to the `/etc/iptables.rules` file.

##### Loading rules

Rules can be loaded with the `iptables-restore` command. For example:

```
$ iptables-restore < /etc/iptables.rules
```

This will load the rules from the `/etc/iptables.rules` file.

## Conclusion

This guide has introduced the basics of configuring a firewall with iptables. For more information, see the resources below.

## Resources

- [Iptables Tutorial](https://www.digitalocean.com/community/tutorials/a-deep-dive-into-iptables-and-netfilter-architecture)
- [How to Setup a Firewall with UFW on an Ubuntu and Debian Cloud Server](https://www.digitalocean.com/community/tutorials/how-to-setup-a-firewall-with-ufw-on-an-ubuntu-and-debian-cloud-server)
- [How to Secure Your Server with CSF Firewall on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-secure-your-server-with-csf-firewall-on-centos-7)