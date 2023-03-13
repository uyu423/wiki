---
title: How to Use Nmap: A Beginner's Guide to Network Scanning
description: 
published: true
date: 2023-03-13T23:33:23.822Z
tags: 
editor: markdown
dateCreated: 2023-03-13T23:33:23.822Z
---

- [Nmap 사용 방법: 네트워크 스캐닝 초보자 가이드***Korean** document is available*](/ko/Knowledge-base/Network/how-to-use-nmap-a-beginner-s-guide-to-network-scanning)
{.links-list}

# How to Use Nmap: A Beginner's Guide to Network Scanning

Network scanning is a vital part of cybersecurity, as it allows you to identify vulnerabilities and potential attack vectors. Nmap is a powerful tool that can help you perform network scans and gather information about the devices on your network. In this beginner's guide, we will cover the basics of Nmap and show you how to use it to conduct network scans.

## What is Nmap?

Nmap is a free and open-source network exploration and security auditing tool. It is often used by network administrators and security professionals to discover hosts and services on a computer network, thus creating a "map" of the network. Nmap uses raw IP packets to determine which hosts are available on the network, what services those hosts are offering, and what operating systems they are running. Nmap can be used for a variety of purposes, including network inventory, managing service upgrade schedules, and monitoring host or service uptime.

## Installing Nmap

Before you begin using Nmap, you must first install it. Nmap is available for Windows, Linux, and Mac OS X, and can be downloaded from the official Nmap website. Once you have downloaded the appropriate package, you can install Nmap by following the instructions provided in the documentation.

## Basic Nmap Commands

Once you have installed Nmap, you can begin using it to scan your network. Here are some basic Nmap commands that you can use to get started:

- ```nmap [target]``` - This command will scan the target IP address or hostname and return information about the open ports and services on the target.

- ```nmap -sS [target]``` - This command will use a TCP SYN scan to determine which ports are open on the target. This is the default scan type if no other options are specified.

- ```nmap -sU [target]``` - This command will use a UDP scan to determine which ports are open on the target.

- ```nmap -O [target]``` - This command will attempt to determine the operating system of the target.

- ```nmap -A [target]``` - This command will attempt to determine the operating system, software versions, and other information about the target.

- ```nmap -v [target]``` - This command will display verbose output, providing more detailed information about the scan.

## Nmap Output

When you run an Nmap scan, the results will be displayed in the terminal window. The output will include information about the open ports and services on the target, the operating system and software versions (if detected), and other relevant information.

Here is an example of the output from an Nmap scan:

```
Starting Nmap 7.60 ( https://nmap.org ) at 2021-07-01 15:33 EDT
Nmap scan report for 192.168.1.1
Host is up (0.0011s latency).
Not shown: 996 closed ports
PORT     STATE SERVICE
21/tcp   open  ftp
22/tcp   open  ssh
23/tcp   open  telnet
80/tcp   open  http
443/tcp  open  https
MAC Address: 00:01:02:03:04:05 (Some Company)

Nmap done: 1 IP address (1 host up) scanned in 0.10 seconds
```

## Advanced Nmap Techniques

Nmap is a powerful tool that can be used for more than just basic network scanning. Here are some advanced Nmap techniques that you can use to enhance your network scans:

### NSE Scripts

Nmap includes a built-in scripting engine called the Nmap Scripting Engine (NSE). NSE scripts can be used to automate common tasks, such as vulnerability scanning and exploit detection. NSE scripts are written in the Lua programming language and can be found in the ```/usr/share/nmap/scripts``` directory (on Linux systems).

To use an NSE script, you simply specify the script name with the ```--script``` option. For example, to use the ```http-vuln-cve2015-1635``` script to scan for the MS15-034 vulnerability on a target, you would use the following command:

```nmap --script http-vuln-cve2015-1635 [target]```

### Zenmap

Zenmap is a graphical user interface for Nmap that allows you to easily configure and run Nmap scans. Zenmap provides a number of features that make it easier to use Nmap, including a topology map that shows the network layout and the results of the Nmap scan.

Zenmap can be run on Windows, Linux, and Mac OS X, and can be downloaded from the official Nmap website.

### Custom Scan Profiles

Nmap allows you to create custom scan profiles that can be used to specify specific scan options and targets. Custom scan profiles can be useful if you frequently perform scans with the same options, as they can save you time and effort.

To create a custom scan profile, you must first create a file in the ```/usr/share/nmap/nselib/data``` directory (on Linux systems) that contains the options you want to use. For example, if you wanted to create a scan profile that performs a TCP SYN scan and includes verbose output, you would create a file called ```myscan.nse``` with the following contents:

```
--myscan.nse
nmap --sS -v
```

You could then run the scan profile by using the following command:

```nmap --script myscan [target]```

## Conclusion

Nmap is a powerful tool that can be used to perform network scans and gather information about the devices on your network. By using the basic commands and advanced techniques covered in this guide, you can gain a deeper understanding of your network and identify potential vulnerabilities. To learn more about Nmap and how it can be used for network security, check out the external resources listed below.

## External Resources

- [Nmap.org](https://nmap.org/)
- [Nmap Reference Guide](https://nmap.org/book/man.html)
- [Nmap Network Scanning: The Official Nmap Project Guide to Network Discovery and Security Scanning](https://www.amazon.com/Nmap-Network-Scanning-Official-Discovery/dp/0979958717) (book)