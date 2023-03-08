---
title: AWS Route 53: Building a Scalable and Resilient DNS System in the Cloud
description: 
published: true
date: 2023-02-06T00:55:57.693Z
tags: 
editor: markdown
dateCreated: 2023-02-06T00:55:52.151Z
---

- [AWS Route 53: creación de un sistema de DNS escalable y resistente en la nube***Spanish** document is available*](/es/Knowledge-base/Cloud/aws-route-53-building-a-scalable-and-resilient-dns-system-in-the-cloud)
{.links-list}
- [AWS Route 53：在云中构建可扩展且有弹性的 DNS 系统***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/aws-route-53-building-a-scalable-and-resilient-dns-system-in-the-cloud)
{.links-list}
- [AWS Route 53: 클라우드에서 확장 가능하고 탄력적인 DNS 시스템 구축***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-route-53-building-a-scalable-and-resilient-dns-system-in-the-cloud)
{.links-list}


# AWS Route 53: Building a Scalable and Resilient DNS System in the Cloud

DNS is a critical part of any web-based infrastructure, and Route 53 is AWS's managed DNS service. In this article, we'll take a look at how to use Route 53 to build a scalable and resilient DNS system in the cloud.

## What is DNS?

DNS is the process of translating human-readable domain names (like www.example.com) into machine-readable IP addresses (like 192.168.1.1). This is necessary because humans are much better at remembering names than numbers.

DNS is handled by DNS servers, which are responsible for maintaining a database of domain names and their associated IP addresses. When a user types a domain name into their browser, the browser will contact a DNS server to look up the IP address. The DNS server will then respond with the IP address, and the browser will connect to the web server at that IP address.

## What is Route 53?

Route 53 is AWS's managed DNS service. It is a highly available and scalable DNS service that provides a cost-effective way to route users to Internet applications. Route 53 is fully compatible with IPv6 and offers a number of features designed to make it easy to use, including:

- Health checks: Route 53 can periodically check the health of your web servers and route traffic away from servers that are unavailable.

- Latency-based routing: Route 53 can route traffic to the fastest server, based on the location of the user.

- Geolocation-based routing: Route 53 can route traffic to different servers based on the location of the user. This can be used to route users to the closest server, or to route users to different versions of your website based on their location.

- Failover: Route 53 can be configured to automatically failover to a standby server if the primary server is unavailable.

- Weighted routing: Route 53 can be configured to route traffic to different servers based on weights that you specify. This can be used to route more traffic to a new server that you're testing, or to route less traffic to a server that is experiencing problems.

## Creating a Route 53 Hosted Zone

Before you can start using Route 53, you must create a hosted zone. A hosted zone is a collection of DNS records for a single domain. For example, if you own the domain example.com, you would create a hosted zone for example.com and add DNS records to the hosted zone.

To create a hosted zone, you can use the AWS Management Console, the Route 53 API, or the AWS Command Line Interface (CLI).

## Adding DNS Records to a Route 53 Hosted Zone

Once you have created a hosted zone, you can add DNS records to the hosted zone. DNS records are used to route traffic to your website or application.

There are many different types of DNS records, but the most common type is an A record. An A record maps a domain name to an IPv4 address. For example, you could create an A record for the domain example.com that points to the IPv4 address 192.168.1.1.

To add an A record to a Route 53 hosted zone, you can use the AWS Management Console, the Route 53 API, or the AWS Command Line Interface (CLI).

## Routing Traffic to an Amazon EC2 Instance

In this section, we'll take a look at how to route traffic to an Amazon EC2 instance. Amazon EC2 is a web service that provides resizable compute capacity in the cloud.

To route traffic to an Amazon EC2 instance, you need to create an A record that points to the public IP address of the Amazon EC2 instance. The public IP address of an Amazon EC2 instance can be found in the Amazon EC2 console.

## Routing Traffic to an Amazon S3 Bucket

In this section, we'll take a look at how to route traffic to an Amazon S3 bucket. Amazon S3 is a web service that provides storage in the cloud.

To route traffic to an Amazon S3 bucket, you need to create a CNAME record that points to the Amazon S3 bucket. The Amazon S3 bucket must be configured to be accessible from the Internet.

## Route 53 Health Checks

Route 53 can be used to periodically check the health of your web servers and route traffic away from servers that are unavailable. This is known as health checking.

When you create a health check, you specify the protocol (HTTP, HTTPS, or TCP), the port, and the path or domain that you want Route 53 to use to check the health of your web server. Route 53 will then periodically send requests to the specified path or domain and check the response code to determine the health of the web server.

If you want to route traffic to a specific server based on the health of the server, you can create a health check for each server and then configure Route 53 to route traffic to the healthy servers.

## Route 53 Latency-Based Routing

Route 53 can be used to route traffic to the fastest server, based on the location of the user. This is known as latency-based routing.

To use latency-based routing, you need to create a latency resource record set for each server that you want to route traffic to. Route 53 will then periodically check the latency between the user and each server to determine the fastest server.

## Route 53 Geolocation-Based Routing

Route 53 can be used to route traffic to different servers based on the location of the user. This is known as geolocation-based routing.

To use geolocation-based routing, you need to create a geolocation resource record set for each server that you want to route traffic to. Route 53 will then use the user's location to determine which server to route traffic to.

## Route 53 Failover

Route 53 can be configured to automatically failover to a standby server if the primary server is unavailable. This is known as failover.

To use failover, you need to create a failover resource record set for each server that you want to route traffic to. Route 53 will then periodically check the health of the primary server. If the primary server is unavailable, Route 53 will route traffic to the standby server.

## Route 53 Weighted Routing

Route 53 can be configured to route traffic to different servers based on weights that you specify. This is known as weighted routing.

To use weighted routing, you need to create a weighted resource record set for each server that you want to route traffic to. Route 53 will then use the weights that you specify to determine which server to route traffic to.

## Conclusion

In this article, we've taken a look at how to use Route 53 to build a scalable and resilient DNS system in the cloud. We've seen how to create a Route 53 hosted zone, add DNS records to the hosted zone, and route traffic to Amazon EC2 and Amazon S3 instances. We've also seen how to use Route 53 health checks, latency-based routing, geolocation-based routing, failover, and weighted routing.