---
title: DNS Fundamentals: How Domain Name Resolution Works
description: 
published: true
date: 2023-03-12T04:32:27.285Z
tags: 
editor: markdown
dateCreated: 2023-03-12T04:32:27.285Z
---

- [DNS 기본 사항: 도메인 이름 확인 작동 방식***Korean** document is available*](/ko/Knowledge-base/Network/dns-fundamentals-how-domain-name-resolution-works)
{.links-list}

DNS Fundamentals: How Domain Name Resolution Works

If you have ever used a computer or the internet, you have interacted with DNS, even if you didn't realize it. DNS stands for Domain Name System, and it serves as the internet's address book. When you type a URL into your browser, the DNS translates the human-readable domain name into an IP address that your computer can understand. In this article, we will explore the fundamentals of DNS, how it works, and why it's important.

## What is DNS?

DNS is a distributed database that maps domain names to IP addresses. It allows users to access websites and services using easy-to-remember domain names instead of having to remember the IP addresses of each website. DNS servers are responsible for storing and maintaining this information, and they work together to provide users with the correct IP address for a given domain name.

## How does DNS work?

When you enter a URL into your browser, your computer sends a DNS request to a DNS server to resolve the domain name into an IP address. This request gets passed up the chain until it reaches a DNS server that has the information it needs to resolve the domain name. This process is known as recursive resolution.

### DNS Records

DNS servers store and retrieve information using DNS records. DNS records contain information such as the IP address associated with a domain name, the type of record, and the time-to-live (TTL) value. The most common DNS records are:

- A Record: Maps a domain name to an IP address.
- CNAME Record: Maps an alias or subdomain to another domain name.
- MX Record: Specifies the mail server responsible for accepting email messages for a domain.

### DNS Caching

To speed up the DNS resolution process, DNS servers use caching. When a DNS server successfully resolves a domain name to an IP address, it stores that information in its cache. The next time a request is made for that domain name, the DNS server can use the cached information instead of having to go through the entire resolution process again. The TTL value in the DNS record determines how long the information is cached.

## DNS Hierarchy

The DNS system is hierarchical, meaning that it's organized in a tree-like structure. At the top of the hierarchy are the root DNS servers, which store information about the top-level domains (TLDs) such as .com, .org, and .edu. Below the root DNS servers are the TLD DNS servers, which store information about the second-level domains, such as google.com or apple.com. Finally, there are the authoritative DNS servers, which store information about specific domain names.

## DNS Security

DNS is a critical component of the internet infrastructure, and it's also vulnerable to attacks. One common attack on DNS is DNS spoofing, where an attacker intercepts a DNS request and responds with a fake IP address. To prevent these attacks, DNSSEC (DNS Security Extensions) was developed. DNSSEC is a set of protocols that adds digital signatures to DNS records to ensure that they are not tampered with during transmission.

## Conclusion

In conclusion, DNS is a critical component of the internet infrastructure that allows users to access websites and services using easy-to-remember domain names. DNS servers work together to resolve domain names into IP addresses using recursive resolution and caching. The DNS system is hierarchical, and it's vulnerable to attacks such as DNS spoofing. DNSSEC provides a way to protect against these attacks by adding digital signatures to DNS records.

External Resources:

- [DNS Explained: How the Internet Finds Your Website](https://www.cloudflare.com/learning/dns/what-is-dns/)
- [DNS Records Explained with Examples](https://www.cloudflare.com/learning/dns/dns-records/)
- [DNS Cache and How It Works](https://www.cloudflare.com/learning/dns/glossary/dns-cache/)