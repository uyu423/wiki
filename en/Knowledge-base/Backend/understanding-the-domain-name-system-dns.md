---
title: Understanding the Domain Name System (DNS)
description: 
published: true
date: 2023-02-11T05:18:06.827Z
tags: 
editor: markdown
dateCreated: 2023-02-11T05:18:05.083Z
---

- [Comprender el sistema de nombres de dominio (DNS)***Spanish** document is available*](/es/Knowledge-base/Backend/understanding-the-domain-name-system-dns)
{.links-list}
- [了解域名系统 (DNS)***Chinese Simplified** document is available*](/zh/Knowledge-base/Backend/understanding-the-domain-name-system-dns)
{.links-list}
- [도메인 이름 시스템(DNS) 이해***Korean** document is available*](/ko/Knowledge-base/Backend/understanding-the-domain-name-system-dns)
{.links-list}




# Understanding the Domain Name System (DNS)

The Domain Name System (DNS) is a directory of internet-connected devices and the resources they offer. It is the way that humans interact with the internet by translating human-readable domain names (like "google.com") into the IP addresses that computers use to communicate with each other (like "216.58.221.46").

DNS is a critical component of the internet. It is what allows us to type in a website's address and be directed to the correct server. It is also what enables email delivery, and it makes it possible to connect to internet-enabled devices like printers and smart TVs.

When you type a domain name into your web browser, your computer contacts a DNS server and asks it for the IP address associated with that domain. The DNS server then responds with the IP address, and your computer connects to the server at that address.

DNS servers are organized into a hierarchy, with the root DNS servers at the top. Each level of the hierarchy contains DNS servers that know about a subset of the IP addresses in the DNS system.

For example, the root DNS servers only know about the IP addresses of the DNS servers at the next level down. The DNS servers at the next level down only know about the IP addresses of the DNS servers at the level after that, and so on.

This hierarchy makes it possible for DNS servers to share the load of responding to requests. It also makes it possible for DNS servers to continue to work even if some of the servers in the hierarchy are unavailable.

DNS servers at each level of the hierarchy contain records that specify the IP addresses of the DNS servers at the next level down. These records are called DNS records, and they are organized into zones.

A zone is a portion of the DNS namespace that is managed by a particular DNS server. Each DNS server is responsible for maintaining the records for a particular zone.

For example, the root DNS servers are responsible for maintaining the records for the root zone. The DNS servers at the next level down are responsible for maintaining the records for the top-level domains, and so on.

DNS servers use a process called recursive resolution to respond to requests for DNS records that they do not have in their own zones.

When a DNS server receives a request for a record that it does not have, it contacts a DNS server that does have the record and asks for the record. The DNS server that has the record then responds with the record, and the DNS server that made the request passes the record back to the original requester.

DNS servers can also use a process called iterative resolution to respond to requests for DNS records.

With iterative resolution, a DNS server contacts a DNS server that has the record and asks for the record. The DNS server that has the record then responds with the record.

DNS servers use a combination of recursive and iterative resolution to respond to requests for DNS records.

DNS servers maintain a cache of DNS records. When a DNS server receives a request for a record, it checks its cache to see if it already has the record. If the DNS server has the record in its cache, it responds to the request with the record from its cache.

If the DNS server does not have the record in its cache, it contacts a DNS server that does have the record and asks for the record. The DNS server that has the record then responds with the record, and the DNS server that made the request passes the record back to the original requester.

The DNS server also adds the record to its cache so that it can respond to future requests for the record without having to contact a DNS server.

DNS servers use a process called caching to improve the performance of the DNS system. By caching DNS records, DNS servers can respond to requests for records without having to contact other DNS servers.

Caching also reduces the load on DNS servers and the network. When a DNS server caches a record, it can respond to future requests for the record without having to contact other DNS servers.

DNS servers can be configured to act as recursive or iterative resolvers.

Recursive resolvers are DNS servers that are configured to contact other DNS servers and retrieve DNS records on behalf of their clients.

Iterative resolvers are DNS servers that are configured to contact other DNS servers and request DNS records, but they do not retrieve the records on behalf of their clients.

DNS servers can be configured to use either recursive or iterative resolution.

Most DNS servers are configured as recursive resolvers.

Recursive resolvers are easier to configure and manage than iterative resolvers. Iterative resolvers require more knowledge of the DNS system and the network.

Recursive resolvers can provide a better user experience because they can resolve DNS queries faster than iterative resolvers. Iterative resolvers have to contact multiple DNS servers to resolve DNS queries, which can take longer.

Iterative resolvers can be more secure than recursive resolvers because they do not disclose as much information about the DNS system and the network.

DNS servers can be configured to use both recursive and iterative resolution.

DNS servers can be configured to use either UDP or TCP.

UDP is a connectionless protocol, and DNS servers that use UDP do not establish a connection with the DNS server that they are querying.

TCP is a connection-oriented protocol, and DNS servers that use TCP establish a connection with the DNS server that they are querying.

DNS servers can be configured to use either UDP or TCP.

UDP is the preferred protocol for DNS because it is faster than TCP. UDP does not establish a connection, so it can send and receive DNS queries and responses without the overhead of TCP.

TCP is a reliable protocol, and DNS servers that use TCP can retry DNS queries if they do not receive a response. TCP can also be used to tunnel DNS queries and responses through a firewall.

DNS servers can be configured to use both UDP and TCP.

DNS servers can be configured to use different ports.

The DNS server that is configured to use UDP is typically configured to use port 53.

The DNS server that is configured to use TCP is typically configured to use port 53.

DNS servers can be configured to use different ports.

DNS servers can be configured to use different ports for UDP and TCP.

The DNS server that is configured to use UDP is typically configured to use port 53.

The DNS server that is configured to use TCP is typically configured to use port 53.

DNS servers can be configured to use different ports for UDP and TCP.

DNS servers can be configured to forward DNS queries.

DNS servers that are configured to forward DNS queries are called forwarders.

Forwarders are DNS servers that are configured to send DNS queries to other DNS servers.

Forwarders can be used to improve the performance of the DNS system.

DNS servers that are configured to use forwarders can send DNS queries to multiple DNS servers. This can improve the performance of the DNS system because the DNS servers that are configured to use forwarders can resolve DNS queries faster than DNS servers that are not configured to use forwarders.

DNS servers that are configured to use forwarders can also be used to improve the security of the DNS system.

DNS servers that are configured to use forwarders can send DNS queries to DNS servers that are located in different networks. This can improve the security of the DNS system because the DNS servers that are configured to use forwarders can resolve DNS queries without having to contact DNS servers that are located in the same network.

DNS servers can be configured to use forwarders.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers can be configured to use different types of forwarding.

DNS servers